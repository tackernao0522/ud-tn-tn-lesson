## 40. メニューを作成しよう

+ WP管理画面 => `プラグイン` => `新規追加` => `プラグインの検索` => `admin bar bottom`と入力<br>

+ `Admin Bar Position`をインストールする<br>

+ サイトにアクセスすると管理ツールバーが下に移っている<br>

+ `myblog/function.php`を編集<br>

```php:function.php
<?php
add_action('init', function () {
  // add_theme_support('titile-tag');
  add_theme_support(('post-thumbnails'));

  // メニューをサポート
  register_nav_menus([
    'global_nav' => 'グローバルナビゲーション'
  ]);
});

/* アイキャッチ画像がなければ、標準画像を取得する */
function get_eyecatch_with_default()
{
  if (has_post_thumbnail()) :
    $id = get_post_thumbnail_id();
    $img = wp_get_attachment_image_src($id, 'large');
  else :
    $img = array(get_template_directory_uri() . '/img/post-bg.jpg');
  endif;

  return $img;
}
```

+ WP管理画面をリロードしてみると `外観` => `メニュー`というのが追加されているので`メニュー`をクリック<br>

+ `位置を管理` => `グローバルナビゲーション` と `function.php`に記述した内容が反映されている<br>

+ `メニューを編集`をクリック => `編集するメニュー選択`で`All Pages Flat`を選択して無視してもいいし、若しくは`選択` => `メニューを削除`をクリックする<br>

+ これを繰り返して`widget_page_menu`以外を削除していく<br>

+ `新しいメニューを作成しましょう`をクリック<br>

+ `メニュー名` => `グローバルナビゲーション`と入力<br>

+ `メニューを作成`をクリック<br>

+ `メニュー項目を追加` => `カスタムリンク` => `URL` => `/`と入力する => `リング文字列` => `ホーム`と入力 => `メニューに追加`をクリック<br>

+ `メニュー項目を追加` => `カテゴリー` => `ブログ`を選択 => `メニューに追加`をクリック<br>

+ `メニュー項目を追加` => `固定ページ` => `お問い合わせ`を選択 => `メニューに追加`をクリック<br>

+ `メニュー設定` => `グローバルナビゲーション`を選択 => `メニューを保存`をクリック<br>
