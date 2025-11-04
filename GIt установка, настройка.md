# Установка и настройка Git в Linux, WSL и Windows.

Опустим рассуждения о том зачем нужен Git и чем он хорош. Придерживаясь формата без отлагательств приступим к установке и настройке.

> Клиентов этой системы значительно больше чем один. Существуют даже полноценные GUI версии, например "Github Desktop" от самих github.com. Я рассмотрю только консольные версии.

## Установка

### Windows

Здесь я использую максимально дефолтный клиент,  который можно взять по адресу https://git-scm.com/install/windows. Скачиваем подходящую для нашей системе версию (x64/Arm64) и устанавливаем как обычное приложение. При установке можно оставлять все рекомендуемые опции.

Есть возможность установить это приложение с помощью `winget tool`:

```cmd
winget install --id Git.Git -e --source winget
```

### Linux, WSL

Установка в этих системах тривиальна:

```bash
sudo apt install -y git
```

> Более подробно про установку в различных дистрибутивах можно почитать здесь: https://git-scm.com/install/linux

## Базовая настройка

Под базовой настройкой я подразумеваю установку своего имени, адреса почты, псевдонимов и исправление бага с кириллицей.

```bash
# Установим личные данные
git config --global user.name "My Name"
git config --global user.email "my@email.com"

# Добавим псевдонимы (не обязательно)
git config --global alias.st status
git config --global alias.ps push
git config --global alias.cm commit
git config --global alias.cl clone

# Исправим проблему с кодировкой (обязательно для WSL)
git config --global core.quotepath off

# Имя главной ветки по умолчанию
git config --global init.defaultBranch main
```

Проверим работоспособность:

![image-20251105032401039](./attach/image-20251105032401039.png)







https://eu-digital.ru/articles/bitriks-virtualnaya-mashina/git-bez-parolya-polnoe-rukovodstvo-po-nastroyke-ssh-klyuchey/



https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account?platform=linux&tool=cli



https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent



https://git-scm.com/book/ru/v2/Git-%d0%bd%d0%b0-%d1%81%d0%b5%d1%80%d0%b2%d0%b5%d1%80%d0%b5-%d0%93%d0%b5%d0%bd%d0%b5%d1%80%d0%b0%d1%86%d0%b8%d1%8f-%d0%be%d1%82%d0%ba%d1%80%d1%8b%d1%82%d0%be%d0%b3%d0%be-SSH-%d0%ba%d0%bb%d1%8e%d1%87%d0%b0#r_generate_ssh_key



https://docs.github.com/ru/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys



#

git remote set-url origin git@github.com:gregory-evans/dev-notes.git
