## 25. 投稿の詳細ページに各情報を出力しよう

+ `myblog`ディレクトリにて作業<br>

+ `myblog/single.php`を編集<br>

```php:single.php
<!DOCTYPE html>
<html lang="en">

<head>
  <?php get_header(); ?>
</head>

<body>

  <!-- Navigation -->
  <?php get_template_part('includes/header'); ?>

  <?php while (have_posts()) : the_post(); ?> // 追加
    <!-- Page Header -->
    <header class="masthead" style="background-image: url('img/post-bg.jpg')">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="post-heading">
              <h1><?php the_title(); ?></h1> // 編集
              // <h2 class="subheading">Problems look mighty small from 150 miles up</h2> 削除する
              <span class="meta">Posted by
                <?php the_author(); ?> // 編集
                on <?php the_date(); ?></span> // 編集
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
            <p>Never in all their history have men been able truly to conceive of the world as one: a single sphere, a globe, having the qualities of a globe, a round earth in which all the directions eventually meet, in which there is no center because every point, or none, is center — an equal earth which all men occupy as equals. The airman's earth, if free men make it, will be truly round: a globe in practice, not in theory.</p>

            <p>Science cuts two ways, of course; its products can be used for both good and evil. But there's no turning back from science. The early warnings about technological dangers also come from science.</p>

            <p>What was most significant about the lunar voyage was not that man set foot on the Moon but that they set eye on the earth.</p>

            <p>A Chinese tale tells of some men sent to harm a young girl who, upon seeing her beauty, become her protectors rather than her violators. That's how I felt seeing the Earth for the first time. I could not help but love and cherish her.</p>

            <p>For those who have seen the Earth from space, and for the hundreds and perhaps thousands more who will, the experience most certainly changes your perspective. The things that we share in our world are far more valuable than those which divide us.</p>

            <h2 class="section-heading">The Final Frontier</h2>

            <p>There can be no thought of finishing for ‘aiming for the stars.’ Both figuratively and literally, it is a task to occupy the generations. And no matter how much progress one makes, there is always the thrill of just beginning.</p>

            <p>There can be no thought of finishing for ‘aiming for the stars.’ Both figuratively and literally, it is a task to occupy the generations. And no matter how much progress one makes, there is always the thrill of just beginning.</p>

            <blockquote class="blockquote">The dreams of yesterday are the hopes of today and the reality of tomorrow. Science has not yet mastered prophecy. We predict too much for the next year and yet far too little for the next ten.</blockquote>

            <p>Spaceflights cannot be stopped. This is not the work of any one man or even a group of men. It is a historical process which mankind is carrying out in accordance with the natural laws of human development.</p>

            <h2 class="section-heading">Reaching for the Stars</h2>

            <p>As we got further and further away, it [the Earth] diminished in size. Finally it shrank to the size of a marble, the most beautiful you can imagine. That beautiful, warm, living object looked so fragile, so delicate, that if you touched it with a finger it would crumble and fall apart. Seeing this has to change a man.</p>

            <a href="#">
              <img class="img-fluid" src="img/post-sample-image.jpg" alt="">
            </a>
            <span class="caption text-muted">To go places and do things that have never been done before – that’s what living is all about.</span>

            <p>Space, the final frontier. These are the voyages of the Starship Enterprise. Its five-year mission: to explore strange new worlds, to seek out new life and new civilizations, to boldly go where no man has gone before.</p>

            <p>As I stand out here in the wonders of the unknown at Hadley, I sort of realize there’s a fundamental truth to our nature, Man must explore, and this is exploration at its greatest.</p>

            <p>Placeholder text by
              <a href="http://spaceipsum.com/">Space Ipsum</a>. Photographs by
              <a href="https://www.flickr.com/photos/nasacommons/">NASA on The Commons</a>.
            </p>
          </div>
        </div>
      </div>
    </article>

    <hr>
  <?php endwhile; ?> // 追加

  <!-- Footer -->
  <?php get_template_part('includes/footer'); ?>

  <?php get_footer(); ?>

</body>

</html>
```

+ `myblog/single.php`を編集<br>

```php:single.php
<!DOCTYPE html>
<html lang="en">

<head>
  <?php get_header(); ?>
</head>

<body>

  <!-- Navigation -->
  <?php get_template_part('includes/header'); ?>

  <?php if (have_posts()): ?> // 追加
  <?php while (have_posts()) : the_post(); ?>
    <!-- Page Header -->
    <header class="masthead" style="background-image: url('img/post-bg.jpg')">
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
            <?php the_content(); ?> // 編集
          </div>
        </div>
      </div>
    </article>

    <hr>
  <?php endwhile; ?>

  <!-- <?php else: ?>
    <p>記事が見つかりませんでした</p> なくても良い-->
  <?php endif; ?>


  <!-- Footer -->
  <?php get_template_part('includes/footer'); ?>

  <?php get_footer(); ?>

</body>

</html>
```

## 26. アイキャッチ画像を挿入しよう① - the_post_thumbnail

