.envを作成して以下をコピーして.envの中に貼り付ける

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

ーーーーーーーーーー

.env

DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=blog-app
DB_USERNAME=laravel

に変更する

ーーーーーーーーーー

https://mailtrap.io/ に登録する
ログインしたら左のナビゲーションの「Email Testing」を押す
右側にある「Add Inbox」を押す
「In box」の中に名前を入れる（何でも大丈夫です）
名前を入れたら「Save」を押す

.env

MAIL_MAILER=smtp
MAIL_HOST=sandbox.smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=
MAIL_PASSWORD=
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=“自分のメールアドレス”
MAIL_FROM_NAME="${APP_NAME}"

MAIL_USERNAMEとMAIL_PASSWORDをそれぞれ mailtrapからコピーして貼り付ける

ーーーーーーーーーー

Dockerを開く
VScodeでターミナルを開く
１docker-compose up --build -d：をうつ
２docker exec -it blog-app bash：をうつ
エラーになったらならなかったら7に飛ぶ
３docker run --rm -v $(pwd):/var/www/html -w /var/www/html composer install：をうつ（これをやるとappが起動できる）
４docker-compose down：をうつ
５docker-compose up --build -d：をうつ
６docker exec -it blog-app bash：をうつ
７composer install：をうつ
８php artisan key:generate：をうつ
９php artisan migrate：をうつ
１０exit：をうつ
localhost:8000が「ite manifest not found at: /var/www/html/public/build/manifest.json」なったら
１npm install：をうつ
２npm run build：をうつ

ーーーーーーーーーー

会員登録を押す
ユーザー名、メールアドレス、パスワード、パスワード（確認用）を入力して「登録」を押す

mailtrapのEmail Testingを開いて、自分が設定した名前を押すと左側の欄にメールが来ます。
メール認証をしたらログインできます。

ーーーーーーーーーー

「新規登録」を押してタイトル、本文に入力して「投稿」を押すと投稿できます・
「詳細」を押すと詳細を見ることができます。
「編集」を押すとタイトル、本文を編集することができ編集するためには「更新」を押します。
「削除」を押すとモータブルウィンドウみたいなものが出てきて最後の警告が出てきます。消したい場合は、「OK」を押して消したくない場合は「キャンセル」を押します。
