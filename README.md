# 何これ
同じ jar のバージョン違いの両方を置くことで初めて動作するとほほ例。

## 使い方
`git clone` してきたら `./gradlew jar` または `gradlew.bat jar`。

以下のファイルができあがるので...

 - hoge-1.0/build/libs/hoge-1.0.jar
 - hoge-2.4/build/libs/hoge-2.4.jar
 - program/build/libs/program-1.0.jar
 - sub1/build/libs/sub1-1.0.jar
 - sub2/build/libs/sub2-1.0.jar

適当なひとつのディレクトリに纏めて、その中で

```sh
java -cp program-1.0.jar:sub1-1.0.jar:sub2-1.0.jar:hoge-1.0.jar:hoge-2.4.jar org.example.Main
```

としてみましょう。

```
Fuga#hoge() [ver 1.0]
Fuga#bar() [ver 1.0]
Piyo#baz()
```

という出力が得られるはずです。

次は

```sh
java -cp program-1.0.jar:sub1-1.0.jar:sub2-1.0.jar:hoge-1.0.jar org.example.Main
```

としてみましょう。 hoge-2.4.jar を削ったものです。 `Piyo` が見付からんと言われて例外吐きますね。

さて今度は

```sh
java -cp program-1.0.jar:sub1-1.0.jar:sub2-1.0.jar:hoge-2.4.jar org.example.Main
```

としてみましょう。 hoge-1.0.jar を削ったものです。 `Fuga.bar()` なぞ知らんと言われてやっぱり例外発生。

最後に

```
java -cp program-1.0.jar:sub1-1.0.jar:sub2-1.0.jar:hoge-2.4.jar:hoge-1.0.jar org.example.Main
```

としてみましょう。最初の版とは hoge-1.0.jar と hoge-2.4.jar の順序が逆です。
これまた `Fuga.bar()` なぞ知らんと言われますね。あー恐ろしや。
