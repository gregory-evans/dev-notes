## Установка ZShell

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

## Plugins

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

Установка плагина авто дополнений выполняется схожим образом. 
Репозитарий -  https://github.com/zsh-users/zsh-autosuggestions.

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

в `~/.zshrc`

```bash
plugins=( [plugins...] zsh-autosuggestions)
```
