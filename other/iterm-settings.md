# Настройки для iTerm2
!!! Актуально для MacOS.

## Оболочка
Использую терминал с оболочкой [Oh My Zsh](https://ohmyz.sh). Скачать можно по ссылуке с сайта или из репозитория: https://github.com/ohmyzsh/ohmyzsh

## Настройки темы
Мне приятны 2 темы: [agnoster](https://github.com/agnoster/agnoster-zsh-theme) и [cobalt2](https://github.com/wesbos/Cobalt2-iterm)

## cobalt2 
Достаточно понятная настройка есть в описании репозитория: https://github.com/wesbos/Cobalt2-iterm

## agnoster
Идём в репозиторий: https://github.com/agnoster/agnoster-zsh-theme - и скачиваем оттуда файл с темой agnoster.zsh-theme

Копируем файл в папку с темами используемой оболочки: `~/.oh-my-zsh/themes`\
При необходимости заменяем файл.

Открываем файл настроек оболочки `~/.zshrc` текстовым редактором, находим параметр ZSH_THEME и изменяем название темы на "agnoster".\
`ZSH_THEME="agnoster"`

Идём в репозиторий и скачиваем цветовую схему https://github.com/altercation/solarized/tree/master/iterm2-colors-solarized

Далее идём в настройки iTerm2 (`Preferences - Profiles - Colors`) и в правом нижнем углу выбираем из выпадающего списка либо стандартную цветовую схему Solarized Dark, либо Import... и импортируем скачанную цветовую схему из репозитория выше.\
Переходим на вкладку `Text` и в меню `Font` и `Non-ASCII Font` изменяем шрифт на Meslo LG L DZ for Powerline или Menlo.

Готово!

Для проверки шрифтов в терминале запустить команду: 
```sh
echo "\ue0b0 \u00b1 \ue0a0 \u27a6 \u2718 \u26a1 \u2699"
```

Если не хватает шрифтов, то их можно поставить из репозитория https://github.com/powerline/fonts
```sh
git clone https://github.com/powerline/fonts.git
cd fonts
./install.sh

cd ..
rm -rf fonts
```
