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

Файл настроек tmux
~/.tmux.conf

Переопределение контрольного сочетания
set-option -g prefix C-q

Включить мышь для изменения размеров разделеных терминалов
set -g mouse on

###
https://github.com/gpakosz/.tmux.git