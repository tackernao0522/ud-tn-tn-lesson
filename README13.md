## 32. パーマリングの仕組みを知ろう

+ WP管理画面の `設定` => `パーマリング` => `月と投稿名`にチェックを入れる => `変更を保存`をクリック<br>

+ WP管理画面の `固定ページ`に新しいタイトルで `テスト`を入力して作成する<br>

+ WP管理画面の `固定ページ`のタイトル `テスト`の編集画面を開く<br>

+ 右の `固定ページ` => `パーマリング` => `URL スラッグ` => `test`に変更して更新ボタンをクリック<br>

+ `http://mysite.local/test/`になる<br>

+ WP管理画面の `固定ページ`に新しいタイトルで `お問い合わせ`を入力して作成する<br>

+ `下書き保存`をクリック<br>

+ 右の `固定ページ` => `パーマリング` => `URL スラッグ` => `contact`に変更して更新ボタンをクリック<br>

+ `公開`をクリック<br>

+ 再度 `公開`をクリック<br>

+ `http://mysite.local/contact/`となる<br>

#### 階層構造を作成するには

+ WP管理画面の `固定ページ` => お問い合わせの編集画面の => 右側の`固定ページ` => `ページ属性` => `親ページ` => `about`を選択 => `更新`をクリック<br>

+ `http://mysite.local/about/contact/`となる<br>

#### 投稿ページのパーマリンク編集

+ WP管理画面の `設定` => `パーマリング` => `カスタム構造`にチェックを入れる<br>

+ `/`を先頭に入力<br>

+ `%year%`を選択 => `%monthnum%`を選択 => `%post_id%`を選択 => `/%year%/%monthnum%/%post_id%/`のようになる<br>

+ `変更を保存`をクリック<br>

+ `http://mysite.local/2022/08/13/`のように投稿画面はなる<br>

## 33. MW WP Formを使ってお問い合わせフォームを作ろう

+ WP管理画面の `プラグイン`をクリック<br>

+ `新規追加`をクリック<br>

+ 代表的なプラグインは `contact form 7` or `mw wp form` or `snow monkey forms` だが今回は`mw wp form`をインストールする<br>

+ `有効化`しておく<br>

+ WP管理画面の `MW WP Form`をクリック<br>

+ `新規追加`をクリック<br>

+ `タイトルを追加`の欄に `お問い合わせ`と入力<br>

+ `テキスト`モードを選択して<br>

+ `お名前`と入力して プルダウンから`テキストフィールド`を選択して`お名前`の次の次の段落へ移動して`フォームタグを追加`をクリック<br>

+ `name*`に`myname`と入力してみる => `Insert`をクリックすると下記のようになる<br>

```
お名前

[mwform_text name="myname" size="60"]
```

+ 改行を2つして `お問い合わせ内容`と入力してプルダウンで `テキストエリア`を選択して `フォームタグを追加`をクリック<br>

+ `name*`に `message`として入力して `Insert`をクリックすると下記のようになればOK<br>

```
お名前

[mwform_text name="myname" size="60"]

お問い合わせ内容

[mwform_textarea name="message" cols="50" rows="5"]
```

+ プルダウンで `確認ボタン`を選択して `フォームタグを追加`をクリックする<br>

+ そのまま `Insert`をクリックして下記のようになる<br>

```
お名前

[mwform_text name="myname" size="60"]

お問い合わせ内容

[mwform_textarea name="message" cols="50" rows="5"]

[mwform_bconfirm value="confirm"]確認画面へ[/mwform_bconfirm]
```

+ そのままの行で `戻るボタン` => `Insert` => `送信ボタン` => `Insert`する<br>

```
お名前

[mwform_text name="myname" size="60"]

お問い合わせ内容

[mwform_textarea name="message" cols="50" rows="5"]

[mwform_bconfirm value="confirm"]確認画面へ[/mwform_bconfirm][mwform_bback value="back"]戻る[/mwform_bback][mwform_bsubmit name="mwform_bsubmit-474" value="send"]送信する[/mwform_bsubmit]
```

+ `公開`をクリック<br>

+ `フォーム識別子`をコピーしておく `[mwform_formkey key="37"]`<br>

+ `固定ページ`に新規追加する (取り敢えず `お問い合わせ と テストを削除しておいてaboutのみにしてから) タイトルに `お問い合わせ`と入力する<br>

+ 内容のエリアに フォーム識別子をペーストする<br>

```
お問い合わせは、こちらのフォームに記述してください。

[mwform_formkey key="37"]
```

+ `下書き保存`をクリックして `パーマリンク`の設定をする<br>

+ `URL スラッグ`を `contact`に変更して `公開する`をクリック<br>

+ 再度 `公開`をクリック<br>

+ http://mysite.local/contact/ にアクセスすると お問い合わせフォームが表示される<br>

+ WP管理画面の `MW WP Form` をクリック<br>

+ `完了画面メッセージ`(ビジュアルモード) => `お問い合わせありがとうございました。`と入力する => 中央揃えにしてみる(完了画面に表示される)<br>

+ `バリデーションリール` => `バリデーションルールを追加`をクリック<br>

+ `バリデーションを適用する項目`(属性を入れる) => `myname` => `必須項目`にチェック<br>

+ `バリデーションを追加`をクリック<br>

+ `バリデーションを適用する項目`(属性を入れる) => `message` => `必須項目`にチェック<br>

+ `更新`をクリック<br>

+ http://mysite.local/contact/ にアクセスして何も入力しないで`確認画面へ`をクリックしてバリデーションが有効か確認してみる<br>

+ 各フィールドの `未入力です`という警告が出ればOK<br>

+ 右側の `自動返信メール設定` => `件名` => `お問い合わせありがとうございました。`と入力する<br>

+ `送信者` => `Taka-Project`と入力してみる<br>

+ `Reply-to ( E-mail address )`に `takaki55730317@gmail.com`と入力してみる<br>

+ `本文`に以下のように入力してみる<br>

```
以下の内容で送信されました。

名前: {myname}
お問い合わせ内容
{message}
```

+ `送信元` => Reply to のアドレスと同じにしても良い<br>

+ `管理者メール設定` => `送信先` => `takaki55730317@gmail.com`

+ `本文`も上と同じにした<br>

+ `更新`しておく<br>
