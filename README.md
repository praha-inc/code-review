## これは何？

- コードレビューの負荷を下げるため、主に新人や新規参画エンジニア向けに PrAha Inc.が使用している「PR を出す前に最低限これはチェックしてね！」というチェックシート
- PrAha Inc.の場合、これに違反するとコンビニに１回パシらされる

## チェックシート

### [全般]

- console.log の消し忘れ（lint で今後弾いたらこのチェックシートから削除）

- ネストを浅くする

- 未使用の変数を残さない！消す！

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

### [Vue]
- component を作る際、computed で済む項目を data に入れない。理由：出来るだけ component には state を持たせず関数的に書くことで component の再利用性を高める
