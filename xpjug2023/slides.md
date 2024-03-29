
## アジャイルから
## ウォーターフォールへ
## そして...

@color_box

2023/09/30
---

## 自己紹介

永和システムマネジメント
アジャイル事業部
ESM, Inc.

Twitter: @color_box
GitHub:  @colorbox

---

アジャイルプロジェクトで
ウォーターフォールみたいな仕様書の
要求に対する対応例

```note
さっそく今日話すことなんですけど
アジャイルプロジェクトで働いているときに、いきなりウォーターフォールプロジェクトみたいな
動きを要求されたらみなさんどうしますか？
今回は私が働いているプロジェトで実際に起った話とその対応について話していこうと思います。
```

---

## プロジェクト紹介

- 約10年続いているプロジェクト
- アジャイルで運営されている


```note
まず私の働いているプロジェクトについての紹介なんですが
だいたい10年くらい続いているプロジェクトです。
初期から弊社が関わっています。
```

---

## 地殻変動

リプレース

```note
大きな変化がありまして
作り直し、いわゆるリプレースってやつが始まりました、
```

---

## リプレース + 再利用

- 全面的リプレース
- 現行プロジェクトは部分的再利用

```note
リプレースプロジェクトは現行プロダクトを全面的に作り直すプロジェクトなんですが
現行プロジェクトを一部再利用して、その分作業量を減らそうという方針が最初に設定されていました。

そういうわけで現行プロジェクトとリプレースプロジェクトが協調して動くという状況になったわけですね
```

---

## ウォーターフォールへ？

- リプレースはウォーターフォール
- 現行はアジャイルによるDevOps

```note
そして、リプレースプロジェクトはウォーターフォールとして進め
現行プロジェクトはアジャイルで、従来と変わらない方式で進めるということになりました。

ある日突然アジャイルプロジェクトがウォーターフォールになるという事態にはならなかったわけです
```

---

ウォーターフォール + アジャイル

```note
そんなわけで、体外的には単一プロダクトを扱うプロジェクトの中で
リプレースプロジェクトと現行プロジェクトという2つのプロジェクトが並走し
なおかつそれらのスタイルが異なっているという。
ウォーターフォールとアジャイルが共存するという状況になったわけです
```
---

## 要仕様書

- リプレースのために仕様把握が必要
- そのための仕様書が求められた

```note
リプレースプロジェクトを進めるにあたり
現行プロジェクトの仕様を把握する必要が出てきました

リプレースなので当然現行プロダクトの仕様が必要になります。
```

---

## 仕様書はない

- 現行プロジェクトでは、動作しない中間成果物は作らない

```note
ただ、ここで問題がありまして、それは何かというと
現行プロジェクトでは、仕様書は作らない方針だったのでした。

いわゆる動作しない中間成果物というのは作らないとしていました
動作するもの、実行されるものであれば、自動テストによる確認で常にその状態を確認できるのでよいのですが
情報が書かれただけの仕様書というのはいずれ保守されなくなって内容が最新の状況を反映しなくなり、役に立たなくなってしまいます
また、ドキュメントを維持管理しようとすると、コードと仕様書とで二重管理になってしまいコストが余分にかかります。

そういった事情からただ情報が書かれただけの仕様書は基本作らないという方針にしていました
```

---

<img src="../manifest_with_doc.png" alt="manifest Image" style="width: 1000px; "/>

```note
つまりこれなんですよ
アジャイルマニフェストにもある通り、包括的なドキュメントよりも動くソフトウェアを、という方針を尊重していたわけです。
```

---

## これまでのやり方

- これまで仕様書は不要だった
- 例えば新メンバは時間をかけて仕様を把握していた
- 短時間で全仕様を把握するという必要がない

```note
そんなわけでこれまでまとまった仕様書は不要だったんですよね

たとえば新メンバが加入したときとかは
調査や実装を通して仕様を徐々に把握してもらっていくというスタイルでやっていました。
徐々にチームの平均的は仕様把握に近づいていくというやり方です

そんなわけで基本的にプロジェクトの全仕様を短時間で一気に把握しなくてはいけないという状況が存在しなかったんです
```

