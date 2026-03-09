# arch-hyprland-rice

Мои конфиги для Hyprland + Waybar + Fish + Kitty + Fastfetch + Rofi  
Управляются через GNU Stow

## Структура
```
arch-hyprland-rice/
└── dotfiles/
    ├── fastfetch/     →  .config/fastfetch
    ├── fish/          →  .config/fish
    ├── hypr/          →  .config/hypr
    ├── kitty/         →  .config/kitty
    ├── rofi/          →  .config/rofi
    └── waybar/        →  .config/waybar
```

# Основные команды

## Подготовка пакетов (один раз при первом переносе)

Перед первым использованием stow нужно создать правильную структуру пакетов и переместить существующие конфиги из домашней директории в dotfiles. Делается это один раз.

```bash
# 1. Переходим в директорию dotfiles
cd ~/arch-hyprland-rice/dotfiles

# 2. Создаём структуру для каждого пакета
# (mkdir -p создаёт все вложенные директории сразу)
mkdir -p hypr/.config/hypr
mkdir -p waybar/.config/waybar
mkdir -p fish/.config/fish
mkdir -p kitty/.config/kitty
mkdir -p rofi/.config/rofi
mkdir -p fastfetch/.config/fastfetch

# 3. Перемещаем существующие конфиги из ~/.config в пакеты
# Если какой-то папки уже нет — команда просто выдаст ошибку, это нормально
mv ~/.config/hypr    hypr/.config/hypr
mv ~/.config/waybar  waybar/.config/waybar
mv ~/.config/fish    fish/.config/fish
mv ~/.config/kitty   kitty/.config/kitty
mv ~/.config/rofi    rofi/.config/rofi
mv ~/.config/fastfetch fastfetch/.config/fastfetch

# 4. Удаляем остатки старых папок в домашней директории (на всякий случай)
rm -rf ~/.config/{hypr,waybar,fish,kitty,rofi,fastfetch}
```

```bash
# Перейти в директорию dotfiles
cd ~/arch-hyprland-rice/dotfiles

# Перенести конфиг в 

# Установить один пакет (создаёт симлинки)
stow hypr -t ~
stow waybar -t ~
stow fish -t ~
stow kitty -t ~
stow rofi -t ~
stow fastfetch -t ~

# Удалить симлинки одного пакета
stow -D hypr -t ~

# Безопасное обновление после git pull
stow -R */ -t ~
```

## Быстрый откат (если что-то сломалось)

```bash
# Для конкретного пакета
rm -rf ~/.config/hypr
stow -D hypr -t ~
stow hypr -t ~
```
## Списки установленных пакетов

В папке `packages/` хранятся актуальные списки всех установленных программ.

```bash
packages/
├── explicitly-installed.txt    # pacman -Qqe → явно установленные из официальных репозиториев
└── aur.txt                     # yay -Qqm     → пакеты из AUR
```

Обновление списков
После установки или удаления пакетов:

```bash
cd ~/arch-hyprland-rice/packages
pacman -Qqe | sort > explicitly-installed.txt
yay -Qqm   | sort > aur.txt
git add .
git commit -m "Обновлены списки пакетов"
```

Восстановление системы на чистой Arch

```bash
# 1. Установить официальные пакеты
sudo pacman -S --needed $(cat ~/arch-hyprland-rice/packages/explicitly-installed.txt)

# 2. Установить AUR-пакеты (сначала yay должен быть установлен)
yay -S --needed $(cat ~/arch-hyprland-rice/packages/aur.txt)
```

