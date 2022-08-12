## 29. 投稿の個別ページ（single.php）を仕上げよう

+ `myblog/single.php`を編集<br>

```php:single.php
<!DOCTYPE html>
<html <?php language_attributes(); ?>> // 編集

<head>
  <?php get_header(); ?>
</head>

<body <?php body_class(); ?>> // 編集

  <?php wp_body_open(); ?> // 追加

  <!-- Navigation -->
  <?php get_template_part('includes/header'); ?>

  <?php if (have_posts()) : ?>
    <?php while (have_posts()) : the_post(); ?>
      <!-- Page Header -->
      <?php
      if (has_post_thumbnail()) :
        $id = get_post_thumbnail_id();
        // var_dump($id);
        $img = wp_get_attachment_image_src($id, 'large');
      // var_dump($img);
      else :
        $img = array(get_template_directory_uri() . '/img/post-bg.jpg');
      endif;
      ?>
      <header class="masthead" style="background-image: url('<?php echo $img[0]; ?>')">
        <div class="overlay"></div>
        <div class="container">
          <div class="row">
            <div class="col-lg-8 col-md-10 mx-auto">
              <div class="post-heading">
                <h1><?php the_title(); ?></h1>
                <span class="meta">Posted by
                  <?php the_author(); ?>
                  on <?php the_date(); ?></span>
              </div>
            </div>
          </div>
        </div>
      </header>

      <!-- Post Content -->
      <article>
        <div class="container">
          <div class="row">
            <div class="col-lg-8 col-md-10 mx-auto">
              <?php the_post_thumbnail(array(32, 32), array('alt' => 'アイキャッチ画像')); ?>
              <?php the_content(); ?>
            </div>
          </div>
        </div>
      </article>

      <hr>
    <?php endwhile; ?>

    <!-- <?php else : ?>
    <p>記事が見つかりませんでした</p> -->
  <?php endif; ?>

  <!-- Footer -->
  <?php get_template_part('includes/footer'); ?>

  <?php get_footer(); ?>

</body>

</html>
```

+ `myblog/includes/header.php`を編集<br>

```php:header.php
<?php wp_body_open(); ?> // 追加

<!-- Navigation -->
<nav class="navbar navbar-expand-lg navbar-light fixed-top" id="mainNav">
  <div class="container">
    <a class="navbar-brand" href="index.html">Start Bootstrap</a>
    <button class="navbar-toggler navbar-toggler-right" type="button" data-toggle="collapse" data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation">
      Menu
      <i class="fas fa-bars"></i>
    </button>
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

+ `myblog/single.php`を編集<br>

```php:single.php
<!DOCTYPE html>
<html <?php language_attributes(); ?>>

<head>
  <?php get_header(); ?>
</head>

<body <?php body_class(); ?>>

  // <?php wp_body_open(); ?> //削除

  <!-- Navigation -->
  <?php get_template_part('includes/header'); ?>

  <?php if (have_posts()) : ?>
    <?php while (have_posts()) : the_post(); ?>
      <!-- Page Header -->
      <?php
      if (has_post_thumbnail()) :
        $id = get_post_thumbnail_id();
        // var_dump($id);
        $img = wp_get_attachment_image_src($id, 'large');
      // var_dump($img);
      else :
        $img = array(get_template_directory_uri() . '/img/post-bg.jpg');
      endif;
      ?>
      <header class="masthead" style="background-image: url('<?php echo $img[0]; ?>')">
        <div class="overlay"></div>
        <div class="container">
          <div class="row">
            <div class="col-lg-8 col-md-10 mx-auto">
              <div class="post-heading">
                <h1><?php the_title(); ?></h1>
                <span class="meta">Posted by
                  <?php the_author(); ?>
                  on <?php the_date(); ?></span>
              </div>
            </div>
          </div>
        </div>
      </header>

      <!-- Post Content -->
      <article>
        <div class="container">
          <div class="row">
            <div class="col-lg-8 col-md-10 mx-auto">
              <?php the_post_thumbnail(array(32, 32), array('alt' => 'アイキャッチ画像')); ?>
              <?php the_content(); ?>
            </div>
          </div>
        </div>
      </article>

      <hr>
    <?php endwhile; ?>

    <!-- <?php else : ?>
    <p>記事が見つかりませんでした</p> -->
  <?php endif; ?>

  <!-- Footer -->
  <?php get_template_part('includes/footer'); ?>

  <?php get_footer(); ?>

</body>

</html>
```

## 30. 固定ページのテンプレートを作成しよう

+ [テンプレート階層](https://unofficialtokyo.com/wordpress-template-hierarchy/)<br>

+ WP管理画面の`固定ページ` => `固定ページ一覧`をクリック<br>

+ `タイトル`にチェックを入れて => `一括操作` => `ゴミ箱へ移動` => `適用`をクリック<br>

+ `新規追加`をクリック<br>

+ `タイトルを追加` => `about`と入力<br>

+ `文章を入力`の箇所に説明などを入力する<br>

+ `公開`をクリック<br>

+ 再度 `公開`をクリック<br>

+ `固定ページを表示`をクリックしてみる<br>

+ `myblog $ mv about.html page.php`を実行<br>

+ `myblog/page.php`を編集<br>

```php:page.php
<!DOCTYPE html>
<html <?php language_attributes(); ?>> // 編集

<head>
  <?php get_header(); ?> // 編集
</head>