---

仕様把握のための資料を求められた

```note
とはいえ今回のリプレース案件で現プロジェクトの全仕様を把握する必要があります
そういった事情から仕様書はないかと要求されたわけですね
```

---


<img src="../manifest_with_doc.png" alt="Example Image" style="width: 1000px; "/>

```note
いわゆる包括的なドキュメントってやつです
```


---

## 人力対応

- リプレースで仕様書が必要
- 仕様問い合わせは人力対応

```note
ただ、求められてもないものはないので出しようがないんですよね
プロダクトを実際に触ってもらったりして分かる範囲の仕様は把握してもらい
それでもわからないような仕様については質問してもらう
という感じにしていたのですね

いわゆる人力対応でした
日に100とか来るわけではないでしょうから、対応可能な範囲に思えたのでそのようにしていました
```


---

## つらい


```note
でもやっぱりつらいんですよね
作業中に質問がちょいちょい来てしまうとその度に作業が中断してスイッチングコストが発生しますし、何より集中が途切れます
問い合わせに対応して調査、確認、返答したりする時間自体もそれなりに取られます。
```

---

## つらいのでなんとかする

```note
つらいのをそのままにするのはもっとつらいのでまぁなんとかしましょうと
```

---

## 簡易仕様書を作る

テストシナリオ名をリスト化する

```note
最初の対応としては、まずテストシナリオを一覧にして渡すことで
完全と言わないでも一部解決できないかというのを試してみました。
```

---

## テストと仕様の関係

- 仕様はチケットシステムと口頭打ち合わせを用いて整理する
- 整理した仕様をテストに落とし込む
- 自動化されたE2E(End-to-End)テストによって仕様が満たされていることを確認する


```note
現行プロジェクトにおけるテストと仕様についてお話するのですが
これまでは何らかの機能についての仕様を決めるときは主にチケットシステムと口頭での打ち合わせというものを
主に利用していました。

実現したいものの概要が書かれたチケットを作成してもらい、そのチケット上で記録を残しつつ議論して
複雑な話については口頭で補足するという流れですね
そういったやりとりを経て仕様が整理されていきます

そこで整理した仕様、期待するふるまいをE2Eテストに落とし込みます

このように、現行プロジェクトのE2Eテストは仕様を反映したものになっているわけです。
```

---

## テストについて

- 自動化E2Eテスト重視
- CIで常に監視

```note
このようにE2Eテストを書いて、修正があるごとにCIでテストを全部実行しています
コードが修正されるたびにCIによってテストが実行され、常に仕様が反映されているかを確認しています
一度策定された仕様はE2Eテストがチェックし続けるというわけですね
```

---

## E2Eテストの例

```
シナリオ: ログインしたユーザーとしてダッシュボードで
          自分の名前が表示されていることを確認できる
  前提 ユーザー 'user@example.com' がパスワード 'password1' でログインする

  ならば 'マイページ' と表示されていること
  かつ '田中太郎' と表示されていること
```

```note
現行プロジェクトで利用されているE2Eテストはこんな感じです
一定の書式に則った日本語でテスト内容を書くと
その記述内容に応じてブラウザとアプリが連動して動いて、自動で確認までしてくれます。

この例だと、サイトにログインしたあと、マイページが表示されていることを確認していますね
日本語で書かれているんですけど、これは内部的にブラウザの操作命令に変換されて、自動でテストされます。
```

---

## E2Eテストで確認していること

- 開発者が不安に思った箇所
- 仕様として満すべき挙動

```note
このE2Eテストは基本的に
開発者が不安に思った箇所
仕様として満たさねばならない挙動
とかってのをテストで担保している
そして、各E2Eテストのシナリオ名は、担保されているものを直接的に表す名前になっています。
```

---

## テストシナリオ名を仕様理解の補助にする

E2Eテストのシナリオ名は仕様読解の助けになる

