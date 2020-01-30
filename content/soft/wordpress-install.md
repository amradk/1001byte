Title: Установка Wordpress
Date: 10-21-2018 13:06
Category: PC
Tags: Linux, soft, wordpress

# Ведение

Ставь Wordpress сказал я, установка занимает 5 минут! Вот только я не учел что 5 минут это если все остальное уже готово: php, MySQL и nginx. В конечном итоге человек, которому я посоветовал установить Wordpress, с задачей справился, хотя и пришлось потратить гораздо больше времени. Раз так то я решил напирасть написать небольшое руководство по установке.

# Термины и определения

* СУБД - Система Управления Базами Данных - ком­плекс про­грамм, по­зво­ляю­щих соз­дать ба­зу дан­ных (БД) и ма­ни­пу­ли­ро­вать дан­ны­ми (встав­лять, об­нов­лять, уда­лять и вы­би­рать). Система обес­пе­чи­ва­ет безо­пас­ность, на­дёж­ность хра­не­ния и це­ло­ст­ность дан­ных, а так­же пре­дос­тав­ля­ет сред­ст­ва для ад­ми­ни­ст­ри­ро­ва­ния БД.
* [php] (https://www.php.net/manual/ru/preface.php) - PHP, расшифровывающийся как "PHP: Hypertext Preprocessor" - «PHP: Препроцессор Гипертекста», является распространенным интерпретируемым языком общего назначения с открытым исходным кодом. PHP создавался специально для ведения web-разработок и код на нем может внедряться непосредственно в HTML-код. Синтаксис языка берет начало из C, Java и Perl, и является легким для изучения. Основной целью PHP является предоставление web-разработчикам возможности быстрого создания динамически генерируемых web-страниц, однако область применения PHP не ограничивается только этим. 
* [php-fpm] (https://www.php.net/manual/ru/install.fpm.php) - FPM (FastCGI Process Manager, менеджер процессов FastCGI) является альтернативной реализацией PHP FastCGI с несколькими дополнительными возможностями обычно используемыми для высоконагруженных сайтов.
* [cgi] (http://students.uni-vologda.ac.ru/pages/pm97/cgi/cgi.html) - (Common Gateway Interface – Общий интерфейс маршрутизации) служит для обеспечения связи внешней прикладной программы с Web-сервером. Обычно Web-серверы возвращают статическую информацию, то есть вы набираете некоторый URL (в своем браузере) в котором задаете имя ресурса, который вы хотите получить. Web-сервер анализирует ваш запрос и отсылает вам то что вы там хотели (или сообщение об ошибке, если указанный вами ресурс недоступен) вот вообщем-то и весь World Wide Web. Во всем этом есть одна проблема информация которую посылает сервер по своей природе статична. Сервер не может вам послать больше того что у него есть на момент вашего запроса. Вот чтобы изменить эту ситуацию к лучшему и был введен стандарт CGI. CGI – расширяет возможности Web-сервера, тем что информация поступаемая от Web-сервера приобретает динамический характер. Делается это следующим образом: Если в URL (в броузере) указать не какой-нибудь статический ресурс, а специальную программу (CGI-скрипт) . А сервер проанализировав такой запрос возьмет и запустит ее. А она в свою очередь (пользуясь всеми ресурсами сервера) выдаст некоторую динамическую информацию (например: страничку) . А Web-сервер после окончания работы CGI-скрипта отправит эту информацию броузеру предварительно снабдив ее нужным для протокола HTTP заголовком.
* [веб-сервер] (https://developer.mozilla.org/ru/docs/Learn/%D0%A7%D1%82%D0%BE_%D1%82%D0%B0%D0%BA%D0%BE%D0%B5_%D0%B2%D0%B5%D0%B1_%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80) - сервер принимающий HTTP-запросы от клиентов, обычно веб-браузеров, и выдающий им HTTP-ответы, как правило, вместе с HTML-страницей, изображением, файлом, медиа-потоком или другими данными.
* [nginx] (https://nginx.org/ru/) - это HTTP-сервер и обратный прокси-сервер, почтовый прокси-сервер, а также TCP/UDP прокси-сервер общего назначения.
* [CMS] (https://ru.wikipedia.org/wiki/%D0%A1%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0_%D1%83%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F_%D1%81%D0%BE%D0%B4%D0%B5%D1%80%D0%B6%D0%B8%D0%BC%D1%8B%D0%BC) - Content management system (система управления содержимым) - информационная система или компьютерная программа, используемая для обеспечения и организации совместного процесса создания, редактирования и управления содержимым, иначе — контентом.
* FQDN - Fully Qualified Domain Name -«полностью определённое имя домена», иногда сокращается до «полное имя домена») — имя домена, не имеющее неоднозначностей в определении. Включает в себя имена всех родительских доменов иерархии DNS.
* DNS - (Domain Name System «система доменных имён») — компьютерная распределённая система для получения информации о доменах. Чаще всего используется для получения IP-адреса по имени хоста (компьютера или устройства).

# Что такое Wordpress

Для тех кто не знает но очень хочет узнать расскажу немного о том что такое Wordpress. Wordpress это одна из самых известных open source CMS. CMS (content management system)- это система управления содержимым web-сайта. Т.е. это специальное программное опеспечение, которое устанавлвется на сервере и позвроляет посредством web - интерфейса управлять содержимым вашего сайта, а именно добавлять или удалять статьи, загружать картинки, размещать новости, придавать всему этому симпатичный вид без написания кода. Wordpress написан на языке PHP (плюс JavaScript, HTML и CSS, куда же без них в web'е) а это значит что нам подребуется что-либо что сможет выполнять PHP код. Нам будет нужен интерпритатор PHP. Также понадобиться СУБД для храниния различных настроек и текста, размещаемых материалов, обычно в качестве СУБД используют MySQL. Также понадобиться ПО web-сервер чтобы принимать запросы пользователей и возвращать ответ, обычно это Apache или Nginx. Далее в качестве СУБД я буду использовать MySQL, в качестве web-сервера Nginx, а исполнять PHP код будет php-fpm, в качестве ОС Debian или Ubuntu Linux.

# Этап I: подготовка

Мне не удалось найти ссылку на документацию на русскоязычной версии сайта Wordpress (https://ru.wordpress.com/) поэтому я оставлю ее здесь https://wordpress.org/support/. Для начала заглянем в раздел [Installing WordPress/Before You Install] (https://wordpress.org/support/article/before-you-install/). В этом рахделе приведен список ПО необходимого для работы WordPress. Особое внимание стоит удилить версиям ПО т.к. если выполнить утановку на неподдерживаемые версии (слишком старые или слишком новые) то в лучшем случае ваш сайт просто не заработает, в худшим можно столкнуть с неожиданным поведением ПО. Т.к. часто начальный этап разработки сайта выполняется на компьютере разработчика а потом выполняется перенос на сервер то важно обедиться что и там и там установлено ПО одинаковых версий или хотя бы должны совпадать первый две цифры версии. ```надо привести пример```

## Установка PHP

Уcтановка для Debian 10:
в репозиториях 10-ой вурсии Debian присутствуют пакеты с необходимой версией php, поэтому все просто
apt install --no-install-recommends php php-fpm

Уcтановка для Ubuntu 16.04:
в репозиториях Ubuntu нужной версии нет, придется подключать дополнительный PPA репозиторий
apt install software-properties-common python-software-properties
у add-apt-repository есть некотороые особенности [при работе с локалями] (https://bugs.launchpad.net/ubuntu/+source/software-properties/+bug/1165569), поэтому сделаем так
LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
apt update
apt install --no-install-recommends php7.3 php7.3-cli php7.3-common php7.3-fpm php7.3-mysql

## Настройка php-fpm

В Debian менять конфиг не потребуется, нужно лишь запомнить значение опций listen, listen.owner, listen.group:
```
grep "^listen" /etc/php/<version>/fpm/pool.d/www.conf

listen = /run/php/php<version>-fpm.sock
listen.owner = www-data
listen.group = www-data
```
В Ubuntu возможно придется сменить пользователя и группу с www-data на nginx.

## Установка MySQL

Я собираюсь использовать MySQL, пакета с сервером БД нет в репозиториях ни Debian 10, ни Ubuntu 16.04:

Debian
```
su -
cd /tmp
wget https://dev.mysql.com/get/mysql-apt-config_0.8.14-1_all.deb
dpkg -i mysql-apt-config*
apt update
apt install mysql-server
mysql_secure_installation
```
Ubuntu
```
su -
cd /tmp
wget https://dev.mysql.com/get/mysql-apt-config_0.8.14-1_all.deb
sudo dpkg -i mysql-apt-config*
sudo apt update
sudo apt install mysql-server
sudo mysql_secure_installation
```

## Настройка MySQL

Добавим несколько опций в конфиг MySQL, которые в дальнейшем упростят нам жизнь. Установим значение кодировки по умолчанию, заставим MySQL слушать только localhost (мы ведь не хотим чтобы кто угодно мог постучаться в нашу базу). Плюс еще несколько настроек для небольшего сервера с 1Gb RAM. Добавим несколько строк в файл ```/etc/mysql/mysql.conf.d/mysqld.cnf```:
```
default-storage-engine         = InnoDB
tmp-table-size                 = 32M
max-heap-table-size            = 32M
innodb-flush-method            = O_DIRECT
innodb-log-files-in-group      = 2
innodb-log-file-size           = 64M
innodb-flush-log-at-trx-commit = 1
innodb-file-per-table          = 1
innodb-buffer-pool-size        = 600M
log-error                      = /var/lib/mysql/mysql-error.log
log-queries-not-using-indexes  = 1
slow-query-log                 = 1
slow-query-log-file            = /var/lib/mysql/mysql-slow.log
bind-address                   = 127.0.0.1
init_connect='SET collation_connection = utf8_general_ci'
init_connect='SET NAMES utf8'
default-character-set=utf8
character-set-server=utf8
collation-server=utf8_general_ci
skip-character-set-client-handshake
```
Если вы планируете использовать версию MySQL 8.* то в конфигурационный файл необходимо добавить строчку:
```
default_authentication_plugin=mysql_native_password
```
Это связано с тем что с 8-ой версии MySQL сменил протокол авторизации пользователей на более защищенный. Wordpress пока еще не поддерживает новый тип авторизации.
После внесения изменений нужно перезапустить mysql:
```
sudo systemctl restart mysql
```

Документация по MySQL от Wordpress (https://wordpress.org/support/article/creating-database-for-wordpress/#using-the-mysql-client, )
Хорошой практикой будет создать отдельного пользователя в MySQL для подключения приложения (в нашем случае Wordpress) к базе данных. Создадим пользователя и базу данных.
```
mysql -u root -p -e 'create database myblogdb CHARACTER SET utf8 COLLATE utf8_general_ci'
mysql -u root -p -e "CREATE USER 'myblog_user'@'localhost' IDENTIFIED BY 'MyPassword'"
mysql -u root -p -e "GRANT ALL PRIVILEGES ON myblogdb.* TO 'myblog_user'@'localhost'"
mysql -u root -p -e "FLUSH PRIVILEGES"
```
Если пользователь был создан в версии MySQL 8.* до того как опция ```default_authentication_plugin=mysql_native_password``` была добавлена в конфигурационный файл то для этого пользователе протогол аутентификации не будет сменен, нужно вручную сменить протокол, сделать это можно с помощью следующей команды:
```
ALTER USER 'myblog_user'@'localhost' IDENTIFIED WITH mysql_native_password BY 'MyPassword';
```

## Установка nginx

Установка nginx будет самой простой, но вот а настройке такого не скажешь.
```
sudo apt install nginx
```

## Установка wordpress

В репозиториях многих Linux-дистрибутивов есть установочные пакеты для wordpress'а, но не будем ими пользоваться по нескольким причинам:
* версия в репозитории может быть довольно старой,
* ОС на сервере и на машине разработчика могут отличаться,
* возможны случаи когда возникнет необходимость изменения каких-либо файлов в директории CMS, в таком раскладе переноса не избежать.
Установка Wordpress'а из архива состоит из нескольких этапов:
1. создать директорию
2. загрузить с сайта архив с нужной версией CMS Wordpress
3. распаковать архив
4. выставить необходимые права на файлы и директории
5. внести изменения в wp-config.php
6. это еще не все

1. Обычно, при установке, nginx создает директорию /var/www. Вот там мы и расместим файлы своего будущего сайта:
```
sudo mkdir /var/www/myblog
```
2. Список доступных для скачавания версий Wordpress доступен по адресу: https://wordpress.org/download/releases/. Мы будем использовать самую свежую версиию, которую можно скачать во ссылке: https://wordpress.org/latest.tar.gz
```
wget https://wordpress.org/latest.tar.gz
sudo mkdir /var/www/myblog
sudo tar -xvzf ./latest.tar.gz -C /var/www/myblog/
sudo mv /var/www/myblog/wordpress/* /var/www/myblog/
sudo rmdir /var/www/myblog/wordpress
sudo chown -R www-data:www-data /var/www/1001byte
```
В Ubuntu в последней команде www-data надо заменить на nginx.

## Настройка Wordpress

Для настройки Wordpress нам понадобиться прописать параметры подключения к БД и еще несколько параметров.
```
cp /var/www/1001byte/wp-confif-sample.php /var/www/1001byte/wp-config.php
```
Чтобы настроить подключение к БД нужно изменить следующие параметры:
```
define( 'DB_NAME', 'myblogdb' );
define( 'DB_USER', 'myblog_user' );
define( 'DB_PASSWORD', 'MyPassword' );
define( 'DB_HOST', 'localhost' );
define( 'DB_CHARSET', 'utf8' );
define( 'DB_COLLATE', '' );
```

## Настройка nginx

Пример конфигурации виртуального сервера для Wordpess можно найте на сайте [nginx] (https://www.nginx.com/resources/wiki/start/topics/recipes/wordpress/?__cf_chl_captcha_tk__=d62abf0932542e2bfb96662cc2af3dc0ff198029-1580153563-0-AZbhHYHKICwAk9tr4BYLWdZFXkPyGrfApuEXa2VQ2CLjXRQOyeoi-2xWSN1yl4SqdiBsF6K0voNBme2YAzmo7_GTAzfnuxgjhxVWwErT3dn8t_1HsL-LkPB11TTUUPkNbIkL5poPucEAdUlTmG9YzbgraFgTeXLs1gfA_Zk5yK7wLgLPqE3ZlGUzKQj6NHMNTAl4NoY0hjpL_OcUfmj7uxlW5NjVUTr4aL7Mz_4U_cmcCQsto5Xt7btSzkozirxWr1nxSIDEoJgnbPEWOnMsll-FVJxEaR2xZg4aIQgIgxGtE8gS9a4hO0awUGHeLqQacZ89qvJ4RiRXc1H6Tke_iXGSzj6n3yjuZZpOSqWmR2t0), им и воспользуемся. Создатим файл ```/etc/nginx/sites-availabe/myblog.conf``` и скопируем туда настройки. Далее нам понадобиться заменить значение некоторых опций:
* ```server``` в разделе ```upstream```,
* ```root``` в разделе ```server``` - путь к директории в которой располагаются файлы сайта,
* ```server_name``` в разделе ```server``` - DNS имя вашего сайта,
* настройки fastcgi в разделе ```location ~ \.php$```.

```
upstream php {
        server unix:<path_to_php_socket>;
}

server {
        server_name <fqdn_name>;
        root <path_to_site_root>;
        index index.php;

        location = /favicon.ico {
                log_not_found off;
                access_log off;
        }

        location = /robots.txt {
                allow all;
                log_not_found off;
                access_log off;
        }

        location / {
                # This is cool because no php is touched for static content.
                # include the "?$args" part so non-default permalinks doesn't break when using query string
                try_files $uri $uri/ /index.php?$args;
        }

        location ~ \.php$ {
                include fastcgi_params;
                fastcgi_intercept_errors on;
                fastcgi_param   SCRIPT_FILENAME $document_root$fastcgi_script_name;
                fastcgi_pass php;

        }

        location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
                expires max;
                log_not_found off;
        }
}
```

Начнем по порядку. Из документации [nginx] (https://nginx.org/ru/docs/http/ngx_http_upstream_module.html): upstream позволяет описывать группы серверов, которые могут использоваться в директивах proxy_pass, fastcgi_pass, uwsgi_pass, scgi_pass, memcached_pass и grpc_pass. Т.е. upstream это абстракция, которая позволяет спрятать за собой несколько экземпляров бэкэнда  выполнять балансировку запросов между ними. Это бывает очень полезно в случайх когда бэкэнд имее какие-либо тхнические особенности и/или ограничения (например, по одному процессу бэкэнда на одно я дро процессора) или же требуется несколько экземпляров бкэнда, котороые запущенны на разных серверах, чтобы справиться с нагузкой. В нашем случае под дерективой upstream будет всего одна запись - путь к unix сокету интерпретатора php. Мы уже получали путь к сокету в пункте про настройку php-fpm, напомню как это можно сделать - ```grep "^listen" /etc/php/<version>/fpm/pool.d/www.conf | grep sock```.
```
manul@manulpc:~$ grep "^listen" /etc/php/7.3/fpm/pool.d/www.conf | grep sock
listen = /run/php/php7.3-fpm.sock
```
Полученное значение нужно прописать в секции upstream вместо <path_to_php_socket>.

Далее в секции ```server``` вместо <path_to_site_root> укажем корректный путь к директории в которой располагаются файлы сайта. Напомню что мы ранее уже создали директории ```/var/www/myblog``` и распоковали в нее CMS Wordpress в пункте про установку wordpress. Конечный вид: ```root /var/www/myblog;```.

```server_name``` вместо <fqdn_name> вставляем DNS имя вашего сайта. Если первое развертывание проходит на машине разработчика то в качестве имени можно указать ```localhost```. Указывать ```llcalhost``` в качестве ```server_name``` может быть весьма непрактично особенно если планируется разворачивать более одного экземпляра CMS. Решить эту проблему можно использовав удобные имена, например, ```dev-myblog```, но чтобы такая схема заработала нужно внести соответствующую запись в ```/etc/hosts```:
```
127.0.0.1 dev-myblog.localdomain dev-blog
```
!!! Внимание, при использовании данного метода лучше не использовать настоящие имя сайта !!!

С настройками cgi из примера с сайта nginx у меня wordpress не заработал, пришлось их немного изменить:
```
location ~ \.php$ {
        include fastcgi_params;
        fastcgi_intercept_errors on;
        fastcgi_param   SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_pass php;
}
```

Хм... похоже что все, осталось перезапустить php-fpm, nginx и приступить к дальнейшей настройке Wordpress уже через веб-интерфейс.