<body <?php body_class(); ?>> // 編集

  <!-- Navigation -->
  <?php get_template_part('includes/header'); ?> // 編集

  <!-- Page Header -->
  <header class="masthead" style="background-image: url('img/about-bg.jpg')">
    <div class="overlay"></div>
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="page-heading">
            <h1>About Me</h1>
            <span class="subheading">This is what I do.</span>
          </div>
        </div>
      </div>
    </div>
  </header>

  <!-- Main Content -->
  <div class="container">
    <div class="row">
      <div class="col-lg-8 col-md-10 mx-auto">
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Saepe nostrum ullam eveniet pariatur voluptates odit, fuga atque ea nobis sit soluta odio, adipisci quas excepturi maxime quae totam ducimus consectetur?</p>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eius praesentium recusandae illo eaque architecto error, repellendus iusto reprehenderit, doloribus, minus sunt. Numquam at quae voluptatum in officia voluptas voluptatibus, minus!</p>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aut consequuntur magnam, excepturi aliquid ex itaque esse est vero natus quae optio aperiam soluta voluptatibus corporis atque iste neque sit tempora!</p>
      </div>
    </div>
  </div>

  <hr>

  <!-- Footer -->
  <?php get_template_part('includes/footer'); ?> // 編集

  <?php get_footer(); ?> // 編集

</body>

</html>
```

+ `myblog/page.php`を編集<br>

```php:page.php
<!DOCTYPE html>
<html <?php language_attributes(); ?>>

<head>
  <?php get_header(); ?>
</head>

<body <?php body_class(); ?>>

  <!-- Navigation -->
  <?php get_template_part('includes/header'); ?>

  <?php if (have_posts()) : ?> // 追加
    <?php while (have_posts()) : the_post(); ?> // 追加
      <!-- Page Header -->
      <header class="masthead" style="background-image: url('img/about-bg.jpg')">
        <div class="overlay"></div>
        <div class="container">
          <div class="row">
            <div class="col-lg-8 col-md-10 mx-auto">
              <div class="page-heading">
                <h1><?php the_title(); ?></h1> // 編集
              </div>
            </div>
          </div>
        </div>
      </header>

      <!-- Main Content -->
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <?php the_content(); ?> // 編集
          </div>
        </div>
      </div>

      <hr>
    <?php endwhile; ?> // 追加
  <?php endif; ?> // 追加

  <!-- Footer -->
  <?php get_template_part('includes/footer'); ?>

  <?php get_footer(); ?>

</body>

</html>
```

+ WP管理画面の固定ページのaboutページに内容を入れて更新してみる<br>

## 31. ファンクション（関数）を作ろう

+ `myblog/functions.php`を編集<br>

```php:functions.php
<?php
add_action('init', function () {
  add_theme_support(('post-thumbnails'));
});

// 追加
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

+ `myblog/single.php`を編集<br>

```php:single.php
<!DOCTYPE html>
<html <?php language_attributes(); ?>>

<head>
  <?php get_header(); ?>
</head>

<body <?php body_class(); ?>>

  <!-- Navigation -->
  <?php get_template_part('includes/header'); ?>

  <?php if (have_posts()) : ?>
    <?php while (have_posts()) : the_post(); ?>
      <!-- Page Header -->
      <?php
      $img = get_eyecatch_with_default(); // 編集
      ?>
      <header class="masthead" style="background-image: url('<?php echo $img[0]; ?>')">
        <div class="overlay"></div>
        <div class="container">
          <div class="row">
            <div class="col-lg-8 col-md-10 mx-auto">
              <div class="post-heading">
                <h1><?php the_title(); ?></h1>
                <span class="meta">Posted by
                  <?php the_author(); ?>
                  on <?php the_date(); ?></span>
              </div>
            </div>
          </div>
        </div>
      </header>

      <!-- Post Content -->
      <article>
        <div class="container">
          <div class="row">
            <div class="col-lg-8 col-md-10 mx-auto">
              <?php the_post_thumbnail(array(32, 32), array('alt' => 'アイキャッチ画像')); ?>
              <?php the_content(); ?>
            </div>
          </div>
        </div>
      </article>

      <hr>
    <?php endwhile; ?>

    <!-- <?php else : ?>
    <p>記事が見つかりませんでした</p> -->
  <?php endif; ?>

  <!-- Footer -->
  <?php get_template_part('includes/footer'); ?>

  <?php get_footer(); ?>

</body>

</html>
```

+ `myblog/page.php`を編集<br>

```php:page.php
<!DOCTYPE html>
<html <?php language_attributes(); ?>>

<head>
  <?php get_header(); ?>
</head>

<body <?php body_class(); ?>>

  <!-- Navigation -->
  <?php get_template_part('includes/header'); ?>

  <?php if (have_posts()) : ?>
    <?php while (have_posts()) : the_post(); ?>
      <!-- Page Header -->
      // 追加
      <?php
      $img = get_eyecatch_with_default();
      ?>
      // ここまで
      <header class="masthead" style="background-image: url('<?php echo $img[0]; ?>')">
        <div class="overlay"></div>
        <div class="container">
          <div class="row">
            <div class="col-lg-8 col-md-10 mx-auto">
              <div class="post-heading">
                <h1><?php the_title(); ?></h1>
                <span class="meta">Posted by
                  <?php the_author(); ?>
                  on <?php the_date(); ?></span>
              </div>
            </div>
          </div>
        </div>
      </header>

      <!-- Post Content -->
      <article>
        <div class="container">
          <div class="row">
            <div class="col-lg-8 col-md-10 mx-auto">
              <?php the_post_thumbnail(array(32, 32), array('alt' => 'アイキャッチ画像')); ?>
              <?php the_content(); ?>
            </div>
          </div>
        </div>
      </article>

      <hr>
    <?php endwhile; ?>

    <!-- <?php else : ?>
    <p>記事が見つかりませんでした</p> -->
  <?php endif; ?>

  <!-- Footer -->
  <?php get_template_part('includes/footer'); ?>

  <?php get_footer(); ?>

</body>

</html>
```
