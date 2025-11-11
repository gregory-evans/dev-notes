# TMUX

`Tmux` - это утилита мультиплексор. Она решает задачу предоставления доступа к нескольким терминалам в рамках одного экрана. Также она сохраняет состояние сессий даже при отключении пользователя от терминала (между рабочими сессиями). Полезна в задаче многооконной организации рабочего пространства при отсутствии подобной возможности у терминальной программы (например Alacritty). Является развитием мультиплексора Screen.

> Github репозиторий проекта - https://github.com/gpakosz/.tmux.git

## Принцип работы

Сервер `tmux` создает **сессию** как совокупность некоторого количество (от одного) псевдотерминалов. В рамках **сессии** может быть создано одно или несколько **окон**. Экран может отображать одно **окно** или разделен на некоторое количество так называемых **панелей**, каждой из которых принадлежит псевдотерминал. 

## Установка

 ```bash
 $ sudo apt install -y tmux
 ```

## Настройка

Установим набор скриптов и настроек `Oh-my-tmux`. Репозиторий проекта - https://github.com/gpakosz/.tmux. Берем с главной страницы проекта необходимые команды и выполняем:

```bash
curl -fsSL "https://github.com/gpakosz/.tmux/raw/refs/heads/master/install.sh#$(date +%s)" | bash
```

В конфигурационном файле `~/.config/tmux/tmux.conf.local` найти следующие строки и раскоментировать их:

```bash
#tmux_conf_theme_left_separator_main='\uE0B0'  # /!\ you don't need to install Powerline
#tmux_conf_theme_left_separator_sub='\uE0B1'   #   you only need fonts patched with
#tmux_conf_theme_right_separator_main='\uE0B2' #   Powerline symbols or the standalone
#tmux_conf_theme_right_separator_sub='\uE0B3'  #   PowerlineSymbols.otf font, see README.md

```

> находящиеся выше 4 строки при этом нужно закоментировать



tmux:

Создание новой сессии 
tmux new-session -s test

Отсоединение
Ctrl + B -> D

Присоединение
tmux attach -t test

Управляющая по умолчанию
Ctrl + B

Создание нового окна
Ctrl + B -> C

Переход между окнами
Ctrl + B -> 0, Ctrl + B -> 1... etc

Горизонтальное разделение
Ctrl + B -> %

Вертикальное разделение
Ctrl + B -> "

Медр уразделенными терминалами
Ctrl + B -> right_arrow, Ctrl + B -> left_arrow etc... (up_arrow, down_arrow)