# Kittygram 
Приложение для публикации фотографий домашних питомцев
Автор: Дима(github.com/Japrojah)

Описание проекта
----------------
Реализованны возможности публикации постов с фотографиями,
кличкой, цветом, годом рождения и достижениями питомцев.
Достижения питомцев можно создавать самостоятельно.
Цвета шерсти питомцев можно выбрать из предустановленного списка.

Используемые технологии
-------
### Приложение:
'Python 3.9'
'django 2.2.16'
'Node.js'
'npm 9.5.0'
'webcolors==1.11.1'
'Pillow==9.0.0'
'dotenv 1.0.0'
### Cервер:
'Веб-сервер/обратный прокси-сервер Nginx'
'WSGI-сервер gunicorn 20.1.0'

# Как развернуть проект на сервере:
### На сервере устрановить Git:
'sudo apt install git'
#### Проверьте версию Git:
'git --version'

### Клонировать репозиторий с сайте GitHub.com:
'git clone git@github.com:Japrojah/infra_sprint1.git'\
#### Проверьте наличие директории:
'ls'

##### Для удобства дальнейшего просмотра файлов:
Вы можете дополнительно установить утилиту 'tree',
она позволит просматривать всё дерево проекта.
Командой 'sudo apt install tree' - установите утилиту.
Командой 'tree infra_sprint1' - выведите дерево проекта.

### Установите python & venv:
'sudo apt install python3-pip python3-venv -y'

### Перейти в репозиторий проекта, в директорию backend/:
'cd infra_sprint1/backend'

### Создать и активировать виртуальное окружение:
`python -m venv venv`\
'source venv/bin/activate'

### Установите зависимости, проведите миграции и создайте суперпользователя командами:
'pip install -r requirements.txt'
'python manage.py migrate'
'python manage.py createsuperuser'

### Подготовьте к работе фронтенд приложение
#### Деактивируйте виртуальное окружение и установите Node.js на сервере:
'curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - &&\
sudo apt-get install -y nodejs'
'npm -v' - проверьте установку пакетного менеджера
#### Перейдите в директорию infra_sprint1/frontend/ и выполните команды:
'npm i'
'npm run start' - чтобы убедиться в работоспособности приложения.

### Разверните WSGI-сервер, мы рекомендуем воспользоваться Gunicorn
#### Установите Gunicorn с активированным виртуальным окружением:
'pip install gunicorn==20.1.0'

### Не забудьте изменить файл infra_sprint1/backend/settings.py и infra_sprint1/.env
В файл 'settings.py' поступают данные о некоторых переменных из файла '.env', такие как 'SECRET_KEY'.
Вам необходимо самостоятельно обозначить эту переменную в файле '.env'.
создать файл командой - 'sudo touch infra_sprint1/.env'
Открыть файл для редактирования - 'sudo nano infra_sprint1/.env'
#### Далее рекомендуем сразу создать демона для беспрерывной работы Gunicorn, конфигурационный файл уже есть в директории infra_sprint1/infra/ под названием gunicorn_kittygram.service
#### Добавьте его в системную папку и запустим, для этого:
##### Скопируйте файл из директории проекта в системную
'sudo cp /infra_sprint1/infra/gunicorn_kittygram.service /etc/systemd/gunicorn.service'
##### Конфигурации в файле уже прописаны, но вы можете изменить их самостоятельно:
'sudo apt install nano' - установить текстовый редактор, рекомендуем Nano
'sudo nano /etc/systemd/gunicorn.service' - открыть файл в текстовом редакторе Nano

#### Запускаем демона gunicorn:
'sudo systemctl start gunicorn'
'sudo systemctl enable gunicorn'
##### Используйте команду 'sudo systemctl' c параметрами 'start/stop/status'


### Осталось немного. Ещё пара команд. Рекомендуем сделать разминку.
### анекдот:
Встречаются две бабки.
Одна у другой спрашивает:
—Чойта у тебя дед орет?
—Да у него зубы лезут.
—Какие зубы мать, ему же уже 70?
—Да он вставную челюсть проглотил


### Установите веб-сервер и настройте обратный прокси-сервер, мы рекомендуем Nginx:
'sudo apt install nginx -y'

#### Настройте файервол на порты 80-HTTP/443-HTTPS/22-SSH:
'sudo ufw allow 'Nginx Full''
'sudo ufw allow OpenSSH'

#### Активируйте файервол:
'sudo ufw enable'

### Далее необходимо собрать статику для фронтенд приложния и указать её для Nginx:
'npm run build' - в директории taski/frontend/
'sudo cp -r /home/user/infra_sprint1/frontend/build/. /var/www/infra_sprint1/'

#### Скопируйте конфигурационный файл для Nginx:
'sudo cp /infra_sprint1/infra/default /etc/nginx/sites-enabled/default'

#### Запустите Nginx:
'sudo systemctl start nginx'

## Поздравляем, проект разврнут, сервер запущен
