# Установка и настройка WSL в Windows 10

Сначала необходимо проверить включена ли возможность виртуализации на процессоре. Для этого открыть диспетчер задач (`Ctrl + Shift + Esc`, `Ctrl + Alt + Del`), на вкладке производительность выбрать `ЦП` и убедиться, что параметр `"Виртуализация"` в состоянии `Включено`. Если виртуализация находится в состоянии `"Отключено"`, тогда необходимо в `BIOS` (`UEFI`) включить данную возможность. Необходимо искать раздел `"Advanсed"` или `"CPU Configuration"`. Нужная нам опция часто называется `"Intel Virtualization Technology"` для процессоров Intel или `"SVM Mode"` для процессоров AMD.

## Установка WSL и дистрибутива Debian

Открыть cmd.exe от имени администратора. Выполнить команду:

```cmd
wsl.exe --install -d Debian
```

Затем запустить установленную версию Linux:

```cmd
Debian
```

После прохождения инициализации и создания имени и пароля нового пользователя, виртуальная машина готова к работе. Выйдем из виртуальной машины.

Установим принудительное использование второй версии `WSL`:

```cmd
wsl --set-version Debian 2
```

Если появится сообщение о необходимости обновления компонента ядра для WSL 2, следует выполнить команду:

```cmd
wsl.exe --update
```

> ### Некоторые полезные данные:
>
> `wsl -l -v` - посмотреть список установленных машин.
>
> Для удаления WSL сначала удалите дистрибутив командой `wsl --unregister <имя_дистрибутива>`, а затем удалите само приложение WSL через «Параметры» > «Приложения» > «Приложения и возможности». Чтобы удалить все связанные с дистрибутивом файлы, можно также вручную очистить папку `%USERPROFILE%\\AppData\\Local\\Packages`
>
> Документация по WSL: https://learn.microsoft.com/ru-ru/windows/wsl/

## Установка и настройка Alacritty

Создадим папки для конфигурации Alacritty:

```cmd
mkdir C:\Users\igrif\AppData\Roaming\alacritty
mkdir C:\Users\igrif\AppData\Roaming\alacritty\themes
```

Поместить файл настроек Alacritty `files\alacritty.toml`  в папку `C:\Users\igrif\AppData\Roaming\alacritty`, а содержимое каталога `files\alacritty-theme-master` в каталог `C:\Users\igrif\AppData\Roaming\alacritty\themes`.

> Расположение тем для Alacritty можно получить из репозитория https://github.com/alacritty/alacritty-theme .

Также необходимо установить недостающие шрифты `Hack Nerd Fonts` из папки `files\Hack` или скачать с сайта https://www.nerdfonts.com/font-downloads.

Теперь можно установить программу `Alacritty`. Дистрибутив находится в директории `files\Alacritty-v0.16.1-installer.msi` или скачать актуальную версию с сайта https://alacritty.org/.

> Можно также использовать Windows Terminal:
>
> https://apps.microsoft.com/detail/9n0dx20hk701?hl=ru-RU&gl=RU

## Установка и настройка ZSH

Установим шелл zsh:

```bash
sudo apt install -y zsh
```

