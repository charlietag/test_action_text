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

* Gems - for **active storage image variant**
  * `image_processing`

    ```bash
    # To enable variants (Transforming Images)
    gem 'image_processing'
    ```

* jQuery
  * yarn add jquery
    * {project_name}/app/javascript/packs/application.js

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
  * https://github.com/charlietag/test_action_text/compare/v0.0.0...v0.0.1
* Start to try
  * https://github.com/charlietag/test_action_text/compare/v0.0.1...master


## Note
* This is cool, Action Text helps you to deal with all attached file actions of add / delete. No matter what you do with uploaded file. Trix will detect and do with the related actions.
* SGID (Signed Global ID)
  * **Be aware**
    * Be sure the following is kept safely
      * **master.key** + **credentials.yml.enc**
        * **secret_key_base**
    * Once one of above is gone
      * All SGID (uploaded file , images links would no longer be available)
    * Actually, this is kind of dangerous if use this in Rich HTML (WYSIWYG)
      * Sometimes we need to change `secret_key_base` if it's hacked. But after doing this all images might not be available due to changed SGID
        * Which means Active Storage is not OK for embedded files, images into articles.
  * Change SGID expires in
    * https://stackoverflow.com/questions/52571555/how-do-you-change-the-active-storage-service-url-expires-in-timeout
  * Active Text
    * Default expired after nil minutes (unlimited)
      * `expires_in: nil`
  * Active Storage
    * Default expired after 5 minutes
      * `expires_in: 5.minutes`
