# Programs

```bash
# Метка для диска
sudo mkfs.ext4 -L Hard /dev/sdb

# fish & fastfetch
sudo pacman -S fish fastfetch imagemagick pkgfile ttf-dejavu powerline-fonts inetutils
	chsh
	/bin/fish

# Терминальный проводник
sudo pacman -S yazi unarchiver
	# Плагины ставятся через менджер ya pack
	ya pkg add yazi-rs/plugins:git
		# Настройка плагина
		# ~/.config/yazi/init.lua
		require("git"):setup {
		-- Order of status signs showing in the linemode
		order = 1500,
		}
		
		# Подключение fetchers (обязательно)
		# ~/.config/yazi/yazi.toml
		[[plugin.prepend_fetchers]]
		id  = "git"
		url = "*"
		run = "git"
		
		[[plugin.prepend_fetchers]]
		id  = "git"
		url = "*/"
		run = "git"
	
	ya pkg add yazi-rs/plugins:full-border
		# Настройка плагина
		# ~/.config/yazi/init.lua
		require("full-border"):setup {
		-- Available values: ui.Border.PLAIN, ui.Border.ROUNDED
		type = ui.Border.ROUNDED,
	
	# Не работает этот плагин
	ya pkg add yazi-rs/plugins:zoom
		# Настройка плагина
		# ~/.config/yazi/init.lua
		
		
		# ~/.config/yazi/yazi.toml
		[[mgr.prepend_keymap]]
		on   = "+"
		run  = "plugin zoom 1"
		desc = "Zoom in hovered file"
		
		[[mgr.prepend_keymap]]
		on   = "-"
		run  = "plugin zoom -1"
		desc = "Zoom out hovered file"
		}




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
# ntfs-3g — форматирование в NTFS
# ark - просмотрщик архивов
sudo pacman -S  expac ncdu radeontop rocm-smi-lib ntfs-3g ark

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


# Скрытие программ из rofi
```bash
# Сначала найди нужный .desktop-файл
# .desktop лежит в /usr/share/applications/, сначала скопируй его в свою пользовательскую папку командой ниже так ты создашь переопределение, которое rofi будет читать в первую очередь, а оригинал останется нетронутым.
cp /usr/share/applications/имя.desktop ~/.local/share/applications/ 
# Теперь открой этот файл в любом редакторе
nvim ~/.local/share/applications/имя_файла.desktop
# Найди в самом начале секцию [Desktop Entry] и добавь туда новую строку:
NoDisplay=true
# Сохрани файл и сразу обнови базу desktop-файлов командой
update-desktop-database ~/.local/share/applications
rm -rf ~/.cache/rofi*
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
