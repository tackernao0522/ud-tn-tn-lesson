## 23. テンプレートファイルのパスを取得しよう - get_template_directory_uri()

+ [get_template_directory_uri()](https://wpdocs.osdn.jp/%E9%96%A2%E6%95%B0%E3%83%AA%E3%83%95%E3%82%A1%E3%83%AC%E3%83%B3%E3%82%B9/get_template_directory_uri)<br>

+ `myblog`ディレクトリに移動<br>

+ `wp-content/themes/myblog/header.php`を編集<br>

```php:header.php
<meta charset="utf-8">
// <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no"> // 削除
// <meta name="description" content=""> // 削除
<meta name="author" content="">

<title><?php the_title(); ?></title> // 編集

<!-- Bootstrap core CSS -->
<link href="<?php echo get_template_directory_uri(); ?>/vendor/bootstrap/css/bootstrap.min.css" rel="stylesheet"> // 編集

<!-- Custom fonts for this template -->
<link href="<?php echo get_template_directory_uri(); ?>/vendor/fontawesome-free/css/all.min.css" rel="stylesheet" type="text/css"> // 編集
<link href='//fonts.googleapis.com/css?family=Lora:400,700,400italic,700italic' rel='stylesheet' type='text/css'> // 編集
<link href='//fonts.googleapis.com/css?family=Open+Sans:300italic,400italic,600italic,700italic,800italic,400,300,600,700,800' rel='stylesheet' type='text/css'> // 編集

<!-- Custom styles for this template -->
<link href="<?php echo get_template_directory_uri(); ?>/css/clean-blog.css" rel="stylesheet"> // 編集

<?php wp_head(); ?>
```

+ `wp-content/themes/myblog/footer.php`を編集<br>

```php:footer.php
  <!-- Bootstrap core JavaScript -->
  <script src="<?php echo get_template_directory_uri(); ?>/vendor/jquery/jquery.min.js"></script> // 編集
  <script src="<?php echo get_template_directory_uri(); ?>/vendor/bootstrap/js/bootstrap.bundle.min.js"></script> // 編集

  <!-- Custom scripts for this template -->
  <script src="<?php echo get_template_directory_uri(); ?>/js/clean-blog.min.js"></script> // 編集

  <?php wp_footer(); ?>
```