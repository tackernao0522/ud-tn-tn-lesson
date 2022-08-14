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

## 34. お問い合わせフォームを実装しよう

+ `myblog/contact.html`の中の `<form>から</form>`までをコピーする<br>

+ WP管理画面の `MW WP Form`をクリックして前回作った `お問い合わせ`をゴミ箱に入れておく<br>

+ `新規追加` => `タイトルを追加` => `お問い合わせ`と入力する<br>

+ 内容(テキストモード) => コピーしたフォームタグをペーストする<br>

```
<form name="sentMessage" id="contactForm" novalidate>
  <div class="control-group">
    <div class="form-group floating-label-form-group controls">
      <label>Name</label>
      <input type="text" class="form-control" placeholder="Name" id="name" required data-validation-required-message="Please enter your name.">
      <p class="help-block text-danger"></p>
    </div>
  </div>
  <div class="control-group">
    <div class="form-group floating-label-form-group controls">
      <label>Email Address</label>
      <input type="email" class="form-control" placeholder="Email Address" id="email" required data-validation-required-message="Please enter your email address.">
      <p class="help-block text-danger"></p>
    </div>
  </div>
  <div class="control-group">
    <div class="form-group col-xs-12 floating-label-form-group controls">
      <label>Phone Number</label>
      <input type="tel" class="form-control" placeholder="Phone Number" id="phone" required data-validation-required-message="Please enter your phone number.">
      <p class="help-block text-danger"></p>
    </div>
  </div>
  <div class="control-group">
    <div class="form-group floating-label-form-group controls">
      <label>Message</label>
      <textarea rows="5" class="form-control" placeholder="Message" id="message" required data-validation-required-message="Please enter a message."></textarea>
      <p class="help-block text-danger"></p>
    </div>
  </div>
  <br>
  <div id="success"></div>
  <button type="submit" class="btn btn-primary" id="sendMessageButton">Send</button>
</form>
```

+ `<form>タグと閉じタグの</form>のみ削除する<br>

```
<div class="control-group">
  <div class="form-group floating-label-form-group controls">
    <label>Name</label>
    <input type="text" class="form-control" placeholder="Name" id="name" required data-validation-required-message="Please enter your name.">
    <p class="help-block text-danger"></p>
  </div>
</div>
<div class="control-group">
  <div class="form-group floating-label-form-group controls">
    <label>Email Address</label>
    <input type="email" class="form-control" placeholder="Email Address" id="email" required data-validation-required-message="Please enter your email address.">
    <p class="help-block text-danger"></p>
  </div>
</div>
<div class="control-group">
  <div class="form-group col-xs-12 floating-label-form-group controls">
    <label>Phone Number</label>
    <input type="tel" class="form-control" placeholder="Phone Number" id="phone" required data-validation-required-message="Please enter your phone number.">
    <p class="help-block text-danger"></p>
  </div>
</div>
<div class="control-group">
  <div class="form-group floating-label-form-group controls">
    <label>Message</label>
    <textarea rows="5" class="form-control" placeholder="Message" id="message" required data-validation-required-message="Please enter a message."></textarea>
    <p class="help-block text-danger"></p>
  </div>
</div>
<br>
<div id="success"></div>
<button type="submit" class="btn btn-primary" id="sendMessageButton">Send</button>
```

+ フォームの編集をする

```html:form.html
<div class="control-group">
  <div class="form-group floating-label-form-group controls">
    <label>お名前</label> <!-- 編集 -->
    <!-- 追加 テキストフィールドを選択してフォームタグを追加をクリックして name*に'myname'と入力 -->
    <!-- idに'name'と入力 classに'form-control'と入力 sizeは省略されているので消しておく -->
    <!-- placeholderに'お名前'と入力 -->
    <!-- 'Insert'をクリック -->
    [mwform_text name="myname" id="name" class="form-control" placeholder="お名前"] <!-- 追加される -->
    <!-- <input type="text" class="form-control" placeholder="Name" id="name" required data-validation-required-message="Please enter your name."> 削除する　-->
    <!-- <p class="help-block text-danger"></p>　削除する -->
  </div>
</div>
<div class="control-group">
  <div class="form-group floating-label-form-group controls">
    <label>メールアドレス</label> <!-- 編集 -->
    <!-- Email フィールドを選択して'フォームタグを追加'をクリック -->
    <!-- name* => 'email', id => 'email', class => 'form-control', size => '削除する' placeholder => 'メールアドレス' => 'Insert'をクリック -->
    [mwform_email name="email" id="email" class="form-control" placeholder="メールアドレス"] <!-- 追加される -->
    <!-- <input type="email" class="form-control" placeholder="Email Address" id="email" required data-validation-required-message="Please enter your email address.">
    <p class="help-block text-danger"></p> 削除する -->
  </div>
</div>
<!-- <div class="control-group">
  <div class="form-group col-xs-12 floating-label-form-group controls">
    <label>Phone Number</label>
    <input type="tel" class="form-control" placeholder="Phone Number" id="phone" required data-validation-required-message="Please enter your phone number.">
    <p class="help-block text-danger"></p>
  </div>
