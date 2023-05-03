---
title: phpのroutingライブラリAltorouterの紹介
publishDate: 2021-07-23:12:03.284Z
description: "phpのroutingライブラリAltorouterの紹介"
---
# phpのroutingライブラリAltorouterの紹介
## モチベーション
webアプリケーションのよくあるパターンは、`index.php`で処理を受けたらURIに応じてルーティングしてリクエストされた処理を実行するというものですが、フレームワークを使っていないアプリケーションの場合、URIがそのまま、実行されるスクリプトのファイル名になっているケースがあります(hoge.com/login.phpみたいな感じ)。こういったアプリケーションの保守をしやすくするためにルーティングを入れたかったので`AltoRouter`というライブラリを(超基本的な使い方だけですが)検証してみました。

## Altorouterとは
klein.phpに影響を受けたルーティングライブラリだそうです。

[公式ドキュメント](http://altorouter.com/)

[類似ライブラリとの比較](https://php.libhunt.com/compare-fastroute-vs-altorouter)

## サンプルリポジトリ
https://github.com/isanasan/test_altorouter

## 導入
composerで普通に入れる

>composer require altorouter/altorouter

## 実装例
単純な例で検証してみます。

```bash
.
├── composer.json
├── composer.lock
├── api
│   └── user.php // 単純なスクリプトを置いてみる
├── public
│   └── index.php // ここにルーティング定義を書く
└── src
    └── Http
        └── Handler
            └── Welcome.php //controllerぽい感じでクラスを置いてみる
```

`index.php`の例
```php
<?php

declare(strict_types=1);

require_once __DIR__ . '/../vendor/autoload.php';

$router = new AltoRouter();

// スクリプトを直で呼び出す
$router->map('GET|POST|PATCH|DELETE', '/user', function () {
    require_once __DIR__ . '/../api/user.php';
});

// laravelっぽくクラスとメソッドを指定する
$router->map('GET', '/', 'isanasan\Router\Http\Handler\Welcome::get', 'welcome');

$match = $router->match();

if ($match !== false) {
    if (is_callable($match['target'])) {
        $match['target']();
    } else {
        $params = explode("::", $match['target']);
        $action = new $params[0]();
        call_user_func_array(array($action, $params[1]), $match['params']);
    }
} else {
    header($_SERVER["SERVER_PROTOCOL"] . ' 404 Not Found');
}

```

`src/Http/Handler`の中身
```php
<?php

namespace isanasan\Router\Http\Handler;

class Welcome
{
    public function get()
    {
        echo 'welcome';
    }
}
```

`api/user.php`の中身
```php
<?php

switch ($_SERVER['REQUEST_METHOD']) {
    case 'GET':
        $response = 'isana';
        echo $response;
        break;
    case 'POST':
    case 'PATCH':
    case 'DELETE':
}
```

以下のコマンドでビルトインサーバを実行します。

`php -S 127.0.0.1:3939 public/index.php -t public`

`http://127.0.0.1:3939/`へアクセス
![image](https://user-images.githubusercontent.com/58712884/126725951-31dac42b-a3fe-4dd2-bb58-c6b9306979a8.png)

`http://127.0.0.1:3939/user`へアクセス
![image](https://user-images.githubusercontent.com/58712884/126726042-a2b62500-5057-4324-917c-75e39a3eaa6d.png)

このようにアクセスしたURIに応じて処理をルーティングできました。今回は非常に簡単な例しか試していませんが、`router->map()`の第二引数を`/users/[i:id]/`のような形にすることでより実用的なルーティングが設定できます。

既存プロジェクトに入れて使う場合は、既に動いているページを`require`で読み込むことで対応し、これから新しく追加していく機能はコントローラっぽい使い方でルーティングすると良いのではないでしょうか。

## ハマりポイント
laravelっぽくルーティングする際に`is_callable($match['target'])`で判定しようとしても`$router->map()`の第三引数はただの文字列にしか過ぎないので`call_user_func()`で呼べませんでした。

## 余談
検証はビルトインサーバーを使いましたがmod_phpなら`.htaccess`を置きます。

`.htaccess`の例
```apacheconf
<IfModule mod_rewrite.c>
    # negotiation拡張を無効化
    <IfModule mod_negotiation.c>
            Options -MultiViews -Indexes
    </IfModule>
    # phpファイルへの直接アクセスを禁じる
    <Files ~ "(\.php)$">
        deny from all
    </Files>
    # index.phpへのアクセスを許可
    <Files ~ "^(index\.php)">
        allow from all
    </Files>

    # public/index.phpへリライト
    RewriteEngine on
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule . public/index.php [L]
</IfModule>

```

## 参考
https://www.youtube.com/watch?v=tbYa0rJQyoM