```note
つまり、テストシナリオだけを抽出してまとめるだけでも
それなりの情報量になって仕様を読み解く補助になるのではないかというわけです
```

---

## 簡易な仕様書

全てのテストシナリオ名を1ファイルにまとめる

```note
というわけでプロジェクト内で定義されているE2Eテストのシナリオ名を全て1ファイルに出力しました、
```

---

## 簡易な仕様書

- E2Eテストは仕様を担保する
- そのシナリオ名は担保する仕様を表す名前である

```note
先程も話したようにE2Eテストは仕様を担保しています。
そして、そのタイトルというのは担保したい仕様を端的に表す名前になってます
そういったシナリオ名を集めて1ファイルにまとめれば
完全とまでは行かないでも、仕様書の代わりになるのではないかと思ったわけです
いわゆる簡易な仕様書、とでも言えるものができたわけですね
```

---

## 簡易な仕様書

- 仕様問い合わせは減少
- ひとまず成功

```note
とりあえずまとめたものを渡してみたところ、仕様に関する問い合わせはある程度減りました。
人力対応に必要となる労力が減ってくれて、つらさが減ったので当初の目論見は成功したといえます。
```

---

テストの中にある情報を
非エンジニアでも
利用可能な形で取り出して活用する

```note
これは何をしたのかと言うと、
テストの中にある情報を
非エンジニアでも
利用可能な形で取り出して活用する
ということをしたわけですね
```

---

## 簡易な仕様の問題点

```note
ただ、この対応に問題がないわけではないんですよね
```

---

## テキストオンリー

情報量が少ない

```note
何が問題かというと、大きなものとしては情報量が少ないという点です
記述されている仕様を満たすためにどのような操作をしているのか？
とか、操作をした結果どのような挙動をするのか？
とか
テキストからでは読み取れない情報がこの簡易仕様書には載ってこないわけですね
```

---

## 問題の解決

- 画像がほしい
- 現行プロジェクトのE2Eテストでスクリーンショット作成可能

```note
情報量を増やすにはどうするか？
文字情報だけだとわかりやすさに限界があります
手っ取り早いのは視覚情報ですよね
百聞は一見にしかずとの名言もありますし
画像、例えば操作中の画面を写したスクリーンショットとかがあるとよさそうですね

嬉しい事にE2Eテストで使用しているライブラリにはスクリーンショットを作成する機能があるんですね

なので、これを使用します。
```

---

## 問題の解決

- 解説もほしい
- E2Eテストの各ステップは「何をしたか」の詳細情報となる

```note
かといって画像だけだとその意味がよくわからなくなってしまいます。

画像とシナリオ名だけでは読み解けない詳細な解説がほしいですよね

テストにおいて、テストシナリオ名に書かれている仕様を確認するために、具体的に何をしているのか？

例えばユーザーはログイン後に何が見れないといけないのか？
ユーザーが通知アイコンををクリックした後はどのような表示が出るべきなのか
とか、そういったテストにおける操作の情報ですね

嬉しいことにですね、そういった情報というのもE2Eテストの中に既に記載されているのですよね
先程お見せした例にもありましたが、シナリオの中にどんなことを実行させるかという情報が入っていました。

なのでこれを使用します。
```

---

## 問題の解決

- 画像と解説をセットにして並べてHTMLとして出力する

```note
こうやって得られた画像と解説を一緒にします
そして画像と解説の組が複数得られるのですが、それらを全部並べます
さらにそれをHTMLとして出力します。

これによってひとつのテストシナリオの中で実行される手順を、画像と解説付きで並べることができるわけです

つまり、テストの実行手順を文書化できたに等しい状態になるわけですね
```

---

## 作成例

```note
そうやってできたHTMLを少しお見せします
タイトルにテストで実行する手順が書かれていて
その手順を実行した後のアプリの状態を示すものとして画像が記載されています
```

---


実行可能なテストから生成された文書は腐らない

