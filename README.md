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

Перехожу в папку с проектом. Установить зависимости:
<pre><code>composer install</code></pre>

Для запуска sail в папке с проектом выполнить:
<pre><code>sail up -d</code></pre>

### laravel framework 12
Нужно сделать ключ приложения
<pre><code>sail artisan key:generate</code></pre>

#### Проблемы с postgreSql - решение
Некоторые из команд, которые инициализируют postgresql могут не отрабатывать нормально, поэтому <br>
захожу в сервис pgsql:

<pre><code>docker exec -it <pgsql-container-name> your_container_name_or_id -U postgres -d laravel
</code></pre>

Выполняю команды одну за другим, ищу тех, которые не отработали <br>
<pre><code>CREATE USER sail WITH PASSWORD 'secret'; # sail уже есть ? выполните строки ниже 
CREATE DATABASE your_database OWNER sail;
GRANT ALL PRIVILEGES ON DATABASE your_database TO sail;
</code></pre>

Теперь доступ в бд восстановлен, выполнить миграции:
<pre><code>sail artisan migrate</code></pre>

Запустить тесты:
<pre><code>sail artisan test</code></pre>

### quasar framework 2.18
Его нужно запустить отдельно, примерная команда имеет вид:
<pre><code>docker exec -it 593c571c890fc22c3b202ae5f83e3ea5083c21bb9af55ee108a34e20b7e7d861 sh</code></pre>

Нужно 2 раза подключиться к терминалу, в первом нужно запустить сам quasar:
<pre><code>npm run dev</code></pre>

Во втором, чтобы запустить тесты, выполнить команду:
<pre><code>npm run test:unit</code></pre>

#### Теперь все готово, можно начинать делать свой крутой проект!
