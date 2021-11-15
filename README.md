# docker-rails

https://docs.docker.com/compose/rails/

## install

```shell
# 初回のみ
# Gemfile作成
mkdir myapp && cd myapp
docker run --rm -v "$PWD":/usr/src/vb_app -w /usr/src/vb_app ruby:2.7.1 bundle init
touch Gemfile.lock
sudo chown -R dev: ./
vim Gemfile # gem Rails のコメントアウトを外す
docker-compose run --no-deps app bundle config set path vendor/bundle
docker-compose run --no-deps app bundle install
docker-compose run --no-deps app bundle exec rails new . --force --no-deps --database=postgresql
sudo chown -R $USER:$USER .
vim config/database.yml
docker-compose build
```

### config/database.yml

```text
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password: password
  pool: 5

development:
  <<: *default
  database: myapp_development


test:
  <<: *default
  database: myapp_test
```

### 立ち上げ

```shell
# 開始
docker-compose run app rake db:create
docker-compose up -d
```