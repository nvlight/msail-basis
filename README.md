<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

## Про приложение

На борту контейнер с 4 сервисами:
1. sail-8.4 (php 8.4 + laravel 12)<br>
2. postgreSql 17<br>
3. Quasar 2.18<br>
4. Redis<br>

Для начала нужно установить php 8.4 + composer (у меня windows 10 + wsl2 (ubuntu 24.04)).<br>
В открытом windows terminal пишем:
<pre><code>sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt update</code>
</pre>

Далее нужно установить зависимости:
<pre><code>composer install</code></pre>

Для запуска sail в папке с проектом выполнить:
<pre><code>sail up -d</code></pre>

### laravel 12
Нужно сделать ключ приложения
<pre><code>sail artisan key:generate</code></pre>

#### Зайти в psql как postgres
docker exec -it <pgsql-container-name> psql -U postgres -d laravel

#### Выполнить SQL:
CREATE USER sail WITH PASSWORD 'secret'; # sail уже есть, круто да?!
CREATE DATABASE your_database OWNER sail;
GRANT ALL PRIVILEGES ON DATABASE your_database TO sail;
\q

Нужно выполнить миграции:
<pre><code>sail artisan migrate</code></pre>

Запустить тесты:
<pre><code>sail artisan test</code></pre>

### quasar framework
Его нужно запустить отдельно, примерная команда имеет вид:
<pre><code>docker exec -it 593c571c890fc22c3b202ae5f83e3ea5083c21bb9af55ee108a34e20b7e7d861 sh</code></pre>
Вместо id моего сервиса нужно прописать тот, который у вас сформировался. <br>

Нужно 2 раза подключиться к терминалу, в первом нужно запустить сам quasar:
<pre><code>npm run dev</code></pre>

Во втором, чтобы запустить тесты, выполнить команду:
<pre><code>npm run test:unit</code></pre>

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT). Again
# msail-basis
