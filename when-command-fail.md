# コマンドを間違えるたびに美少女に罵られたい！

コマンドを間違えるたびに美少女に罵られてみたい、と誰しも思ったことはありませんか？
そんな長年の夢を叶えましょう！！！

# 結果

![k.png](https://qiita-image-store.s3.amazonaws.com/0/154157/1f4d9b9a-81f9-4f68-78b4-0a646fba53ef.png)

罵ってくれました。

# 方法

## jp2aを導入する

任意のJPEG画像をアスキーアートにして表示してくれるパッケージです。
たぶん以下でインストールできます。

```bash
$ sudo apt install jp2a # for Debian,Ubuntu
$ brew install jp2a     # for MacOSX,Linuxbrew
```

## 画像を用意する

可愛い女の子の画像を用意しましょう。また、グレースケールにしておくと表示が綺麗になります。

## シェルにフックを登録する

コマンドを間違えたときに呼ばれる関数があるので、それを使いましょう。
jp2aを使い画像を表示し、その後にメッセージを表示します。

Bashの場合

```bash:bashrc
function command_not_found_handle(){
  if [ -e /usr/bin/jp2a ];then
    if [ -e ~/kirino.jpg ];then
      jp2a ~/kirino.jpg -i
    fi
  fi
  echo "ハァ…？$1とか何言ってんの？\nコマンドもろくに覚えられないなんて、アンタどうしようもないクズね。"
}
```

ZSHの場合

```bash:zshrc
function command_not_found_handler(){
  if [ -e /usr/bin/jp2a ];then
    if [ -e ~/kirino.jpg ];then
      jp2a ~/kirino.jpg -i
    fi
  fi
  echo "ハァ…？$1とか何言ってんの？\nコマンドもろくに覚えられないなんて、アンタどうしようもないクズね。"
}
```

---
fishの場合

@QUANON さんから、以下のようなコメントを頂きました！ありがとうございます！！

>僕は fish を使っているのですが、このシェルでも次の function を定義することで実現できました。

```sh
function command_not_found_handler --on-event fish_command_not_found
    if type -q jp2a; and test -e ~/kirino.jpg
        jp2a ~/kirino.jpg -i
    end

    echo ハァ…?$argv[1]とか何言ってんの?
    echo コマンドもろくに覚えられないなんて、アンタどうしようもないクズね。
end
```

bashとzshで'handle'と'handler'の違いがあるので注意です。また画像のパスは適宜変更してください。
また、jp2a自体のオプションを弄ることで、表示するときの行や列を指定することができます。
デフォルトでは、白に近い部分を表示させますが、ぼくの場合白黒にしてほとんど白となってしまい、見づらかったので、あえて黒の部分を表示させるために`-i`を付けています。

```bash
$ jp2a hoge.jpg --width=100 # 横幅を100列固定で表示
$ jp2a hoge.jpg --height=100 # 横幅を100列固定で表示
$ jp2a hoge.jpg -i # 白黒反転で表示
```

これで一通りの手順は完了です。

![k.png](https://qiita-image-store.s3.amazonaws.com/0/154157/1f4d9b9a-81f9-4f68-78b4-0a646fba53ef.png)

# もっと高解像度で罵られたい。というかもう動画がいい。

そう思った方、とても良い考え方だと思います。同士です。
次は、アスキーアートだけではなく、本当の画像やgifアニメを表示させたいと思います。

### iTerm2.appの場合

> コメント欄にて、@kuzukuzu1gou さんがiTerm2でimgcatを使う方法を教えてくれました。

![k.png](https://camo.qiitausercontent.com/6a2c90c8dbe2c8dd79267206fbfb5a0d84de3761/68747470733a2f2f71696974612d696d6167652d73746f72652e73332e616d617a6f6e6177732e636f6d2f302f34313430382f30393561643030332d396633612d386533312d356337632d6535343433666332633536632e706e67)

jp2aの部分を、そのまま`imgcat`というコマンドに置き換えれば表示できます。

```bash
$ imgcat hoge.jpg
```

### xterm mltermの場合

img2sixelというパッケージを使えば、画像の表示や、gitアニメの再生ができます。

```bash
$ img2sixel hoge.jpg
$ img2sixel hoge.gif -l disable # -l disableを付けないとアニメがループしてプロンプトが帰ってこない
```

また、任意のyoutubeや動画ファイルをgitアニメにするには以下を参考にしてください。
[Linuxで、コマンドだけでyoutubeから動画をダウンロードして任意の時間を切り出してgitアニ化する](https://qiita.com/onokatio/items/40b12a2c50b4f9cc3e75)

![k.png](https://qiita-image-store.s3.amazonaws.com/0/154157/7fbe3061-c702-8347-ccc5-eba72f469119.png)

![demo.gif](https://qiita-image-store.s3.amazonaws.com/0/154157/e95b7085-6ebd-9a22-214b-d69ab05c5663.gif)


ゾクゾクしちゃいますね。
これで楽しいシェルライフを送りましょう！
