# docker-rails

https://docs.docker.com/compose/rails/

## install

```shell
# 初回のみ
docker-compose run --no-deps web rails new . --force --database=postgresql
sudo chown -R $USER:$USER .
docker-compose build
vim config/database.yml
```

## config/database.yml

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

## develop

```shell
# 開始
docker-compose run web rake db:create
docker-compose up -d
```