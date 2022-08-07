# WP管理画面設定

+ `settings->General`をクリック<br>

+ `Site Language` => `日本語`を選択<br>

+ `Timezone` => `UTC+9`を選択<br>

+ `Save Changes`をクリックして日本語になる<br>

+ `プラグイン` => `新規追加`をクリック<br>

+ `プラグインの検索`枠で `multibyte`と入力<br>

+ `WP Multibyte Patch`を`今すぐインストール`する<br>

+ `有効化`をクリック<br>

+ 左上の`MySite`をクリックするとサイトを表示できる 再度`MySite`の部分をクリックすると管理画面に戻れる<br>

# セクション3: WordPressのテーマを知ろう

## 5. テーマの確認と変更をしてみよう

+ WP管理画面の`外観` => `テーマ`をクリックしてテーマを選択して`有効化`して変更する<br>

+ Localの`MySite`の部分を右クリックして`Go to site folder`をクリックすると theme folderを開ける<br>

+ `mysite/app/public/wp-content/themes/`にthemesのファイルがある<br>

+ `app/public/wp-content/themes/twentytwenty/index.php`を編集<br>

```php:index.php
<?php
/**
 * The main template file
 *
 * This is the most generic template file in a WordPress theme
 * and one of the two required files for a theme (the other being style.css).
 * It is used to display a page when nothing more specific matches a query.
 * E.g., it puts together the home page when no home.php file exists.
 *
 * @link https://developer.wordpress.org/themes/basics/template-hierarchy/
 *
 * @package WordPress
 * @subpackage Twenty_Twenty
 * @since Twenty Twenty 1.0
 */

get_header();
?>

<main id="site-content">

  // 追加
  <p>テーマを変更しました</p>

	<?php

	$archive_title    = '';
	$archive_subtitle = '';

	if ( is_search() ) {
		global $wp_query;

		$archive_title = sprintf(
			'%1$s %2$s',
			'<span class="color-accent">' . __( 'Search:', 'twentytwenty' ) . '</span>',
			'&ldquo;' . get_search_query() . '&rdquo;'
		);

		if ( $wp_query->found_posts ) {
			$archive_subtitle = sprintf(
				/* translators: %s: Number of search results. */
				_n(
					'We found %s result for your search.',
					'We found %s results for your search.',
					$wp_query->found_posts,
					'twentytwenty'
				),
				number_format_i18n( $wp_query->found_posts )
			);
		} else {
			$archive_subtitle = __( 'We could not find any results for your search. You can give it another try through the search form below.', 'twentytwenty' );
		}
	} elseif ( is_archive() && ! have_posts() ) {
		$archive_title = __( 'Nothing Found', 'twentytwenty' );
	} elseif ( ! is_home() ) {
		$archive_title    = get_the_archive_title();
		$archive_subtitle = get_the_archive_description();
	}

	if ( $archive_title || $archive_subtitle ) {
		?>

		<header class="archive-header has-text-align-center header-footer-group">

			<div class="archive-header-inner section-inner medium">

				<?php if ( $archive_title ) { ?>
					<h1 class="archive-title"><?php echo wp_kses_post( $archive_title ); ?></h1>
				<?php } ?>

				<?php if ( $archive_subtitle ) { ?>
					<div class="archive-subtitle section-inner thin max-percentage intro-text"><?php echo wp_kses_post( wpautop( $archive_subtitle ) ); ?></div>
				<?php } ?>

			</div><!-- .archive-header-inner -->

		</header><!-- .archive-header -->

		<?php
	}

	if ( have_posts() ) {

		$i = 0;

		while ( have_posts() ) {
			$i++;
			if ( $i > 1 ) {
				echo '<hr class="post-separator styled-separator is-style-wide section-inner" aria-hidden="true" />';
			}
			the_post();

			get_template_part( 'template-parts/content', get_post_type() );

		}
	} elseif ( is_search() ) {
		?>

		<div class="no-search-results-form section-inner thin">

			<?php
			get_search_form(
				array(
					'aria_label' => __( 'search again', 'twentytwenty' ),
				)
			);
			?>

		</div><!-- .no-search-results -->

		<?php
	}
	?>

	<?php get_template_part( 'template-parts/pagination' ); ?>

</main><!-- #site-content -->

<?php get_template_part( 'template-parts/footer-menus-widgets' ); ?>

<?php
get_footer();
```

## 6. テンプレート階層を知ろう

+ `app/public/wp-content/themes/twentytwenty/index.php`を編集<br>

