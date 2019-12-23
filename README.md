## これは何？

- コードレビューの負荷を下げるため、主に新人や新規参画エンジニア向けに PrAha Inc.が使用している「PR を出す前に最低限これはチェックしてね！」というチェックシート
- 週に一度の頻度で項目を追加していく
- 追加する際は理由も記載すること！
- PrAha Inc.の場合、これに違反するとコンビニに１回パシらされる

## チェックシート

### [全般]

- console.log の消し忘れ（lint で今後弾いたらこのチェックシートから削除）

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
