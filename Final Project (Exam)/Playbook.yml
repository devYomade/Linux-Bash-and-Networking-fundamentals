---
- name: deploy my laravel app
  hosts: all
  remote_user: root

  tasks:
    - name: update packages
      apt:
        update_cache: true
        upgrade: true
    - name: install python
      apt:
        name:
          - python3-pip
          - git
          - lsb-release
          - ca-certificates
          - apt-transport-https
          - software-properties-common
          - gnupg2
          - curl
          - wget
          - debconf-utils
          - libaio1
    - name: install mshell: python3 -m pip install PyMySQL
    - name: install cryptography
      shell: pip install cryptography
    - name: install apache2 and utils
      apt:
        name: apache2, apache2-utils
    - name: create repository
      apt_repository:
        repo: ppa:ondrej/php
    - name: update package
      apt:
        update_cache: true
        upgrade: true
    - name: install php modules
      apt:
        name: php8.1, libapache2-mod-php8.1, php8.1-cli, php8.1-common, php8.1-mysql, php8.1-opcache, php8.1-soap, php8.1-zip, php8.1-intl, php8.1-bcmath, php8.1-xml, php8>
    - name: configure mysql
      shell:
        debconf-set-selections <<EOF
        mysql-apt-config mysql-apt-config/select-server select mysql-8.0
        "mysql-community-server mysql-community-server/root-pass password root"
        "mysql-community-server mysql-community-server/re-root-pass password root"
        EOF
    - name: Install Composer Globally
      shell: wget --user-agent="Mozilla" -O /tmp/mysql-apt-config_0.8.24-1_all.deb htttps://dev.mysql.com/get/mysql-apt-config_0.8.24-1_all.debysql
    - name: edit
      shell: sudo DEBIAN_FRONTEND=noninteractive dpkg -i /tmp/mysql-apt-config_0.8.24-1_all.deb < /dev/null > /dev/null
    - name: update package
      apt:
        update_cache: true
        upgrade: true
    - name: install mysql1
      shell: DEBIAN_FRONTEND=noninteractive apt-get install mysql-server mysql-client --assume-yes --force-yes < /dev/null > /dev/null
    - name: create database
      shell: 'mysql -ne "{{ item }}"'
      with_items:
        - CREATE DATABASE laravel;
    - name: create user
      shell: 'mysql -ne "{{ item }}"'
      with_items:
        - CREATE USER 'laravel'@'localhost' IDENTIFIED BY 'laravel';
    - name: grant all privileges
      shell: 'mysql -ne "{{ item }}"'with_items:
        - GRANT ALL PRIVILEGES ON laravel.* TO 'laravel'@'localhost';
    - name: flush privileges
      shell: 'mysql -ne "{{ item }}"'
      with_items:
        - FLUSH PRIVILEGES;
    - name: change directory
      copy:
        src: /home/vagrant/pgsql.sh
        dest: /root
    - name: create script
      shell: bash /root/pgsql.sh
    - name: clone repo
      shell: git clone https://github.com/f1amy/laravel-realworld-example-app.git /var/www/laravel
    - name: Create an apache virtual host configuration file
      copy:
        dest: /var/www/laravel/.env
        content: |
          APP_NAME="Laravel"
          APP_ENV=local
          APP_KEY=
          APP_DEBUG=true
          APP_URL=https://localhost
          APP_PORT=3000
          LOG_CHANNEL=stack
          LOG_DEPRECATIONS_CHANNEL=null
          LOG_LEVEL=debug
          DB_CONNECTION=mysql
          DB_HOST=localhost
          DB_PORT=3306
          DB_DATABASE=laravel
          DB_USERNAME=laravel
          DB_PASSWORD=laravel
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
    - name: Create the web.php file in the routes directory
      blockinfile:
        path: /var/www/laravel/routes/web.php
        block: |
          Route::get('/', function () {
            return view('welcome');
          });
    - name: file permission
      shell: chown -R root:root /var/www/laravel
    - name: file permission
    - name: file permission
      shell: chmod -R 0755 /var/www/laravel
    - name: file permission
      shell: chmod -R 0755 /var/www/laravel/storage
    - name: file permission
      shell: chmod -R 0755 /var/www/laravel/bootstrap/cache
    - name: create .htaccess file
      copy:
        dest: "/var/www/laravel/.htaccess"
        content: |
          <IfModule mod_rewrite.c>
            RewriteEngine On
            RewriteCond %{REQUEST_URI} !^/public/
            RewriteCond %{REQUEST_FILENAME} !-d
            RewriteCond %{REQUEST_FILENAME} !-f
            RewriteRule ^(.*)$ /public/$1
            RewriteRule ^(/)?$ public/index.php [L]
          </IfModule>
    - name: install composer
      shell: php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
    - name: Verify Installation Script is Safe to Run
      shell: php -r "if (hash_file('sha384', 'composer-setup.php') === '55ce33d7678c5a611085589f1f3ddf8b3c52d662cd01d4ba75c0ee0459970c2200a51f492d557530c71c15d8dba01eae') >
    - name: composer setup
      shell: php composer-setup.php
    - name: unlink composer
      shell: php -r "unlink('composer-setup.php');"
    - name: move composer.phar to another directory
      shell: mv composer.phar /usr/local/bin/composer
    - name: change directory and create composer project
      shell: cd /var/www/laravel && composer create-project -n
    - name: change directory and run php artisan
      shell: cd /var/www/laravel && php artisan migrate --seed
    - name: Create an apache virtual host configuration file
      copy:
        dest: "/etc/apache2/sites-available/domain.conf"
        content: |
          <VirtualHost *:80>
              ServerAdmin email@miniprojec.com
              ServerName miniprojec.com
              ServerAlias miniprojec.com
              DocumentRoot /var/www/laravel/public
              <Directory /var/www/laravel/public>
                  Options Indexes FollowSymLinks
                  AllowOverride All
                  Require all granted
              </Directory>
              ErrorLog ${APACHE_LOG_DIR}/error.log
              CustomLog ${APACHE_LOG_DIR}/access.log combined
          </VirtualHost>
    - name: Disable default apache  page
      shell: a2dissite 000-default.conf
    - name: enable laravel page
      shell: a2ensite laravel.conf
    - name: Enable a2enmod rewrite
      shell: a2enmod rewrite
    - name: restart apache
      service:
        name: apache2
        state: restarted
    - name:  Change file ownership, group and permissions
      shell: chown -R www-data:www-data /var/www/laravel
    - name: make snapd
      apt:
        name:
          - snapd
    - name: install core
      shell: snap install core
    - name: refresh core
      shell: snap refresh core
    - name: install certbot
      shell: snap install --classic certbot
    - name: move
      shell: ln -s /snap/bin/certbot /usr/bin/certbot
    - name: send mail
      shell: yes | certbot --apache --agree-tos --redirect -m email@domain.com -d domain.com
      
                                                                             
