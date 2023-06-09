[Визитная карточка команды](https://github.com/Legendary2/GB_CommandProgCPP_team3/wiki)

[Инструкция по развертыванию ПО "THare"](https://github.com/Legendary2/GB_CommandProgCPP_team3/edit/main/README.MD#%D0%B8%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%86%D0%B8%D1%8F-%D0%BF%D0%BE-%D1%80%D0%B0%D0%B7%D0%B2%D0%B5%D1%80%D1%82%D1%8B%D0%B2%D0%B0%D0%BD%D0%B8%D1%8E-%D0%BF%D0%BE-thare)

[Правила работы с репозиторием](https://github.com/Legendary2/GB_CommandProgCPP_team3/edit/main/README.MD#%D0%BF%D1%80%D0%B0%D0%B2%D0%B8%D0%BB%D0%B0-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D1%8B-%D1%81-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B5%D0%BC)

[Рабочий процесс команды №3](https://drive.google.com/file/d/1KAaR9hctvW2iiWwgqO0asiC_NJ4L_I4n/view?usp=share_link)

[First Release Notes](https://github.com/Legendary2/GB_CommandProgCPP_team3/releases/tag/v.0.1.0)

[Second Release Notes](https://github.com/Legendary2/GB_CommandProgCPP_team3/releases/tag/v.0.5.0)

# 1. Инструкция по развертыванию ПО "THare".
## 1.1 Требуемое ПО
Для корректной сборки проекта на рабочей станции должно быть предуставновлено следующее ПО:
### Linux Ubuntu 22.04:
1. Qt v6.2.4 LTS.
2. CMake v3.26.
3. 7-Zip
4. Версия glibc выше 2.34

### Windows 10:
1. Qt v6.2.4 LTS.
2. CMake v3.26.
3. 7-Zip

## 1.2 Установка ПО
### Linux Ubuntu 22.04:
1. Qt v6.2.4 LTS

https://docs.google.com/document/d/1kM6dwnTYJyXO_quz3wDepJl7CVUYDPrBvn453UYi1zo/edit

2. CMake

https://cmake.org/install/

3. 7-Zip

https://7-zip.org/download.html

### Windows 10:
1. Qt v6.2.4 LTS

https://rutracker.org/forum/viewtopic.php?t=6196654 (для доступа может потребоваться VPN в браузере)

2. CMake

https://cmake.org/install/

3. 7-Zip

https://7-zip.org/download.html

## 1.3 Развертывание проекта
### Windows 10:
1.3.1 Для того чтобы развернуть проект на вашей системе, в первую очередь требуется склонировать удаленный репозиторий команды.
```
git clone (http репозитория, либо ssh(у кого настроен))
```
1.3.2 Далее необходимо запустить `Qt Creator` по пути `Qt\Tools\QtCreator-7.0.0\bin`
![image](https://user-images.githubusercontent.com/78610228/224943349-cfe887d5-c664-459c-bae1-49a56a232b05.png)

1.3.3 На ветке `main` находится актуальный рабочий релиз, который требуется запустить через`QtCreator`
![image](https://user-images.githubusercontent.com/78610228/220890872-9cc25359-4a32-40b5-9587-f43309324ba1.png)

1.3.4 Для сборки проекта под `Windows` выбираем компилятор `MSVC`.
![image](https://user-images.githubusercontent.com/78610228/220891376-5fb55256-802e-4473-b8d6-c1af8b86f7d6.png)

1.3.4.1 Для проекта на `Windows` также может понадобится дополнительно скачать сборщик проекта [`Ninja`](https://drive.google.com/file/d/17m5o9hbwFz5loNbDy6oWGuOKzn1AGMfn/view?usp=share_link) и добавить его в директорию Qt. Затем необходимо добавить путь до файла .exe в переменную среды Windows `PATH`.

### Linux Ubuntu 22.04:

Здесь будут приведены два способа: А) с использованием инструментов командной строки, а также Б) при помощи `IDE QtCreator`.

#### А. С помощью инструментов командной строки

1. Получение исходных кодов проекта. Исходники можно получить с главной странички проекта: `https://github.com/Legendary2/GB_CommandProgCPP_team3/tree/main`любым удобным способом, например  склонировав их себе в локальное хранилище при помощи утилиты `git`:

```
git clone git@github.com:Legendary2/GB_CommandProgCPP_team3.git
```

2. Переходим в директорию, содержащую исходный код:

```
cd GB_CommandProgCPP_team3/EditorTeam
```

3. Создаём здесь каталог для сборки и переходим в него:

```
mkdir build && cd $_
```

4. Генерация скриптов сборки. На этом этапе вероятны два варианта развития событий. Если вы устанавливали в систему библиотеку разработчика Qt6 с помощью пакетного менеджера, то все необходимые пути в переменных окружения уже должны быть прописаны и поэтому достаточно выполнить команду:

```
cmake ..
```

В другом случае, если `Qt6` был установлен в обход пакетного менеджера, либо же в силу каких-либо обстоятельств настройки переменных окружения, отвечающих за хранение путей размещения `Qt6` сбились, то для генератора скриптов сборки эти пути нужно задать явно. К примеру, `Qt6` был установлен в домашний каталог текущего пользователя в директорию `~/Qt`, тогда команда будет следующей:

```
cmake -DCMAKE_PREFIX_PATH=$HOME/Qt/6.2.4/gcc_64 -DQt6_DIR=$HOME/Qt/6.2.4/gcc_64/lib/cmake/Qt6 ..
```

5. Непосредственно сама сборка проекта:

```
cmake —build .
```


#### Б. При помощи `IDE QtCreator`

1. 	Получение исходных кодов проекта. Их можно скачать в виде zip-архива с помощью веб-браузера с  главной  странички проекта `https://github.com/Legendary2/GB_CommandProgCPP_team3/tree/main`, либо же воспользовавшись утилитой `git`:

```
git clone git@github.com:Legendary2/GB_CommandProgCPP_team3.git
```

2. Запустим `qtcreator`, кликнем `Open Project` и в диалоговом окошке выберем файл `CmakeLists.txt` (директория `GB_CommandProgCPP_team3/EditorTeam/`):
![image](https://user-images.githubusercontent.com/78610228/224943596-14bd2ccf-25f9-4a04-917e-f110b7f3294f.png)

3. Далее необходимо настроить проект, выбрав нужный комплект сборки. Крайне рекомендуем использовать `LTS` версию `6.2.4`:
![image](https://user-images.githubusercontent.com/78610228/224943664-8fd45a78-3a5a-488f-b694-2d1d5ecc78d4.png)

4. После открытия и настройки проекта его можно будет собрать (иконка «Молоточек»), либо даже сразу собрать-запустить (иконка «Зелёный треугольник»):

![image](https://user-images.githubusercontent.com/78610228/224943728-cc8540ad-3b3a-48dc-bba4-8bd97348c327.png)


# 2. Правила работы с репозиторием
###
2.1 Клонируем репозиторий на локальный компьютер командой:

```
git clone (http репозитория, либо ssh(у кого настроен))
```
http(ssh) берется на главной странице репозитория, нужно нажать зеленую кнопку `Code` и скопировать оттуда http(ssh.
###

2.2 Переходим через консоль `Git bash` в папку со склонированным репозиторием и выполняюм следующую команду для перехода на ветку `develop`:
```
git checkout develop
```
###
2.3 Далее выполняем синхронизацию с удаленным репозиторием, вводя следующие команды:
```
git fetch
git pull
```
Команды `fetch` и `pull` требуется выполнять каждый раз при начале работы с веткой.
###
2.4 Переходим на локальную рабочую ветку.
Если ветка не существует, создаем ее следующее командой:
```
git checkout -b название_ветка
```
Если она существует, осуществляем на нее переход как обычно:
```
git checkout название_ветки
```
###

2.5 Закончив работу на ветке и убедившись в том, что все сделано правильно, добавляй файлы в проект командами:

```
git add .
git commit -m 'Содержание коммита`
```
###
2.6 Далее выполняется загрузка изменений на удаленный репозиторий.
Если ветка на удаленном репозитории не существует, выполняем следующую команду:
```
git push -u origin название_ветки
```
Если ветка уже существует на удаленном репозитории, то выполняем следующую команду
```
git push
```
