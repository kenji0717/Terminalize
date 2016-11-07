title: memo.mm

2016,03/31: 最終版ここで作っておこう．

たぶんできたと思う．やっぱりterminalize.cssを指定してもらう
ことにした．でなるべく自分でスタイルが付けられるようにして
いる．全然スタイル付けなくても使えないことないけどちょっと
しょぼくなる．例えば以下のようにスタイルを付ける．

    #stdio {
      background: #000;
      color: #fff;
      font-family: "Osaka-mono", "Osaka-等幅", "ＭＳ ゴシック", "Consolas", "Courier New", monospace;
      font-size: 14px;
      width: 40em;
      height: 25ex;
    }

等幅フォント使いたいだけなんだけどfont-familyの設定は難しい．
あらゆる環境で「全角1文字の幅=半角2文字の幅」になるような
指定がしたいんだけど．．．上の設定ならまあまだがiPadと
Androidでちょっとずれるね．

WindowsのIE11が一番変だな．入力欄のbackgroundがinheritされない．
今Edgeも試してみたらこっちは大丈夫だね．

今残っている問題点は．．．

* 入力行の`<input>`の横幅を90%と指定しているので右端まで入力
  できない．
* 入力した文字列が長いとstdoutの部分でも上手く表示されない場合
  がある．
* ああああああ！！！！！！プロンプト付けたらまたフォントの
  問題勃発したっぽい

あと簡単な使い方の説明．

HTMLの中に，

    <div id="stdio">
    </div>

と書いといてJavaScriptで

    var term = terminalize("stdio");

でOK．1行入力された時にその入力をキャッチするための
リスナーを登録したい時は

    function inputListener(s) {
      alert(s);
    }
    var term = terminalize("stdio",inputListener);

とすれば良い．でもリスナーは後で追加したり，削除したりも
できる．(複数のリスナーを登録することもできる)
リスナーって名前にしたけど，実態は1引数の関数．

あとはtermに付いてくる関数の説明

* term.clear();
  + その名のとうりクリア
* term.addInputListener(listener);
  + リスナーの追加．リスナーは複数追加できる．
* term.removeInputListener(listener);
  + リスナーの削除．
* var s = term.read();
  + 画面に出力されている物を読み出す．(入力行は
    含まれない)
* term.echoOff();
  + デフォルトでは入力行に入力した文字列を出力に
    エコーバックするけど，これをOFFにする．
* term.echoOn();
  + OFFにしたエコーバックをONにする
* term.setPrompt("> ");
  + 入力行のプロンプトを変更する．デフォルトは"$ "．
    プロンプトを消したかったら""を指定すればOK．

それからリスナーが受けとる文字列にはプロンプトの部分は
含まれていません．

-----

* ああああああ！！！！！！プロンプト付けたらまたフォントの
  問題勃発したっぽい