Следующим шагом установим скрипт кастомизации OhMyZsh. Подробности об установке по адресу https://github.com/ohmyzsh/ohmyzsh/wiki, откуда берем и выполняем команду:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Далее установим тему оформления (powerlevel10k). Информация и файлы находятся в репозитории https://github.com/romkatv/powerlevel10k. Установку будем производить через OhMyZsh.

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k"
```

После чего в файле `~/.zshrc` заменим значение параметра `ZSH_THEME` на `"powerlevel10k/powerlevel10k"`. 

После перезапуска оболочки `exec zsh`, автоматически запустится мастер настройки темы. Здесь просто нужно следовать указаниям мастера и выбирать необходимые параметры. 

> Если мастер настройки не запустился автоматически или для переконфигурирования, можно запустить его вручную - `p10k configure`

Установим подсветку синтаксиса в zsh. 

Репозиторий: https://github.com/zsh-users/zsh-syntax-highlighting.

Установка для Oh-my-zsh:

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

И активируем его, для этого редактируем `~/.zshrc`

```bash
plugins=( [plugins...] zsh-syntax-highlighting)
```

Установка плагина авто дополнений устанавливается схожим образом. Репозитарий -  https://github.com/zsh-users/zsh-autosuggestions.

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

в `~/.zshrc`

```bash
plugins=( [plugins...] zsh-autosuggestions)
```

## Настройка копирования в буфер обмена Windows

В общем случае возможно копирование содержимого консоли WSL в буфер обмена Windows с помощью встроенной утилиты Windows `clip.exe`:

```bash
echo "Hello" | clip.exe
```

Но, к сожалению, копирование кириллических символов выполняется не корректно - со сбоем кодировки. Поэтому лучше использовать другую утилиту, не имеющую такой проблемы: `win32yanc.exe`. Её можно получить из репозитория на гитхабе https://github.com/equalsraf/win32yank/.

После скачивания, необходимо переместить исполняемый файл в любую директорию Windows находящуюся в переменной `Path`, например `C:\WINDOWS\System32`. С этого момента станет доступна операция копирования в буфер обмена Windows включая кириллические символы

```bash
echo "Привет" | win32yank.exe
```

В Linux для выполнения такой операция служит утилита `pbcopy`, поэтому для удобства добавим алиас для этой команды в шелл. 

```bash
#~.zshrc
[...]
alias pbcopy="win32yank.exe -i"
```

> Получить содержимое буфера обмена в консоль можно командой `win32yank.exe -o`
>
> Также можно создать алиас:
>
> ```bash
> #~.zshrc
> [...]
> alias pbpaste="win32yank.exe -o"
> ```

## Установка и настройка утилит

```bash
# Сначала обновление репозитория
sudo apt update

# Установим базовый набор утилит
sudo apt install -y zip unzip curl wget tmux gpg pass gcc bsdmainutils fzf ripgrep 
sudo apt install -y htop btop bat fastfetch micro mc eza duf fd-find
# Создадим ссылку для запуска bat (без неё не будет работать)
sudo ln -s $(which batcat) /usr/local/bin/bat

# Установим git
sudo apt install -y git
# Добавим псевдоним
git config --global alias.st status
# Установим личные данные
git config --global user.name "Grigorii Evseev"
git config --global user.email "grigorii.evseev@outlook.com"
# Исправим проблему с кодировкой
git config --global core.quotepath off
```

> Чтобы убрать фон у редактора `micro` необходимо после его запуска нажать `Ctrl + E` и в появившейся командной строке написать `set colorscheme solarized` (или выбрать другую тему без фона, для чего после `set colorscheme` поставить пробел и нажать `Tab`, затем с помощью `Tab` выбрать необходимую тему). Настройки автоматически сохранятся в файл `~/.config/micro/settings.json`.

> Чтобы установить плагин для управления файлами, нужно нажать `Ctrl + E` и в командной строке написать `plugin install filemanager`. Открыть плагин можно командой `tree` в командной консоли редактора.

Добавление алиасов в шелл (`~/.zshrc`):

```bash
if [ -x "$(command -v eza)" ]; then
	alias ls="eza -l -F --header --icons"
	alias la="eza -l -F --header --icons -a -g"
	alias tree="eza -l -F --header --icons -a -g -T"
	alias lg="eza -l -F --header --icons -a -g -T --git --git-repos --git-ignore"
fi

alias cat="bat"
alias df="duf"
alias m="micro"
alias open="explorer.exe ."
alias explorer="explorer.exe"
alias find="fdfind"
```

После добавления алиасов необходимо перезагрузить консоль `exec zsh`.
