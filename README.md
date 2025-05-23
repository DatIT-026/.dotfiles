# How to customize your Linux Mint (Sway)

## Linux Installation
Install Linux on your computer. If you are new here, I recommended you to use [Linux Mint](https://linuxmint.com/download.php). 

## Setup sway
To install [sway](https://wiki.archlinux.org/title/Sway):
```
sudo apt update
sudo apt install sway
```
If you are using NVDIA card, change to `Exec=sway --unsupported-gpu` in `/usr/share/wayland-sessions/sway.desktop`.

## Initial Setup ([~/.config/sway/config](https://github.com/DatIT-026/.dotfiles/blob/7c909ba9b74543761accd89f754b99f7c10b3aa4/sway/config))
- Kitty installation
  ```
  sudo apt install kitty
  Kitty +kitten themes
  ```
  and find and replace to become the code below in `~/.config/sway/config`:
  ```
  Bindsym $mod+Return exec kitty
  ```
  To make the cursor shape, add this in `~/.config/kitty/kitty.conf `:
  ```
  cursor_shape block
  ```
- For Wallpaper setup, install `swaybg`:
  ```
  sudo apt install swaybg
  ```
  add it to `~/.config/sway/config` if you don't have it:
  ```output * bg ~/Pictures/me2.jpg fill```

- For brightnessctl keybind setup:
  ```
  sudo apt install brightnesstcl
  sudo usermod -aG video your_username
  ```
  Then add this keybind to use `Fn + f5`, `Fn + f6` key in `~/.config/sway/config`:
  ```
  bindsym XF86MonBrightnessDown exec brightnessctl set 5%-
  bindsym XF86MonBrightnessUp exec brightnessctl set 5%+
  ```
  
## Setup your waybar ([~/.config/waybar/config](https://github.com/DatIT-026/.dotfiles/blob/45199d81e42283f6a230838ceb10d78e7814d45f/waybar/config) and [~/.config/waybar/style.css](https://github.com/DatIT-026/.dotfiles/blob/ffd9354b3f1b491ef9c7cb919489d2a249a2d4a9/waybar/style.css))
1. Install waybar:
   ```
   sudo apt install waybar
   ```
   Add my config to `~/.config/waybar/config`.
3. Font installation ([here](https://www.nerdfonts.com/font-downloads)):
- Unzip and try this:
  ```
  mkdir -p ~/.local/share/fonts
  cp path_to_downloaded_fonts/*.otf ~/.local/share/fonts/
  ```
  For example: `unzip JetBrainsMono.zip -d ~/.local/share/fonts/` && `unzip ~/Downloads/FiraCode.zip -d ~/.local/share/fonts/`
  
- Update cache fonts:
  ```
  fc-cache -fv
  ```
  
## Fastfetch is perfect
1. Install prerequisite if needed:
   ```
   sudo apt install software-properties-common
   ```
2. Add the Fastfetch PPA:
   ```
   sudo add-apt-repository ppa:fastfetch/stable
   ```
3. Update package lists & Install Fastfetch:
   ```
   sudo apt update
   sudo apt install fastfetch
   ```
4. Verify installation by running: `fastfetch`

To customize the ASCII art logo in fastfetch, try this:
1. Preparing a file, for example in my repo: [`me.txt`](https://github.com/DatIT-026/.dotfiles/blob/e5dc35be66362a01108ce516d10a0bd962217056/Documents/me.txt).
2. Try this code:
```
fastfetch --logo-color-1 red --logo-color-2 yellow --color cyan
```
3. Fastfetch configuration:
  Try this code:
  ```
  fastfetch --gen-config > ~/.config/fastfetch/config.jsonc
  ```
  and then paste your config to this `~/.config/fastfetch/config.jsonc`. For example:
   ```
     {
    "$schema": "https://github.com/fastfetch-cli/fastfetch/raw/dev/doc/json_schema.json",
  
    "logo": {
      "source": "/home/datto/Documents/me.txt",
      "color": {
        "1": "cyan"
      }
    },
  
    "display": {
      "color": "cyan"
    },
  
    "modules": [
        "title",
        "separator",
        "os",
        "host",
        "kernel",
        "uptime",
        "packages",
        "shell",
        "display",
        "de",
        "wm",
        "wmtheme",
        "theme",
        "icons",
        "font",
        "cursor",
        "terminal",
        "terminalfont",
        "cpu",
        "gpu",
        "memory",
        "swap",
        "disk",
        "localip",
        "battery",
        "poweradapter",
        "locale",
        "break",
        "colors"
      ]
    }
  ```

## Also try yazi
First, install Rust & some tools:
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
rustup update
sudo apt update
sudo apt install build-essential pkg-config libssl-dev
```

Next, clone repo Yazi from Github:
```
git clone https://github.com/sxyazi/yazi.git
cd yazi
```
Build & install Yazi:
```
# yazi-fm (file manager)
cargo install --path yazi-fm --locked

# yazi-cli (CLI)
cargo install --path yazi-cli --locked
```

Add Yazi to PATH:
```
export PATH="$HOME/.cargo/bin:$PATH"
source ~/.bashrc
```
Check version:
```
yazi --version
ya --version
```
Also try yazi with [helix](https://helix-editor.com/) in `~/.config/yazi/yazi.toml`:
```
[manager]
show_hidden = true
sort_by = "alphabetical"
sort_dir_first = true
[opener]
edit = [
  { run = 'hx "$@"', block = true },
]`
```
