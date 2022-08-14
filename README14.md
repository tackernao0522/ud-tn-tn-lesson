## 36. カテゴリーページを作成しよう

+ WP管理画面 => `投稿` => `カテゴリー` => `ブログ` => `表示` をクリックするとカテゴリーのページにアクセスできる (http://mysite.local/category/blog/)<br>

+ `設定` => `パーマリンク設定` => `カテゴリーベース` => `topics`と入力して => `変更を保存`をクリックして`blog`カテゴリーにアクセスしてみると http://mysite.local/topics/blog/ に変更されている<br>

+ `topics`を元に戻しておく<br>

+ `メモ`という新規カテゴリーを作成する<br>

+ 新規投稿で タイトル `「メモ」の記事`を入力して `カテゴリー` => `メモ`にチェックして公開する<br>

+ `メモ`カテゴリーを表示してみる (http://mysite.local/category/memo/) カテゴリーアーカイブというページで表示されている<br>

+ `$ cp myblog/index.php myblog/archive.php`を実行<br>

+ `myblog/archive.php`を編集<br>

```php:archive.php
<!DOCTYPE html>
<html lang="en">

<head>

  <?php get_header(); ?>

</head>

<body>

  <!-- Navigation -->
  <?php get_template_part('includes/header'); ?>

  <!-- Page Header -->
  <header class="masthead" style="background-image: url('img/home-bg.jpg')">
    <div class="overlay"></div>
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="site-heading">
            <h1>Category</h1> // 編集
            <span class="subheading"><?php wp_title(''); ?></span> // 編集 カテゴリー名の表示 ('')がないと '>>'が入ってしまう
          </div>
        </div>
      </div>
    </div>
  </header>

  <!-- Main Content -->
  <div class="container">
    <div class="row">
      <div class="col-lg-8 col-md-10 mx-auto">
        <?php if (have_posts()) : ?>
          <?php while (have_posts()) : the_post(); ?>
            <div class="post-preview">
              <a href="<?php the_permalink(); ?>">
                <h2 class="post-title">
                  <?php the_title(); ?>
                </h2>
                <h3 class="post-subtitle">
                  <?php the_excerpt(); ?>
                </h3>
              </a>
              <p class="post-meta">Posted by
                <?php the_author(); ?>
                on <?php the_time(get_option('date_format')); ?>
              </p>
            </div>
            <hr>
          <?php endwhile; ?>
          <!-- Pager -->
          <div class="clearfix">
            <a class="btn btn-primary float-right" href="#">Older Posts &rarr;</a>
          </div>
        <?php else : ?>
          <p>記事が見つかりませんでした</p>
        <?php endif; ?>
      </div>
    </div>
  </div>

  <hr>

  <!-- Footer -->
  <?php get_template_part('includes/footer'); ?>

  <?php get_footer(); ?>
</body>

</html>
```

+ [wp_title](https://wpdocs.osdn.jp/%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%82%BF%E3%82%B0/wp_title)<br>
