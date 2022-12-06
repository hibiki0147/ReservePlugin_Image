※このリポジトリは「ReservePlugin」用の画像リポジトリです。コードは公開しておりません。

# 概要
QRコードを発行し、受付ができるプラグイン。<br>
サイト内にフォームを設置し、入力してもらったメールアドレスにQRコードを添付し、そのQRコードで受付が可能になります。

# ビルド手順
## ●環境構築
### １.サーバーの用意と「WordPress」のインストール。
・自分でサーバー（今回はローカル環境のXamppを例にする）を立て、「WordPress」が入っていないならインストールしてもらいアクセスする。<br>
[XAMPPを使ってWordPressローカル環境を構築する全手順](https://lucy.ne.jp/bazubu/xampp-wordpress-23795.html)


### ２.phpの設定変更
このプラグインはメールを送る機能と、画像を作る機能がある。<br>
しかし、サーバー側で設定されていなければ、エラーが生じるため、方法を記す。<br>
※xamppでは、初期状態ではエラーが発生する。

#### 概要
・編集するファイル<br>
php-ini<br>
sendmail.ini<br>

・必要な用意<br>
メールアカウント（パスワードをファイルに直接書き込むため、普段使いしていないものが安全かも？：今回はGmialアカウントを使用）<br>

#### 実践
php-ini:<br>
　[mail function]に<br>

　SMTP = localhost<br>
　smtp_port = 25<br>
　sendmail_path = "\"C:\xampp\sendmail\sendmail.exe\" -t"<br>
　mail.add_x_header = Off<br>
　に修正<br>

　Module Settingsに<br>

　php8 以降なら	extension=php_gd.dll<br>
　php8 より前なら	extension=php_gd2.dll<br>
　を追加<br>

　※php_gd.dellやphp_gd2.dllが「ext」に入っていないなら<br>
　[https://www.php.net/downloads.php](https://www.php.net/downloads.php)<br>
　から自分のバージョンにあったものをダウンロードする。<br>



　sendmail.ini:<br>
　sendmailに<br>

　smtp_server=smtp.gmail.com<br>
　smtp_ssl=auto<br>
　auth_username="メールアドレス"<br>
　auth_password="パスワード"<br>
　force_sender="メールアドレス"<br>
　に修正<br>

　Apatch再起動すると、メールを送ったり、画像をphpから作成できるようになる。<br>


参考にしたサイト様<br>
　【XAMPP】ローカル開発環境でメール送信をできる様にする<br>
　[https://miya-system-works.com/blog/detail/107](https://miya-system-works.com/blog/detail/107)<br>


　【2022年版】XAMPPのローカル環境でメールを送信する方法		（Gメールの場合　二段階承認が必須になったらしい）<br>
　[https://my-web-note.com/xampp-mail-send-php/](https://my-web-note.com/xampp-mail-send-php/)<br>



## ●ライブラリのインストール
ダウンロードしたフォルダの中の「ReservePlugin」フォルダがプラグインに当たるフォルダである。<br>
下記のURLからダウンロードそれぞれライブラリをダウンロードし、<br>


・phpqrcode<br>
[https://sourceforge.net/projects/phpqrcode/files/](https://sourceforge.net/projects/phpqrcode/files/)<br>
ダウンロード後展開し、「phpqrcode」フォルダを丸ごと「classes」フォルダへ<br>


・jsQR<br>
[https://github.com/cozmo/jsQR](https://github.com/cozmo/jsQR)<br>
ダウンロード後展開し、「docs」フォルダ内の「jsQR.js」ファイルのみ取り出し、<br>
「admin」フォルダ内に「qrcode」フォルダをつくり、その中に置く。<br>



# インストール手順
## プラグインのインストール
１.もし「ReservePlugin」フォルダが圧縮されていなければzipファイルに圧縮する。<br>

２.ブラウザでWordPressの管理画面を開けたら、左のサイドバーより、「プラグイン」を選択する。<br>

３.開いた画面で「プラグイン」と見出しが出てくるので、その右横の「新規追加」ボタンを押す。<br>

４.次も「プラグインを追加」と見出しが出てくるので、その右横の「プラグインのアップロード」ボタンを押す。<br>

５.「ZIP 形式のプラグインファイルをお持ちの場合、こちらからアップロードしてインストールまたは更新できます。」<br>
と出てくるので、「ファイルを選択」から１番で圧縮したzipファイルを選択する。<br>

６.「今すぐインストール」ボタンを押す。<br>

７.うまくいけば「プラグインのインストールが完了しました。」と出てくる。<br>
　ただインストールしたいだけであれば、「プラグインインストーラへ移動」のリンクに飛び、戻る。<br>
※インストール事態はここで終わっているのだが、機能を使いたければ「有効化」しなければならない。<br>
　ここから下はその手順を示す。<br>

８.７番で「プラグインを有効化」ボタンを押す。<br>
　（または「プラグインインストーラへ移動」のリンクに飛んだのなら、左のサイドバーより、「プラグイン」を選択し、<br>
　「ReservePlugin」と書かれてある欄の下の「有効化」を押す。）<br>

９.うまく有効化できれば、「プラグイン」という見出しの下に「プラグインを有効化しました。」と出てくる。<br>


## ●アンインストール
１.ブラウザでWordPressの管理画面を開けたら、左のサイドバーより、「プラグイン」を選択する。<br>

２.もし「ReservePlugin」が有効化されているなら「無効化」を押す。<br>

３.無効化されたなら、「削除」を押す。<br>


# 操作手順
## 1.メイン画面へ移動
「ReservePlugin」が有効化されていれば<br>
左のサイドバーに「ReservePlugin」という<br>
メニューが追加されているので、それをクリックします。<br>

![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image1.png)

## 2.メイン画面
はじめは何も表示されていませんが、テーブルを追加していきましょう<br>

![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image2.png)


テーブル名を、半角小文字数字アンダーバーのみで指定し、コメントを打ち込みます。<br>
「テーブル追加」ボタンを押すとテーブルが追加されます。<br>

![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image3.png)

テーブルの追加に成功すると、このような画面になる。（テーブル名の「wp_」はWordPressインストール時に設定した「接頭語」にあたる）<br>

テーブル名のリンクは、テーブルの詳細画面へ<br>

フォーム・メール編集、QRコードの欄のボタンはそれぞれの画面へ遷移するようになっている。<br>

テーブルを削除したい場合は、削除の欄のボタンを押していただくとその行のテーブルが削除される。<br>

![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image4.png)


## テーブルの詳細画面
テーブル名が見出しとして表示され、そのテーブルの持つ列が下に表示される。<br>
（ [id、datetime、code、address]はデフォルトで列として追加されている。）<br>
新しく列を追加したい場合は、下記を入力し、「送信」ボタンを押す。<br>

![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image5.png)

![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image6.png)


## フォーム・メール編集（フォーム）
テーブルの内容によって自動的にHTML文が作られるので必要に応じて編集する。<br>

（name属性やtype属性を変えるとうまくデーターベースに登録されない可能性があるので注意。）<br>

「送信」ボタンを押すと登録される。<br>

![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image7.png)


## フォーム・メール編集（メール）
件名と本文を入力する。<br>

「メール」ボタンを押すと入力画面が変わる。<br>

置き換え文字は、本文の内容にユーザーの入力内容を使いたいときに、活用する。<br>

※例<br>
usernameに登録した内容が「山田」ならば<br>
「{username}」は、メール本文では「山田」に置き換わる<br>

「送信」ボタンを押すと登録される。<br>

![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image8.png)


## QRコードは後に、紹介


## 固定ページに飛ぶ、作成する
左のサイドバーから「固定ページ」を選択する。<br>

既存の固定ページがある場合、固定ページのタイトルを押す。<br>
固定ページがない場合、「固定ページ」という見出しの右横の「新規追加」ボタンを押す。<br>

![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image9.png)


## ショートコードを置く
タイトルを追加に適当なタイトルを付け、ヘッダーの「＋」ボタンを押し、<br>
検索欄に「ショートコード」と入力。<br>


出てきたショートコードのアイコンをクリックすると、<br>
ショートコードのブロックが出来上がる。<br>
![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image10.png)


## ショートコードを入力する
フォーム・メール編集画面で出てきた<br>
ショートコード<br>

[ReservePlugin_FormCreate table=1]<br>

を打ち込む。<br>

※テーブルによってショートコードは変わります。作成したテーブルの編集画面を見に行きましょう。<br>

これでフォーム自体の設置は完了です。<br>

![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image11.png)

## プレビューで確認しよう
ヘッダーの「プレビュー」から「新しいタブでプレビュー」を選びます。<br>

そうすると新しいタブで実際に表示される画面が見れます。<br>
![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image12.png)


## 入力してみよう
入れているテーマなどで実際の画面は大きく変わっているかもしれませんが、フォームが設定されていることを確認します。<br>


そして自分のメールアドレスと必要な内容を入力しましょう。
（※確認画面がまだ作れていないので、誤ったメールアドレスを入力すると知らない人へメールが送られる可能性があります。注意してください。）<br>

![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image13.png)


## 送信の完了。
送信が完了すると画面が左のようになり、確認メールがQRコード付きで届く<br>

![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image14.png)

![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image15.png)


## QRコード
「ReservePlugin」の管理画面に戻り、QRコード欄の「開く」ボタンを押すと、左図のような画面に移動する。<br>

「QRコードリーダー」ボタンを押すとカメラの使用が求められる場合があるので許可。<br>

カメラを使用し、先程送られてきたQRコードをかざすと、登録内容が返ってくる。<br>

※「http」通信ではローカル環境以外だと動かない。<br>

![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image16.png)

![画像名だよ～](https://github.com/hibiki0147/ReservePlugin_Image/blob/main/Images/image17.png)


# 商標
QRコードは(株)デンソーウェーブの登録商標です。
