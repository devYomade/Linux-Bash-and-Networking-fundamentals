---
 - name: deploy my laravel app
   hosts: all
   become: yes
   become_user: root


   tasks:
     - name: Update all packages
       apt:
         update_cache: yes
         autoclean: yes
         autoremove: yes


     - name: Install (git, apache2 unzip, python 3, curl)
       apt:
        name:
         -  git
         -  unzip
         -  apache2
         -  python3-mysqldb
         -  mysql-server
         -  ufw
    - name: Update "apt"
       apt:
         update_cache: yes
         autoclean: yes


     - name: Install PHP Modules
       apt:
        name:
         - php8.1
         - libaapache2-mod-php
         - php8.1-cli
         - php8.1-mbstring
         - php8.1-xml
         - php8.1-dev
         - php8.1-zip
         - php8.1-mysql


     - name: Allow HTTP
       ufw:
         rule: allow
         proto: tcp

     - name: Allow HTTPS
       ufw:
         rule: allow
         port: "443"
         proto: tcp

     - name: Allow SSH
       ufw:
         rule: allow
         port: "443"
         proto:  tcp

     - name: Allow MySQL
       ufw:
         rule: allow
         port: "3306"
         proto: tcp
         
         
      - name: Update apt
       apt:
         update_cache: yes
         autoclean: yes
         autoremove: yes

     - name: Install Pip
       apt:
         name:  pip
         state: present

     - name: Create a database
       mysql_db:
            login_user: 'root'
            login_password: "1234"
            name: "laravel"
            state: present

     -  name: Create a database user
        mysql_user:
            login_user: 'root'
            login_password: "1234"
            name: "laravel"   
            password: "1234"
            priv: 'Laravel-exam.*:ALL,GRANT'

     -  name: download composer
        get_url:
           url: https://getcomposer.org/installer
           with_items:
           - "php /tmp/compsoer-installer.php"
           - mv composer.phar /usr/local/bin/composer

     -  name: grant composer executable permissions
        ansible.builtin.file:
         path: /usr/local/bin/composer
         mode: "0755"

     -  name: Change the working directory to /var/www/ and create laravel directory
        command: mkdir laravelapp
        args:
         chdir: /var/www/
         creates: laravelapp

     - name: Clone the project repo into a new directory
        git:
         repo: https:// github.com/flamy/laravel-realworld-example-app
         dest: /var/www/laravelapp
         clone: yes
         update: no

     - name: Create the web.php file in the routes directory
       ansible.builtin.copy:
         dest: /var/www/laravelapp/routes/web.php
         content: |
           <?php
           Route::get('/', function () {
               return view('welcome');
           });

     - name: Create an apache virtual host configuration file
       ansible.builtin.copy:
         dest: /var/www/laravelapp/.env
         content: |
          APP_NAME="Laravel Realworld Example App"
          APP_ENV=local
          APP_KEY=
          APP_DEBUG=true
          APP_URL=http://localhost
          APP_PORT=3000
          LOG_CHANNEL=stack
          LOG_DEPRECATIONS_CHANNEL=null
          LOG_LEVEL=debug
          DB_CONNECTION=mysql
          DB_HOST=localhost
          DB_PORT=3306
          DB_DATABASE=laravel-realworld
          DB_USERNAME=laravel
          DB_PASSWORD=1234
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
          MAIL_HOST=mailhog
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
          PUSHER_APP_CLUSTER=mt1
          MIX_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
          MIX_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"
          L5_SWAGGER_GENERATE_ALWAYS=true
          SAIL_XDEBUG_MODE=develop,debug
          SAIL_SKIP_CHECKS=true

