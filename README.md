# Programs

```bash
sudo mkfs.ext4 -L Hard /dev/sdb

# fish & fastfetch
sudo pacman -S fish fastfetch imagemagick pkgfile ttf-dejavu powerline-fonts inetutils
	chsh
	/bin/fish


# Дефолтные программы
sudo pacman -S steam discord qbittorrent haruna obsidian telegram-desktop openrgb kvantum dolphin
yay -S zen-browser-bin audiorelay onlyoffice-bin qt6ct-kde
yay -S elyprismlauncher-bin betterdiscord-installer millennium
yay -S visual-studio-code-bin android-studio
yay -S proton-vpn-gtk-app portproton

# Утилиты системы:
# hyprpolkitagent — права администратора GUI
# hyprlock — блокировка экрана
# expac — инфа о пакетах pacman
# ncdu — анализ диска
# radeontop — загрузка GPU
# rocm-smi-lib — мониторинг AMD GPU
sudo pacman -S  expac ncdu radeontop rocm-smi-lib

# CLI-утилиты для удобной работы / замены стандартных инструментов:
# lsd — улучшенный ls
# bat — cat с подсветкой
# btop — монитор ресурсов
# zoxide — умная навигация по папкам
# fzf — fuzzy-поиск
# fd — быстрый find
# ripgrep — быстрый поиск по тексту
# lazygit — TUI для git
sudo pacman -S lsd bat btop zoxide fzf fd ripgrep lazygit
	https://www.youtube.com/watch?v=UzWOX7-Tye8

# Инструменты Wayland/Hyprland:
# hyprshot — скриншоты
# hyprpicker — выбор цвета с экрана
# satty — аннотация скринов
# wl-clipboard — буфер обмена Wayland
sudo pacman -S hyprshot hyprpicker satty wl-clipboard wl-clip-persist cliphist

# Распаковка zip
sudo pacman -S unzip

# Управление dotfiles через симлинки
sudo pacman -S stow

# Просмотрщик фото
sudo pacman -S loupe

# Редактор кода
sudo pacman -S nvim
	git clone https://github.com/NvChad/starter ~/.config/nvim && nvim
	# В init.lua
	-- Устанавливаем таймаут для комбинаций (в миллисекундах)  
	vim.o.timeoutlen = 300 -- 300ms для двойного нажатия 'j'  
	-- Маппинг jj в insert mode → Esc  
	vim.keymap.set("i", "jj", "<Esc>", { noremap = true, silent = true })

# Утилита для копирования файлов в облачные хранилища
sudo pacman -S rclone
	systemctl --user start rclone-backup.service
	systemctl --user daemon-reload 
	systemctl --user enable --now rclone-backup.timer

# nodejs npm
sudo pacman -S nodejs npm
	mkdir -p ~/.npm-global  
	npm config set prefix '~/.npm-global'

# Демон обоев (устарел, на смену пришел awww)
sudo pacman -S swww
	chmod +x ~/.config/rofi/scripts/powermenu.sh
	chmod +x ~/.config/rofi/scripts/wallpapermenu.sh 

# Хранение секретов / пароли и ключи
sudo pacman -S gnome-keyring libsecret seahorse
	# Приложения по умолчанию в dolphin
	rm -rf ~/.cache/ksycoca6*
		kbuildsycoca6 --noincremental
		nvim ~/.config/kdeglobals
			[General]
			TerminalApplication=kitty
	# Секреты
	systemctl --user enable --now gnome-keyring-daemon.service
	mkdir -p ~/.vscode 
	vim ~/.vscode/argv.json
	{ "password-store": "gnome-libsecret" }

# Аудиосервер + совместимость / управление звуком / используется всей системой и в GUI (`pavucontrol`)
sudo pacman -S pipewire pipewire-pulse pipewire-alsa pavucontrol

# Bluetooth стек + утилиты + GUI / подключение устройств / используется для BT-девайсов
sudo pacman -S bluez bluez-utils blueman
	sudo systemctl enable --now bluetooth.service

# CLI утилиты KDE / интеграция с KDE (например, `kioclient`) / используется для открытия файлов, URL, интеграции в GUI
sudo pacman -S kde-cli-tools

# Работа с FAT/exFAT / форматирование, проверка флешек / используется при работе с USB-накопителями
sudo pacman -S exfatprogs dosfstools

# Vulkan API + аудио API / разработка и запуск игр/графики / используется играми, эмуляторами
sudo pacman -S vulkan-headers openal

# Polkit агент + локер + портал для sandbox-приложений / доступ к файлам, скриншотам / нужен для Flatpak, браузеров, Hyprland + меню приложений
sudo pacman -S hyprpolkitagent hyprlock xdg-desktop-portal xdg-desktop-portal-hyprland archlinux-xdg-menu

# Просмотр изображений + генерация превью файлов + firewall / превью видео/изображений и фильтрация трафика / файловые менеджеры + сеть + превью файлов + расширения KIO / миниатюры PDF, видео, доп. протоколы (smb, ftp) / файловые менеджеры (Dolphin и др.)
sudo pacman -S tumbler ffmpegthumbnailer nftables kdegraphics-thumbnailers ffmpegthumbs kio-extras

# Qt6 QML + UI компоненты / отрисовка интерфейсов / нужны для Qt/Hyprland приложений, SDDM /usr/share/sddm/themes/pixie/
sudo pacman -S qt6-declarative qt6-svg qt6-quickcontrols2
	git clone https://github.com/xCaptaiN09/pixie-sddm.git
	cd pixie-sddm
	sudo ./install.sh
```

