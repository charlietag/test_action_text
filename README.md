# README
* Try rails built-in packages
  * Action Text

## Packages

* Ruby version
  * 2.7.0

* Rails version
  * 6.0.3.2

## Basic setup
* Gems - useful for dev
  * gem 'pry-rails', :group => :development
  * gem 'bullet', group: 'development'

* jQuery
  * yarn add jquery
    * test_active_storage_preview/app/javascript/packs/application.js

      ```bash
      import "jquery/src/jquery"
      ...
      ```

* bootstrap
  * yarn add bootstrap popper.js (don't add popper v2, bootstrap default requires v1.16) , (no need to import popper.js manually, bootstrap will do it automatically)
    * app/javascript/packs/application.js
      * `import "bootstrap/dist/js/bootstrap"`
    * app/assets/stylesheets/application.css
      * `*= require 'bootstrap/dist/css/bootstrap'`

## Rails setup

* generate scaffold
  * `bin/rails g scaffold Book name:string author:string`

* Install active_storage
  * `bin/rails action_text:install`


## config - credential

* command
  * `EDITOR=vim bundle exec rails credentials:edit`

    ```bash
    development:
      db:
        user: user
        pass: pass

    production:
      db:
        user: user
        pass: pass
    ```

* config/database.yml

  ```bash
  default: &default
    adapter: mysql2
    encoding: utf8mb4
    pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
    username: <%= Rails.application.credentials[Rails.env.to_sym][:db][:user] %>
    password: <%= Rails.application.credentials[Rails.env.to_sym][:db][:pass] %>
    socket: /var/lib/mysql/mysql.sock

  development:
    <<: *default
    database: {project_name}_development

  test:
    <<: *default
    database: {project_name}_test

  production:
    <<: *default
    database: {project_name}_production
  ```

* Create database
  * `bundle exec rails db:create`

## Changes
* Basic config and setup
  * https://github.com/charlietag/test_active_storage_preview/compare/v0.0.0...v0.0.1
* Start to try
  * https://github.com/charlietag/test_active_storage_preview/compare/v0.0.1...master