```note
E2Eテストから文書を生成する利点というのは
実行可能なテストから生成されたファイルなので
保守されずに腐ることがないんですね

いわゆる、動作しない中間成果物、
誰も保守しなくなったためにアプリの最新状態を反映できなくなったドキュメント
みたいな悲しい文書化をなくせるんですね

なぜなら、E2Eテストから文書を作成できて、常に最新仕様を反映したものとなるためです
```


---

## ライブラリ化

```note
そして、これまで話した文書化の処理を取り出して
ライブラリとしてリリースしました
```

---

## 作ったライブラリ

ライブラリ名:siyousho(仕様書)

https://rubygems.org/gems/siyousho

<img src="../rubygems_siyousho.png" alt="Example Image" style="width: 1000px; "/>


```note
ライブラリ名は仕様書、です。
このプロジェクトはRuby on Railsで作られていて、使用言語はRubyです。
ですので、このライブラリもRubyで書きました。
動かすための条件がいくつかあるのですが、一般公開しており、誰でも使えるようになっています。
```

---

## 機能紹介

- ライブラリを入れてテストを実行するだけで
- 仕様書が全自動で作成！

```note
ライブラリの紹介なのですが

機能としてはごくごく単純です
このライブラリを入れてテスト実行するだけで
先程紹介したような仕様書を全自動で生成できます。
```

---

## 作ったライブラリについて

- 1シナリオ1仕様書
- ブラウザさえあれば最新仕様を確認可能
- 新規参画者への情報共有にも応用可能

```note
シナリオ一つにつき1つのHTMLファイルを生成します
HTMLで出力しているので、非エンジニアでも仕様を確認できるようになっています。
E2Eテストに入っている情報を読み出しやすく加工しているというわけです

例えばプロジェクトの新しく入った方、特に非エンジニアの方への仕様説明資料などにも活用可能というわけですね
もちろんエンジニアの人でも、テストの挙動をざっくりと確認したいといったときにも使えそうです
```


---

## オチ

```note
まず初めに言うと、さっきのライブラリとそれによって生成された仕様書は
結局仕事で活用されることはありませんでした。
```

---

## アジャイルから
## ウォーターフォールへ
## そして


```note
突然なのですが
最初に話した発表タイトルは不完全なものだったので
完全なタイトルを発表させていただきます。
最初にお見せした発表のタイトルは
「アジャイルからウォーターフォールへ、そして」
でした
```

---

## アジャイルから
## ウォーターフォールへ
## そして
# メテオフォール


```note
正式名称は
アジャイルからウォーターフォールへ
そしてメテオフォール
というタイトルでした。
```

---

## メテオフォール

- 上層部の判断による大幅な方針変換
- 生成した仕様書が不要に

```note
だいたい何が起きたか感づいた方もいるかと思うのですが
プロジェクトの大幅な方針変換が行われたわけです
メテオフォールというやつですね

一番最初にプロジェクトのリプレース案件に伴って、仕様書だのが必要になったという話をしたかと思います。
現行プロジェクトを一部再利用するため、その仕様書が必要になるというこちでした
しあｋし、この方針変更で現行プロジェクトを再利用するという話が全部消えてしまいました
今回作成した仕様書が使われることはきれいさっぱりなくなってしまったわけです。

残ったのは作ったライブラリだけというわけですね
```

---

## まとめ

- テストの中の情報を活用する
- そのために丁寧なテストコードが必要

```note
はいまとめです


今回は
マンパワーではなく技術で解決しようね、といった話や
テスト、特にE2Eテストに書かれた情報を活用して仕様の補助資料を作る、という話をさせていただきました。

一番伝えたいこととしましては、テストを丁寧に書くことの重要性ですね
テストを仕様の確認をするように記述することで、仕様書の近似的な存在にできます。
そのように丁寧に書いたテストはプロジェクトの情報資源として活用可能になります。

なので、E2Eテストは丁寧に書きましょう！

発表は以上となります。

今日お話した内容がどなたかのお役に立てば幸いです。

ありがとうございました。
```
