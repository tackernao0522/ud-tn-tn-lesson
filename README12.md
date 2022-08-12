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
