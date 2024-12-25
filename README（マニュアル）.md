# セットアップ手順

## .envの設定

以下をコピーして`.env`ファイルに貼り付けてください。

```env
APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=

BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1

VITE_APP_NAME="${APP_NAME}"
VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
VITE_PUSHER_HOST="${PUSHER_HOST}"
VITE_PUSHER_PORT="${PUSHER_PORT}"
VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"
VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"
```

次に、以下の内容に変更してください。

```env
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=blog-app
DB_USERNAME=laravel
DB_PASSWORD=password
```

## Mailtrapの設定

1. [Mailtrap](https://mailtrap.io/)に登録します。
2. ログイン後、左側のナビゲーションから「Email Testing」をクリックします。
3. 右側の「Add Inbox」をクリックします。
4. 名前を入力（任意）して「Save」を押します。

.envファイルを以下の内容に変更します。

```env
MAIL_MAILER=smtp
MAIL_HOST=sandbox.smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=あなたのMailtrapのユーザー名
MAIL_PASSWORD=あなたのMailtrapのパスワード
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS="自分のメールアドレス"
MAIL_FROM_NAME="${APP_NAME}"
```

Mailtrapで表示される`MAIL_USERNAME`と`MAIL_PASSWORD`をコピーして貼り付けてください。

## Dockerのセットアップ

1. Dockerを開き、VSCodeのターミナルを開きます。
2. 以下のコマンドを順に実行します。

```bash
docker-compose up --build -d
```

エラーが発生しない場合は手順３に進んでください。発生した場合は以下を実行してください。

```bash
docker run --rm -v $(pwd):/var/www/html -w /var/www/html composer install
#↑これをやるとappが起動できる
docker-compose down
docker-compose up --build -d
docker exec -it blog-app bash
```

3. 次に以下のコマンドを実行します。

```bash
docker exec -it blog-app bash
composer install
php artisan key:generate
php artisan migrate
exit
```

4. `localhost:8000`にアクセスします。

もし以下のエラーが表示された場合：

```
Vite manifest not found at: /var/www/html/public/build/manifest.json
```

以下を実行してください。

```bash
npm install
npm run build
```

## 機能確認

1. サイトの「会員登録」を押します。
2. ユーザー名、メールアドレス、パスワードを入力して「登録」を押します。
3. Mailtrapの「Email Testing」を開き、自分が設定したInboxをクリックします。
4. メールが届いていることを確認し、認証リンクをクリックします。
5. ログインして動作を確認します。

## 投稿機能の確認

1. 「新規登録」を押します。
2. タイトルと本文を入力して「投稿」を押します。
3. 投稿一覧に表示されることを確認します。
4. 「詳細」を押して投稿の詳細を確認します。
5. 「編集」を押してタイトルや本文を編集し、「更新」を押します。
6. 「削除」を押すとモーダルウィンドウが表示されます。「OK」を押すと削除され、「キャンセル」を押すと削除されません。
