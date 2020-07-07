# Chapter5

PHPとMySQLを使ったアプリケーションの連携の実装を行います。

## 困ったときに見るべきサイト

- [PHP入門](https://www.javadrive.jp/php/)
- [PHPマニュアル](https://www.php.net/manual/ja/index.php)

## データベースとは

[データベースについてのスライド](https://docs.google.com/presentation/d/1yP06dB2DNpq79V-D0jb1avFbeVXqKYhosDGgzUqTfr0/edit#slide=id.g89d8af4848_0_0)

### 課題1

データベースを使って掲示板アプリを書き換えてください。
なお、以前の投稿は消しても構いません。

ヒント：スキーマは以下のものを使ってもよいです。

```sql
CREATE TABLE IF NOT EXISTS `thread` (
`id` int(11) AUTO_INCREMENT,
`name` varchar(255) NOT NULL,
`content` varchar(255) NOT NULL,
`created_at` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
`deleted_at` DATETIME DEFAULT NULL,
PRIMARY KEY (`id`)
) DEFAULT CHARSET=utf8;
```

PDOの使い方

- [https://www.javadrive.jp/php/pdo/](https://www.javadrive.jp/php/pdo/)
- [https://www.php.net/manual/ja/class.pdo.php](https://www.php.net/manual/ja/class.pdo.php)

課題1が終わったら、[composer](https://getcomposer.org/)をダウンロードして、 `composer.json` を入れ替える。

```json:composer.json
{
    "name": "career2-php/career2-php-sample1",
    "require": {
        "davedevelopment/phpmig": "^1.6",
        "vlucas/phpdotenv": "^5.0",
        "pimple/pimple": "^3.0"
    },
    "require-dev": {
        "squizlabs/php_codesniffer": "^3.5"
    },
    "scripts": {
        "sniffer": [
            "./vendor/bin/phpcs --standard=phpcs.xml ./"
        ],
        "sniffer-rewrite": [
            "./vendor/bin/phpcbf --standard=phpcs.xml ./"
        ]
    }
}
```

`composer.json` を更新したら `composer install` を実行してください。(動画参照)

### 課題2

データベースを使って、複数の掲示板を立てられるようにしてください。
スレッドと掲示板のタイトルが、掲示板毎に変わっていればOKです。

ヒント：今のthreadは複数の掲示板の投稿を管理できるようになっていないので、掲示板全体を管理するテーブルを作り、掲示板と投稿を紐付けるカラムをthreadに追加してください。