+ [the_post_thumbnail](https://wpdocs.osdn.jp/%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%82%BF%E3%82%B0/the_post_thumbnail)<br>

+ `touch myblog/functions.php`を実行<br>

+ `wp-content/themes/myblog/functions.php`を編集<br>

```php:functions.php
<?php
add_action('init', function () {
  add_theme_support(('post-thumbnails'));
});
```

+ WP管理画面の`投稿` => `抜粋の練習です`をクリック => 右の`投稿`メニューの中に`アイキャッチ画像の設定枠`ができている<br>

+ `アイキャッチ画像を設定`をクリックして適当な画像をアップロードする<br>

+ `アイキャッチ画像を設定`をクリック<br>

+ `更新`ボタンをクリック(これではまだ反映されない)<br>

+ `myblog/single.php`を編集<br>

```php:single.php
<!DOCTYPE html>
<html lang="en">

<head>
  <?php get_header(); ?>
</head>

<body>

  <!-- Navigation -->
  <?php get_template_part('includes/header'); ?>

  <?php if (have_posts()): ?>
  <?php while (have_posts()) : the_post(); ?>
    <!-- Page Header -->
    <header class="masthead" style="background-image: url('img/post-bg.jpg')">
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
            <?php the_post_thumbnail(array(32, 32), array('alt' => 'アイキャッチ画像')); ?> // アイキャッチ画像が表示される 引数はオプション
            <?php the_content(); ?>
          </div>
        </div>
      </div>
    </article>

    <hr>
  <?php endwhile; ?>

  <!-- <?php else: ?>
    <p>記事が見つかりませんでした</p> -->
  <?php endif; ?>

  <!-- Footer -->
  <?php get_template_part('includes/footer'); ?>

  <?php get_footer(); ?>

</body>

</html>
```

+ WP管理画面の`メディア` => `ライブラリ`をクリック<br>

+ 表示したい画像をクリックして そのURLは http://mysite.local/wp-admin/upload.php?item=21 であり id は `21`になっている<br>

+ `myblog/single.php`を編集<br>

```php:single.php
<!DOCTYPE html>
<html lang="en">

<head>
  <?php get_header(); ?>
</head>

<body>

  <!-- Navigation -->
  <?php get_template_part('includes/header'); ?>

  <?php if (have_posts()) : ?>
    <?php while (have_posts()) : the_post(); ?>
      <!-- Page Header -->
      <?php
      $img = wp_get_attachment_image_src(21); // 追加
      ?>
      <header class="masthead" style="background-image: url('<?php echo $img[0]; ?>')"> // 編集
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

これでheaderの画像が表示される<br>

+ `myblog/single.php`を編集<br>

```php:single.php
<!DOCTYPE html>
<html lang="en">

<head>
  <?php get_header(); ?>
</head>

<body>

  <!-- Navigation -->
  <?php get_template_part('includes/header'); ?>

  <?php if (have_posts()) : ?>
    <?php while (have_posts()) : the_post(); ?>
      <!-- Page Header -->
      <?php
      $id = get_post_thumbnail_id(); // 追加
      $img = wp_get_attachment_image_src($id); // 動的にする
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

## 27. アイキャッチ画像を挿入しよう② - wp_get_attachment_image_src

+ [wp_get_attachment_image_src](https://wpdocs.osdn.jp/%E9%96%A2%E6%95%B0%E3%83%AA%E3%83%95%E3%82%A1%E3%83%AC%E3%83%B3%E3%82%B9/wp_get_attachment_image_src)<br>

+ `myblog`ディレクトリに移動<br>

※ `wp_get_attachment_image_src()`はメディアライブラリから取り出す関数である<br>

+ `myblog/single.php`を編集<br>

```php:single.php
<!DOCTYPE html>
<html lang="en">

<head>
  <?php get_header(); ?>
</head>

<body>

  <!-- Navigation -->
  <?php get_template_part('includes/header'); ?>

  <?php if (have_posts()) : ?>
    <?php while (have_posts()) : the_post(); ?>
      <!-- Page Header -->
      <?php
      $id = get_post_thumbnail_id();
      var_dump($id); // 24
      $img = wp_get_attachment_image_src($id);
      var_dump($img);
      // 0 => string 'http://mysite.local/wp-content/uploads/2022/08/audience--150x150.jpg' (length=68)
      // 1 => int 150
      // 2 => int 150
      // 3 => boolean true
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

+ WP管理画面の`設定` => `メディア`をクリックしたところが画像のサイズ設定になる(デフォルトは`thumbnai`サイズになっている)<br>

+ `myblog/single.php`を編集<br>

```php:single.php
<!DOCTYPE html>
<html lang="en">

<head>
  <?php get_header(); ?>
</head>

<body>

  <!-- Navigation -->
  <?php get_template_part('includes/header'); ?>

  <?php if (have_posts()) : ?>
    <?php while (have_posts()) : the_post(); ?>
      <!-- Page Header -->
      <?php
      $id = get_post_thumbnail_id();
      // var_dump($id);
      $img = wp_get_attachment_image_src($id, 'large'); // 編集
      // var_dump($img);
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

+ `large`を1024から2048くらいにしても良い<br>

+ `myblog/single.php`を編集<br>

```php:single.php
<!DOCTYPE html>
<html lang="en">

<head>
  <?php get_header(); ?>
</head>

<body>

  <!-- Navigation -->
  <?php get_template_part('includes/header'); ?>

  <?php if (have_posts()) : ?>
    <?php while (have_posts()) : the_post(); ?>
      <!-- Page Header -->
      <?php
      if (has_post_thumbnail()) : // 追加
        $id = get_post_thumbnail_id();
        // var_dump($id);
        $img = wp_get_attachment_image_src($id, 'large');
      // var_dump($img);
      else : // 追加(アイキャッチ画像を指定していない場合)
        $img = array(get_template_directory_uri() . '/img/post-bg.jpg'); // 追加
      endif; // 追加
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
