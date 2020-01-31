## これは何？

- コードレビューの負荷を下げるため、主に新人や新規参画エンジニア向けに PrAha Inc.が使用している「PR を出す前に最低限これはチェックしてね！」というチェックシート
- 週に一度の頻度で項目を追加していく
- 追加する際は理由も記載すること！
- PrAha Inc.の場合、これに違反するとコンビニに１回パシらされる

### コードレビュー観点
100点を目指すとレビュー時間に時間が取られてしまうため60点のコードを目指す。
60点のコードレビュー観点は後でリファクタリングしやすいかどうかを元に観点を決めた。
class内でのみで使用される関数やプロパティは他のclassとの影響がなく、後でリファクタしやすいためレビューの対象にはならない。
#### レビュー観点
- interface名また、interfaceの関数名が不適切でないか
- クラスの切り方は適切か
- カプセル化はできているか

### [全般]
- 色んなところで使い回される可能性がある値を、定数化していない
  - 例：カラーコード、ディレクトリのパス、制限文字数、キューの名前、プロパティ名、クッキーに使うキーなどなど・・・
  - 理由：パスやカラーコードなど変更される可能性がある値を直接書き込むと、いざ変更された時にコードの変更箇所が増える。

- ネストを浅くする

```
NG
if (hoge) {
  //hogehoge
} else {
  //fugafuga
}

GOOD
if (hoge) {
  //hogehoge
  return
}

//fugafuga
```

理由：可読性の向上。詳しくはリーダブルコードなど参照

- 未使用の変数を残さない！消す！

- あるPR/issueの後続系PRを作成するときは、必ず対象PR/issueへのリンクを貼る
  - レビュワーが開発の流れを追いやすくなる

### [Vue]
- component を作る際、computed で済む項目を data に入れない
  - 理由：出来るだけ component には state を持たせず関数的に書くことで component の再利用性を高める


### [Node.js]
- Promiseな関数を連続で実行する（awaitを連続で書く）場合かつ並列で実行して問題ない場合は、Promise.all() を使用すること
  - 処理速度向上のため

```
NG
await aPromiseFunction()
await bPromiseFunction()

OK
await Promise.all(aPromiseFunction(), bPromiseFunction())
```

- 基本的に==ではなく===を使う
  - 意図しない等価結果を防ぐ。例えば 0 == false, '' == false はtrueになる。こういった挙動を理解した上で使えるようにするため、基本は===を習慣づける

#### [Jest]
- 要素数と文字列長をテストをする場合は、toHaveLength() を使うこと
  - 可読性の向上のため
  - ref: https://jestjs.io/docs/en/expect#tohavelengthnumber
```
NG
expect(nArray.length).toBe(0)

OK
expect(nArray).toHaveLength(0)
```