# Установка:

```bash
# Подготовка флешки
lsblk
sudo umount /dev/sdb*
sudo dd if=archlinux.iso of=/dev/sdb bs=4M status=progress oflag=sync
sync

# Подготовка диска
sudo wipefs -a /dev/...  
sudo sgdisk --zap-all /dev/...
sudo pacman -Sy archinstall
archinstall
```

# Настройка системы:
# YAY (AUR)

```bash
sudo pacman -Syu
sudo pacman -S --needed base-devel git
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
cd ..
sudo rm -rf yay
```

# Fonts

```bash
sudo pacman -S ttf-font-awesome otf-font-awesome ttf-jetbrains-mono
sudo pacman -S ttf-jetbrains-mono-nerd
sudo pacman -S ttf-fira-code
sudo pacman -S nerd-fonts-jetbrains-mono
yay -S ttf-ms-fonts
[FiraCode] - (https://github.com/ryanoasis/nerd-fonts/releases/download/v3.4.0/FiraCode.zip) распоковать в /usr/share/fonts
fc-cache -fv
```

# Cursor

```bash
Cursor: Bibata-Modern-Classic - скачиваем с gnome-look, распаковываем и переносим в директорию: /usr/share/icons
sudo cp -r Bibata-Modern-Classic/ /usr/share/icons/
Переходим в /usr/share/icons/ и прописываем команду
hyprctl setcursor "Bibata-Modern-Classic" 28
```

# Theme
```bash 
sudo pacman -S nwg-look
sudo pacman -S papirus-icon-theme
Theme: скачиваем с gnome-look, распаковываем и переносим в директорию: /usr/share/themes, либо через github
```


# RCLONE


```
rice/
└── dotfiles/
    ├── fastfetch/             →  .config/fastfetch
    ├── fish/                  →  .config/fish
    ├── kitty/                 →  .config/kitty
    ├── nvim/                  →  .config/nvim
    ├── rclone/                →  .config/rclone
    ├── BetterDiscord/         →  .config/BetterDiscord
    ├── systemd/               →  .config/systemd
    └── rofi/                  →  .config/rofi
```

**Аккуратно надо быть с systemd и rclone, там нужно будет заново вызвать systemctl --user list-timers --user и раскидать на таймер и прочее**
# Основные команды
Перед первым использованием stow нужно создать правильную структуру пакетов и переместить существующие конфиги из домашней директории в dotfiles. Делается это один раз.

```bash
# 1. Переходим в директорию dotfiles
cd ~/Arch_Hyprland_Dotfiles/dotfiles

# 2. Создаём структуру для каждого пакета
mkdir -p \ 
		 hypr/.config/hypr \
         kitty/.config/kitty \
         btop/.config/btop \
         dunst/.config/dunst \
         fastfetch/.config/fastfetch \
         fish/.config/fish \
         Kvantum/.config/Kvantum \
         nvim/.config/nvim \
         nwg-look/.config/nwg-look \
         OpenRGB/.config/OpenRGB \
         qt6ct/.config/qt6ct \
         rclone/.config/rclone \
         rofi/.config/rofi \
         systemd/.config/systemd \
         waybar/.config/waybar

# 3. Перемещаем существующие конфиги из ~/.config в пакеты
mv ~/.config/kitty/*    kitty/.config/kitty

for dir in hypr kitty btop dunst fastfetch fish Kvantum nvim nwg-look OpenRGB qt6ct rclone rofi systemd waybar
        set files ~/.config/$dir/* ~/.config/$dir/.*
        if test -e ~/.config/$dir
            mv $files $dir/.config/$dir 2>/dev/null
        end
    end

# 4. Удаляем остатки старых папок в домашней директории (на всякий случай)
for dir in hypr kitty btop dunst fastfetch fish Kvantum nvim nwg-look OpenRGB qt6ct rclone rofi systemd waybar
    rm -rf ~/.config/$dir
end

# Установить один пакет (создаёт симлинки)
stow hypr kitty btop dunst fastfetch fish Kvantum nvim nwg-look OpenRGB qt6ct rclone rofi systemd waybar -t ~
# Удалить симлинки одного пакета
stow -D kitty -t ~

# Безопасное обновление после git pull
stow -R */ -t ~
```

# Быстрый откат (если что-то сломалось)

```bash
# Для конкретного пакета
rm -rf ~/.config/kitty
stow -D kitty -t ~
stow kitty -t ~
```














