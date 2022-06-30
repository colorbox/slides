バグから生まれたgemの話
#### 失敗から学ぶ技術

@color_box

---

rspec-all_records_validatorのはなし

---

### プロジェクトで出たバグの話

---

### ある日突然の問い合わせ

---

### 「なんか更新機能動かないよ？」

---

なぜか特定レコードがinvalidになっていた

---

### モデル構造

```ruby
class Binder < ApplicationRecord
  has_many :documents
  validates :documents, length: {minimum: 1}
end

class Document < ApplicationRecord
  belongs_to :binder
end
```

---

Binderからdocumentsに対する関連が消失

has_many関連のlengthに対する
最小値のバリデーションによりinvalidに

---

### バリデーションをすり抜けるはなし

---

### 発生原因

結論から書くとバグ

---

## 問題のバリデーション

関連の個数に対するバリデーションは
バグですり抜けうる

```ruby
validates :documents, length: {minimum: 1}
```

---

### 再現コード

binderをそれが持つ書類ごとコピーしようとして
下記のようなコードを書いてしまう

```ruby
original_binder = binder.find(XXX)

copied_documents = original_binder.documents.each do |document|
  document.dup
end

Binder.create!(documents: copied_documents)
```

---

### バグ

```ruby
copied_documents = original_binder.documents.each do |document|
  document.dup
end
```

オリジナルのbinderのdocumentsをコピーする
`each`を使用したため
コピー元のdocumentsが移動

`map`等を使用すべき箇所だった

---

バリデーションがあるのに
すり抜けてしまう

---

同じフローを実行するE2Eテストは存在
検出できなかった

---

テスト内で`original_binder`に対する
バリデーションは実行されていれば検出できた

---

新規に作製されたレコードについてのみ実行され
古いレコードはバリデーションされない

---

`original_binder`でバリデーションが
実行されないため

### すり抜けが発生

---

自動で検出できると嬉しい

---

### こういうすり抜けをなんとかしたい

テスト終了時にDB内のすべてのレコードに対してvalidationをかけることで検出できそう

---

テスト終了時に
全レコードの
バリデーションチェック

---

## Q. 
特定レコードが
invalidになることを確認するテストはどうする？

---

# A. 無視する

---

featureやsystemのような
E2Eテストのみを対象とする

バグでない限り
ユーザー操作を模倣したテスト終了時に
invalidなデータが発生しているのはおかしい

---

### 初手、プロトタイプ、検証

ひとまずざっくりRSpecのafterフックに仕込む

```ruby
config.after do
  ApplicationRecord.subclasses.all? {|klass| 
    klass.all.each {|obj| 
      expect(obj).to be_valid 
    }
  }
end
```

---

### 雑に仕事プロジェクトに導入

テスト用のコードなので本番環境に入らない

本番には影響がなく開発/テスト環境に閉じる

最悪取り外せば良い

---

### 判明した問題

`default_scope`を使用していると正常なユーザー操作後でもinvalidになるレコードが
### 大量発生する

CI実行時間が
### 1.5倍に

---

### `default_scope`の問題

`default_scope`を使用していると
そのモデルと関連するレコードがinvalidになるのは
### 不可避

---

レコード総チェックの中で特定のモデルを
### 避けたい

---

### 実行時間の問題

全モデルをチェックする上で
不要なモデルまで処理してそう

fixtureで投入するマスターデータなどは
バリデーション不要のはず

---

レコード総チェックの中で特定のモデルを
### 避けたい

---

### モデルのフィルタ機能追加

`default_scope`絡みでinvalidになるレコードを除外
バリデーション不要なレコードを除外して高速化

---

### リリースまで

概ね機能はできたのでgemとしてリリースしたい
テストは絶対必要

---

### テストどうしよう

書きづらい

---

feature specもしくはsystem spec終了時のみ
実行したいコードのテスト
RSpecのafterでのみ実行される
コードをRSpecで実行する？

`expect`が失敗することをテストする？
`expect in expect`問題

---

どうやってテストする？

---

### 分割して対処

本質でない箇所は一旦無視
「全レコードに対してバリデーションを実行」
という部分のみテストする

---

レコードを用意して
バリデーションをかけるための場が必要
擬似的なRailsプロジェクトが必要

---

### 先人から学ぶ

テストを実行する場としてのRailsアプリが必要

DatabaseRewinder gemのテストを参考にする

小さいRailsアプリをテスト用に追加

---

`expect` in `expect` 問題

---

テスト対象コード中に`expect`があるのは明らかな
### 破綻

`expect`が失敗することを確認するテストは
### そもそも無理

---

RSpecの中で「`expect`が失敗」したら
その時点でテストは失敗する

`expect`が失敗することによって
成功するテストは書けなさそう:thinking:

---

gem内のコードとして`expect`ではなく
`validation!`を使用する

「例外が発生することを確認するテスト」は
「`expect`が失敗することを確認するテスト」
の100倍書きやすい

---

`expect` in `expect`を回避して対応

---

### リリース

そんなこんなで機能もテストも用意できたので
リリース

```console
$ rake release
```

---

### 改良編

件のバグは`has_many`関連を持つモデルでのみ発生
has_manyを持つモデルのみを対象として高速化

`ActiveRecord::Reflection::ClassMethods`
を使用することで
`has_many`関連を持つモデルを抽出できる

---

### まとめ

バグによってはバリデーションをすり抜けうる
2つのパターン

1. `default_scope`設定されたモデルの周辺モデル

2. `has_many`関連に対する個数のバリデーション

---

2 のパターンのすり抜けをテストで防止するため
rspec-allrecords_validatorを是非どうぞ
https://github.com/colorbox/rspec-all_records_validator
