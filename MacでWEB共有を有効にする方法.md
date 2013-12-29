MacでWEB共有を有効にする方法
===

Mac OS X 10.7 までは「WEB共有」機能がありましたが、10.8以降はシステム設定でON/OFFに出来なくなったので、(なるべく簡単に)有効にする方法を説明します。

## ON/OFFの方法

システム環境設定の追加ペインという形で、"WEB SHARING"が公開されています。

http://clickontyler.com/web-sharing/


0. 上記ページにアクセスするか、[ここ](http://clickontyler.com/web-sharing/download/)をクリックしてダウンロードします。
0. ダウンロードしたファイル(Web Sharing.prefPane)をダブルクリックして、システム環境設定に追加します。
0. 追加された"Web Sharing"で、スイッチをONにします。
0. http://localhost にアクセス
0. /Library/WebServer/Documents 以下に置いたHTMLが参照できます。

## ユーザディレクトリを有効にする
標準のドキュメントルート( /Library/WebServer/Documents )のままだと、使いにくいケースがあるので、ホームディレクトリ内で編集できるように設定を追加します。

0. ホームディレクトリに"Sites"フォルダを作成します。`$ mkdir ~/Sites`
0. Macのターミナル(アプリ)を開きます。
0. VimでApacheの設定ファイルを開きます。 `$ sudo vim /private/etc/apache2/extra/httpd-userdir.conf`
0. 下記の設定を追記して、保存します。
0. システム環境設定 > "Web Sharing"で、スイッチを一旦OFFにして、ONにします。(=Apacheの再起動)

```
<Directory "/Users/*/Sites/">
	Options Indexes MultiViews
	AllowOverride All
	Order allow,deny
	Allow from all
</Directory>
```
以上で、ブラウザから http://localhost/~username にアクセスすると、ホームディレクトリ内のSitesフォルダを参照できるようになります。