```php:index.php
<?php
/**
 * The main template file
 *
 * This is the most generic template file in a WordPress theme
 * and one of the two required files for a theme (the other being style.css).
 * It is used to display a page when nothing more specific matches a query.
 * E.g., it puts together the home page when no home.php file exists.
 *
 * @link https://developer.wordpress.org/themes/basics/template-hierarchy/
 *
 * @package WordPress
 * @subpackage Twenty_Twenty
 * @since Twenty Twenty 1.0
 */

get_header();
?>

<main id="site-content">
  // 編集
  <p>index.phpです</p>

	<?php

	$archive_title    = '';
	$archive_subtitle = '';

	if ( is_search() ) {
		global $wp_query;

		$archive_title = sprintf(
			'%1$s %2$s',
			'<span class="color-accent">' . __( 'Search:', 'twentytwenty' ) . '</span>',
			'&ldquo;' . get_search_query() . '&rdquo;'
		);

		if ( $wp_query->found_posts ) {
			$archive_subtitle = sprintf(
				/* translators: %s: Number of search results. */
				_n(
					'We found %s result for your search.',
					'We found %s results for your search.',
					$wp_query->found_posts,
					'twentytwenty'
				),
				number_format_i18n( $wp_query->found_posts )
			);
		} else {
			$archive_subtitle = __( 'We could not find any results for your search. You can give it another try through the search form below.', 'twentytwenty' );
		}
	} elseif ( is_archive() && ! have_posts() ) {
		$archive_title = __( 'Nothing Found', 'twentytwenty' );
	} elseif ( ! is_home() ) {
		$archive_title    = get_the_archive_title();
		$archive_subtitle = get_the_archive_description();
	}

	if ( $archive_title || $archive_subtitle ) {
		?>

		<header class="archive-header has-text-align-center header-footer-group">

			<div class="archive-header-inner section-inner medium">

				<?php if ( $archive_title ) { ?>
					<h1 class="archive-title"><?php echo wp_kses_post( $archive_title ); ?></h1>
				<?php } ?>

				<?php if ( $archive_subtitle ) { ?>
					<div class="archive-subtitle section-inner thin max-percentage intro-text"><?php echo wp_kses_post( wpautop( $archive_subtitle ) ); ?></div>
				<?php } ?>

			</div><!-- .archive-header-inner -->

		</header><!-- .archive-header -->

		<?php
	}

	if ( have_posts() ) {

		$i = 0;

		while ( have_posts() ) {
			$i++;
			if ( $i > 1 ) {
				echo '<hr class="post-separator styled-separator is-style-wide section-inner" aria-hidden="true" />';
			}
			the_post();

			get_template_part( 'template-parts/content', get_post_type() );

		}
	} elseif ( is_search() ) {
		?>

		<div class="no-search-results-form section-inner thin">

			<?php
			get_search_form(
				array(
					'aria_label' => __( 'search again', 'twentytwenty' ),
				)
			);
			?>

		</div><!-- .no-search-results -->

		<?php
	}
	?>

	<?php get_template_part( 'template-parts/pagination' ); ?>

</main><!-- #site-content -->

<?php get_template_part( 'template-parts/footer-menus-widgets' ); ?>

<?php
get_footer();
```

+ `app/public/wp-content/themes/twentytwenty/singular.php`を編集<br>

```php:singular.php
<?php
/**
 * The template for displaying single posts and pages.
 *
 * @link https://developer.wordpress.org/themes/basics/template-hierarchy/
 *
 * @package WordPress
 * @subpackage Twenty_Twenty
 * @since Twenty Twenty 1.0
 */

get_header();
?>

<main id="site-content">
  // 追加
	<p>singular.php</p>
	<?php

	if ( have_posts() ) {

		while ( have_posts() ) {
			the_post();

			get_template_part( 'template-parts/content', get_post_type() );
		}
	}

	?>

</main><!-- #site-content -->

<?php get_template_part( 'template-parts/footer-menus-widgets' ); ?>

<?php get_footer(); ?>
```

