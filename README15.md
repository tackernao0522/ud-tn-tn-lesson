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

## 41. メニューを実装しよう

+ `myblog/includes/header.php`を編集<br>

```php:header.php
<?php wp_body_open(); ?>

<!-- Navigation -->
<nav class="navbar navbar-expand-lg navbar-light fixed-top" id="mainNav">
  <div class="container">
    <a class="navbar-brand" href="index.html">Start Bootstrap</a>
    <button class="navbar-toggler navbar-toggler-right" type="button" data-toggle="collapse" data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation">
      Menu
      <i class="fas fa-bars"></i>
    </button>
    <?php wp_nav_menu(); ?> // 追加
    <div class="collapse navbar-collapse" id="navbarResponsive">
      <ul class="navbar-nav ml-auto">
        <li class="nav-item">
          <a class="nav-link" href="index.html">ホーム</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="about.html">About</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="post.html">Sample Post</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="contact.html">Contact</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

+ [wp_nav_menu](https://wpdocs.osdn.jp/%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%82%BF%E3%82%B0/wp_nav_menu)<br>

+ サイトをリロードしてみる(メニューが表示される)<br>

+ WP管理画面 => `外観` => `メニュー` => `メニュー項目を追加` => `カテゴリー` => `マークアップ`を選択 => `メニューを追加`をクリック => `メニューを保存`<br>

+ サイトをリロードするとメニューバーに`マークアップ`が追加表示されている<br>

+ [wp_get_nav_menu_items](https://wpdocs.osdn.jp/%E9%96%A2%E6%95%B0%E3%83%AA%E3%83%95%E3%82%A1%E3%83%AC%E3%83%B3%E3%82%B9/wp_get_nav_menu_items)<br>

+ `myblog/includes/header.php`を編集<br>

```php:header.php
<?php wp_body_open(); ?>

<!-- Navigation -->
<nav class="navbar navbar-expand-lg navbar-light fixed-top" id="mainNav">
  <div class="container">
    <a class="navbar-brand" href="index.html">Start Bootstrap</a>
    <button class="navbar-toggler navbar-toggler-right" type="button" data-toggle="collapse" data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation">
      Menu
      <i class="fas fa-bars"></i>
    </button>
    // <?php wp_nav_menu(); ?> // 削除する
    // 追加
    <?php
    // メニューIDを取得する
    $menu_name = 'global_nav';
    $locations = get_nav_menu_locations();
    $menu = wp_get_nav_menu_object($locations[$menu_name]);
    // var_dump($menu); // term_id = int 159
    $menu_items = wp_get_nav_menu_items($menu->term_id);
    // var_dump($menu_items);
    ?>
    // ここまで
    <div class="collapse navbar-collapse" id="navbarResponsive">
      <ul class="navbar-nav ml-auto">
        <li class="nav-item">
          <a class="nav-link" href="index.html">ホーム</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="about.html">About</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="post.html">Sample Post</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="contact.html">Contact</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

+ `myblog/includes/header.php`を編集<br>

```php:header.php
<?php wp_body_open(); ?>

<!-- Navigation -->
<nav class="navbar navbar-expand-lg navbar-light fixed-top" id="mainNav">
  <div class="container">
    <a class="navbar-brand" href="index.html">Start Bootstrap</a>
    <button class="navbar-toggler navbar-toggler-right" type="button" data-toggle="collapse" data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation">
      Menu
      <i class="fas fa-bars"></i>
    </button>

    <?php
    // メニューIDを取得する
    $menu_name = 'global_nav';
    $locations = get_nav_menu_locations();
    $menu = wp_get_nav_menu_object($locations[$menu_name]);
    $menu_items = wp_get_nav_menu_items($menu->term_id);
    ?>

    <div class="collapse navbar-collapse" id="navbarResponsive">
      <ul class="navbar-nav ml-auto">
        // 編集
        <?php foreach ($menu_items as $item) : ?>
          <li class="nav-item">
            <a class="nav-link" href="<?php echo $item->url; ?>"><?php echo $item->title; ?></a>
          </li>
        <?php endforeach; ?>
        // ここまで
      </ul>
    </div>
  </div>
</nav>
```

+ WP管理画面 => `外観` => `メニュー` => `メニュー項目を追加` => `固定ページ` => `フロントページ`を選択 => `メニューを追加`をクリック => `メニューを保存`<br>

+ サイトをリロードするとメニューバーに`フロントページ`が追加表示されている(確認後削除)<br>