</div> 今回は削除 -->
<div class="control-group">
  <div class="form-group floating-label-form-group controls">
    <label>お問い合わせ内容</label> <!-- 編集 -->
    <!-- テキストエリアを選択して'フォームタグを追加'をクリック -->
    <!-- name* => 'message', id => 'message' class => 'form-control', colsは削除, rows => '5'のまま, placeholder => 'お問い合わせ内容' => 'Insert'をクリック -->
    [mwform_textarea name="message" id="message" class="form-control" rows="5" placeholder="お問い合わせ内容"] <!-- 追加される -->
    <!-- <textarea rows="5" class="form-control" placeholder="Message" id="message" required data-validation-required-message="Please enter a message."></textarea>
    <p class="help-block text-danger"></p> 削除する -->
  </div>
</div>
<br>
<div id="success"></div>
<!-- '確認ボタン'を選択 => 'フォームタグを追加' -->
<!-- class => 'btn btn-primary' => 'Insert'をクリック -->
<!-- 'Back Button'を選択 => 'フォームタグを追加' -->
<!-- class => 'btn btn-secondary' => 'Insert'をクリック -->
<!-- '送信ボタン'を選択 => 'フォームタグを追加' -->
<!-- name => 'send', class => 'btn btn-primary', 'Insert'をクリック -->
          [mwform_bconfirm class="btn btn-primary" value="confirm"]確認画面へ[/mwform_bconfirm][mwform_bback class="btn btn-secondary" value="back"]戻る[/mwform_bback][mwform_bsubmit name="send" class="btn btn-primary" value="send"]送信する[/mwform_bsubmit]<!-- 追加される -->
<!-- <button type="submit" class="btn btn-primary" id="sendMessageButton">Send</button> -->
```

最終的に下記のようになる<br>

```html:sample.html
<div class="control-group">
  <div class="form-group floating-label-form-group controls">
    <label>お名前</label>
    [mwform_text name="myname" id="name" class="form-control" placeholder="お名前"]
  </div>
</div>
<div class="control-group">
  <div class="form-group floating-label-form-group controls">
    <label>メールアドレス</label>
    [mwform_email name="email" id="email" class="form-control" placeholder="メールアドレス"]
  </div>
</div>
<div class="control-group">
  <div class="form-group floating-label-form-group controls">
    <label>お問い合わせ内容</label>
    [mwform_textarea name="message" id="message" class="form-control" rows="5" placeholder="お問い合わせ内容"]
  </div>
</div>
<br>
<div id="success"></div>
[mwform_bconfirm class="btn btn-primary" value="confirm"]確認画面へ[/mwform_bconfirm][mwform_bback class="btn btn-secondary" value="back"]戻る[/mwform_bback][mwform_bsubmit name="send" class="btn btn-primary" value="send"]送信する[/mwform_bsubmit]
```

+ `バリデーションルール` => `バリデーションルールを追加`をクリック<br>

+ `バリデーションと適用する項目` => `myname`<br>

+ `必須項目` => チェック<br>

+ `バリデーションルール` => `バリデーションルールを追加`をクリック<br>

+ `バリデーションと適用する項目` => `email`<br>

+ `必須項目` => チェック<br>

+ `メールアドレス` => チェック<br>

+ `バリデーションルール` => `バリデーションルールを追加`をクリック<br>

+ `バリデーションと適用する項目` => `message`<br>

+ `必須項目` => チェック<br>

+ `自動返信メール` => `email`と入力する<br>

+ `公開`をクリック<br>

+ `フォーム識別子`をコピー `[mwform_formkey key="40"]`<br>

+ `固定ページ` => `お問い合わせ`をクリック<br>

+ 下記のように編集<br>

```
お問い合わせ

お問い合わせは、こちらのフォームに記述してください。

[mwform_formkey key="40"] // コピーしたのをペーストする
```

+ `更新`をクリック<br>

+ http://mysite.local/contact/ にアクセスしてみる<br>

## 38. カテゴリーとタグについて知ろう

+ WP管理画面 => `投稿` => `カテゴリー` => `新規カテゴリー追加` => `名前`に `お買い物`と入力 `スラッグ`に `shop`と入力<br>

+ `新規カテゴリーを追加`ボタンをクリック => `名前` => `PC`と入力, `スラッグ` => `pc`と入力, `親カテゴリー` => `お買い物`を選択 => '新規カテゴリーを追加`ボタンをクリック<br>

+ WP管理画面 => `投稿` => `タグ` => `新規タグを追加` => `お買い物`と入力, `スラッグ` => `お買い物`と入力<br>

+ `新規タグを追加`ボタンをクリック => `名前` => `PC`と入力, `スラッグ` => `pc`と入力 => `新規タグを追加`ボタンをクリック<br>

+ 新規投稿のタイトルに `なにも選ばない投稿`と入力すると、右の`カテゴリー`と`タグ`を選択することができる<br>

+ `公開`ボタンをクリックするとカテゴリーは`Uncategorized`にチェックが入っているがタグは空白になっている<br>

+ `Uncategorized`のチェックを外して`更新`をクリックすると `-` になる<br>

+ `Uncategorized`にチェックが自動的に入るのは`設定` => `投稿設定` => `投稿用カテゴリーの初期設定`が `Uncategorized`になっているからである<br>

+ 一旦カテゴリーを全削除する<br>

+ `カテゴリー` => `Uncategorized`をクリック => `カテゴリーを編集` => `名前` => `ニュース(作成したサイトで一番多いものと思われるものを入力)` => `スラッグ` => `news`と入力 => `更新`をクリック<br>

+ `<-カテゴリーへ移動`をクリックすると変更されている<br>
