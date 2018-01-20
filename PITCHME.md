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

- あなたの仕事をCode化すると何が得られるのか
  - あるいは何を失うのか
- (恐らく)一番原始的なCode化
- そして伝説へ...

---

今日話すこと

- **あなたの仕事をCode化すると何が得られるのか**
  - **あるいは何を失うのか**
- (恐らく)一番原始的なCode化
- そして伝説へ...

---

さいきん自動化流行ってますよね

---

なんで流行ってるんですかね？

- 楽したい？ |
- 少ない人数で運用を回したい？ |
- ミスを無くしたい？ |

---

それって自動化のメリットではなく、

Code化のメリットだったりしませんか？？

---

そう！Code化です！

---

**Code化 is 何**

コンピューターに命令する手段

---

あれ？ルーターのコマンドもコンピューターに命令する手段では？？

---

コマンドを並べるだけでも、十分にCodeです

```
switch# conf t
switch(config)# int gi 1/1
switch(interface)# ip add 192.168.0.1 255.255.255.0
switch(interface)# end
switch# wr mem
switch# exit
```

---

pexpectの紹介

---