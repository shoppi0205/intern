Docker環境構築
.envに61〜74を打ちます

APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost:8000

LOG_CHANNEL=stack

DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=blog-app
DB_USERNAME=laravel
DB_PASSWORD=secret

docker-compose up -d --build　をターミナルで打ちます。


メールアドレス「test@com」
パスワード「Test2024」
でログインします。

左の青文字新規投稿を押してタイトルと投稿内容を書いて投稿ボタンを押すと新規投稿を追加できます。

詳細を押すと詳細を見ることができます。
編集を押すとタイトルと投稿内容を編集でき、編集後更新ボタンを押すと編集できます。

削除を押すと確認の文が出てきて削除することができます。
