# 環境構築

### api(Rails)側
1. railsプロジェクトの作成
```
docker compose run --no-deps api rails new . --force  -d mysql --api
```
2. gemfileを更新した状態でbuild
```
docker compose build
```
3. api/config/database.yml　に貼り付け
```
default: &default
  adapter: mysql2
  encoding: utf8
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password: passwordadmin
  host: db
  timeout: 5000
 
development:
  <<: *default
  database: development_mydb
 

test:
  <<: *default
  database: test_mydb
 

production:
  <<: *default
  database: myapp_production
  username: myapp
  password: <%= ENV["MYAPP_DATABASE_PASSWORD"] %>

```
4. dbの作成
```
docker compose run api rails db:create
```
### front(React)側
1. reactプロジェクトの作成
```
docker compose run --rm front sh -c "npm install -g create-react-app && create-react-app reactapp"
```