+ [テンプレート階層画像](https://developer.wordpress.org/files/2014/10/Screenshot-2019-01-23-00.20.04.png) <br>

+ [テンプレート階層DOC](http://wpdocs.osdn.jp/%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E9%9A%8E%E5%B1%A4)<br>

+ `app/public/wp-content/themes/twentytwenty/singular.php`を削除してみる<br>

+ Topページ = 表示される<br>

+ アーカイブページ = 表示される

+ Recent Postの `Hello world`にアクセスすると `singular.php`ではなく、`index.php`にアクセスされる(アーカイブ)<br>

※ `index.php`さえあれば、テーマとして機能することになる<br>


+ `singular.php`を戻す<br>

※ テンプレート階層は左側にあるボックスほど優先度が高い<br>

+ `app/public/wp-content/themes/twentytwenty/single.php`を作成<br>

+ `single.php`を編集<br>

```php:single.php
single.php
```

+ Recent Postの `Hello world`にアクセスすると`single.php`にアクセスされる<br>

+ `app/public/wp-content/themes/twentytwenty/single-post.php`を作成<br>

+ `single-post.php`を編集<br>

```php:single-post.php
single-post.php
```

+ Recent Postの `Hello world`にアクセスすると`single-post.php`にアクセスされる<br>

## 7. Query Monitorでテンプレートを確認しよう

+ WP 管理画面にアクセス<br>

+ メニューの `プラグイン`をクリック<br>

+ `新規追加`ボタンをクリック<br>

+ `プラグインの検索`の中に`query monitor`と入力する<br>

+ `Query Monitor` を `今すぐインストール`する<br>

+ `有効化`をクリック<br>

+ `app/public/wp-cintent/themes/twentytwenty/single-post.php`を削除<br>

+ `app/public/wp-cintent/themes/twentytwenty/single.php`を削除<br>

+ これで http://mysite.local/hello-world/ にアクセスして Query Monitorを確認すると`singular.php`を指している<br>

+ `app/public/wp-cintent/themes/twentytwenty/single.php`を作成して`singular.php`の中身をコピーする<br>

+ これで http://mysite.local/hello-world/ にアクセスして Query Monitorを確認すると`single.php`を指している<br>

+ `app/public/wp-cintent/themes/twentytwenty/single.php`を削除<br>

+ `app/public/wp-cintent/themes/twentytwenty/singular.php`を削除<br>

+ これで http://mysite.local/hello-world/ にアクセスして Query Monitorを確認すると`index.php`を指している<br>

## 8. 最小構成のテーマを作成してみよう

+ WP管理画面の `外観` => `テーマ`をクリック<br>

+ `wp-content/themes/mytheme`ディレクトリを作成<br>

+ 管理画面の`テーマ`画面をリロードすると`mytheme`を認識しようとしているがエラーが出ている<br>

+ `app/public/wp-content/themes/mytheme/style.css`を作成<br>

+ 管理画面の`テーマ`画面をリロードするとエラー内容が変わる<br>

+ `app/public/wp-content/themes/mytheme/index.php`を作成<br>

+ 管理画面の`テーマ`画面をリロードするとエラーが出なくなる(index.php と style.cssは必須ファイルである)<br>

+ `有効化`すると画面は真っ白だがアクセスできるようになる<br>

+ `app/public/wp-content/themes/mytheme/index.php`を編集<br>

```php:index.php
新しいテーマです
```

+ アクセスすると反映している<br>

+ `app/public/wp-content/themes/mytheme/style.css`を編集<br>

```css:style.css
/*
Theme Name: Taka's テーマ
*/
```

+ 管理画面の`テーマ`画面をリロードするとテーマ名が変わる<br>

+ `テーマの詳細`をクリックしてもテーマ名が変わっているのがわかる<br>

+ `app/public/wp-content/themes/mytheme/style.css`を編集<br>

```css:style.css
/*
Theme Name: Taka's テーマ
Version: 1.0
*/
```

+ `テーマの詳細`をクリックするとVersionも反映されているのがわかる<br>

+ `app/public/wp-content/themes/mytheme/style.css`を編集<br>

```css:style.css
/*
Theme Name: Taka's テーマ
Version: 1.0
Author: たかき
*/
```

+ `テーマの詳細`をクリックするとAuthorも反映されているのがわかる<br>

+ `app/public/wp-content/themes/mytheme/style.css`を編集<br>

```css:style.css
/*
Theme Name: Taka's テーマ
Version: 1.0
Author: たかき
Description: このテーマは、たかきの専用テーマです
*/
```

+ `テーマの詳細`をクリックするとDescriptionも反映されているのがわかる<br>

+ [テーマの作成](https://wpdocs.osdn.jp/%E3%83%86%E3%83%BC%E3%83%9E%E3%81%AE%E4%BD%9C%E6%88%90#.E3.83.86.E3.83.BC.E3.83.9E.E3.82.B9.E3.82.BF.E3.82.A4.E3.83.AB.E3.82.B7.E3.83.BC.E3.83.88) <br>

+ `app/public/wp-content/themes/mytheme/index.php`を編集<br>

```php:index.php
<?php the_title(); ?>
```

+ アクセスすると画面に`Hello world!`と表示される<br>

+ WP管理画面の `投稿` => `新規追加`をクリック<br>

+ `x`をクリックして、`タイトルを追加`に `新しい投稿です`と入力して `公開`ボタンをクリックしてさらに `公開`ボタンをクリック<br>

+ WP管理画面の`投稿一覧`に戻ってlocalブラウザにアクセスするとタイトルが変わっている<br>
