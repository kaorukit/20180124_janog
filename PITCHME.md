---

まずはCode化だ！

@kaorukit

---

自己紹介

@kaorukit

[NetOpsCoding](https://github.com/netops-coding/netops-tips/wiki)
からきました

---

今日話すこと

- あなたの手順書をCode化すると何が得られるのか
  - あるいは何を失うのか
- (恐らく)もっとも原始的なCode化
- そして伝説へ...

---

さいきん自動化流行ってますよね

---

なんで流行ってるんですかね？

- 自分が楽したい？ |
- 少ない人数で運用を回したい？ |
- ヒューマンエラーを無くしたい？ |

---

それって自動化のメリットではなく、

Code化のメリットだったりしませんか？？

---

そう！Code化です！

---

**Code化 is 何**

コンピューターに命令する手段

---

あれ？

スイッチのコマンドもコンピューターに命令する手段では？？

---

Yes.

コマンドを並べるだけでも、十分にCodeです

```
# ssh admin@192.0.2.1
Password:

switch> ena
Password:

switch# conf t
switch(config)# int gi 1/1
switch(interface)# ip add 198.51.100.1 255.255.255.0
switch(interface)# end
switch# wr mem
switch# exit
```

※本資料では[RFC5737](https://tools.ietf.org/html/rfc5737)で定義された資料用IPアドレスを使用します。

---

今日話すこと

- **あなたの仕事をCode化すると何が得られるのか**
  - **あるいは何を失うのか**
- (恐らく)もっとも原始的なCode化
- そして伝説へ...

---

あなたの手順書をCode化すると何が得られるのか

- 再現性の(比較的)高い手順 |

---

- 手順書
  - [人間]が[手順書]を使って[機器]を操作

- Code
  - [コンピューター]が[Code]を使って[機器]を操作

---

信頼性

コンピューター>機器>>>超えられない壁>>>人間

---

では何を失うのか

- 人間がよしなに作業出来る「遊び」 |
- 職人「CPU負荷高めだから、コマンド投入間隔を少し空けよう」 |

---

柔軟性

人間>>>超えられない壁>>>コンピューター=機器

---

Code化 is 正しい

とも限らない

---

余談

---

The presentation powered by gitpatch.

https://github.com/kaorukit/20180124_janog

---

パワポと比べると・・・

- いい感じにレイアウトしてくれるので楽
  - 自分で細かくレイアウトするのには不向き
- テキストベースなので、レビューが楽
  - 履歴も追いやすい
  - 画像を入れたら一緒だけど。。。

---

閑話休題

---

今日話すこと

- あなたの仕事をCode化すると何が得られるのか
  - あるいは何を失うのか
- **(恐らく)もっとも原始的なCode化**
- そして伝説へ...

---

pexpect

- expectのpythonパッケージ |
- 通常人間が行う対話処理をCodeで行うことが出来る |

---

さっきのコレをCode化してみましょう

```
# ssh admin@192.0.2.1
Password:

switch> ena
Password:

switch# conf t
switch(config)# int gi 1/1
switch(interface)# ip add 198.51.100.1 255.255.255.0
switch(interface)# end
switch# wr mem
switch# exit
```

---

```
import pexpect

ssh_connection = pexpect.spawn(ssh admin@192.168.0.1)

ssh_connection.expect(r"Password:")
ssh_connection.sendline("login_password")

ssh_connection.expect("switch>")
ssh_connection.sendline("ena")

ssh_connection.expect(r"Password:")
ssh_connection.sendline("enable_password")

ssh_connection.expect(r"switch#")
ssh_connection.sendline("conf t")

ssh_connection.expect(r"switch(config)#")
ssh_connection.sendline("int gi 1/1")

ssh_connection.expect(r"switch(interface)#")
ssh_connection.sendline("ip add 198.51.100.1 255.255.255.0")
ssh_connection.sendline("end")

ssh_connection.expect(r"switch#")
ssh_connection.sendline("wr mem")

ssh_connection.expect(r"switch#")
ssh_connection.sendline("exit")

ssh_connection.close()
```

@[1](pexpectモジュールをimport)
@[3](機器にsshセッションを開始)
@[5](機器の文字列出力を待機)
@[6](文字列を送信)
@[8-28](文字列待機からの文字列送信を繰り返す)
@[30](sshセッションを終了)

---

ちょっとダサいけど、直感的に理解出来ますよね・・・？

---

出来るところからCode化、どうでしょう？

---

今日話すこと

- あなたの仕事をCode化すると何が得られるのか
  - あるいは何を失うのか
- (恐らく)もっとも原始的なCode化
- **そして伝説へ...**

---

あなた「ふむ。自分もサクッとCode化始められそうだ。」

---

数日後・・・

あなた「あれ？こういう場合はどうやってCode化すればいいんだ？」

---

天の声「NetOpsCodingに参加するのです」

---

NetOpsCodingのslackは[こちら](https://docs.google.com/forms/d/1PxKlivU7cpjp_unEGyUmjWIzXUv_k6EkeVo-uWv07gY/viewform)から参加できます。

#beginner でガンガン質問してみましょう！

優しいガチ勢が教えてくれますよ！

---

Let's NetOpsCoding!

---