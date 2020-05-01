# Herbstluftwm
### Minimal setup

## Installed apps
* archlinux-keyring
* rust
* go
* nodejs
* npm 
* pip
* brightnessctl (control screenbrightness from cli)
* slack
* weechat (terminal irc client) 
	- https://github.com/wee-slack/wee-slack
* neovim (terminal text/code editor)
	- https://github.com/junegunn/vim-plug
  - once nvim has been installed and configured open nvim
  - and run `:checkhealth`
  - https://github.com/neoclide/coc.nvim/wiki/Install-coc.nvim
* ZSH plugins
	- https://github.com/shibumi/hikari-zsh
	- https://github.com/zdharma/fast-syntax-highlighting
* lf (terminal file manager)
	- aur/python-pdftotext
	- chafa
	- odttotext
	- atool
	- w3m
	- mpv
	- mediainfo
* qutebrowser (vim based web browser)
* firefox (web browser)
* slock (Screen locker)
* st (default terminal)
* termite (terminal)
* skim - (fuzzy finder written in rust)
* bat - (like cat but with syntax highlighting)
* dmenu (minimal menu to search and open apps)
* rg - (blazing fast grep alternative, written in rust)
* Fonts
  - community/ttf-font-awesome
  - aur/ttf-font-awesome-4
  - community/awesome-terminal-fonts
  - ttf-material-design-icons-git
  - noto-fonts noto-fonts-cjk noto-fonts-emoji noto-fonts-extra
  - aur/nerd-fonts-complete (I think this contains everything)
    - ```sh
        $ cd ~/Downloads (you need ~4GB of space to build)
        $ yay --getpkgbuild nerd-fonts-complete
        $ cd nerd-fonts-complete
        $ wget -O nerd-fonts-2.1.0.tar.gz https://github.com/ryanoasis/nerd-fonts/archive/v2.1.0.tar.gz
        $ makepkg -sci BUILDDIR=.
      ```
  - aur/sanskrit-fonts
  - aur - ttf-ancient-fonts
  - aur - ttf-fira-code
  - aur - ttf-inconsolata
  - aur - ttf-google-fonts-git ?
  - adobe-source-han-sans-otc-fonts ?
  - adobe-source-han-serif-otc-fonts ?
  - aur/ttf-tw ?
* gotop
* htop
* zathura - (Zathura is a highly customizable and functional document viewer)
	- zathura-pdf-mupdf-0.3.5-2
	- zathura
* audio
	- pulseaudio 
	- pulseaudio-alsa
	- alsa-utils ( provides alsamixer [tui volumecontrol] and alsamixer)
	- alsa-plugins
	- pulsemixer (tui volumecontrol center)
		https://github.com/GeorgeFilipkin/pulsemixer 
  - pavucontrol (graphical volume control center)
* feh (set bacground)
* arandr
* rsync
* zip
* unzip
* lsof
* jq  (json text viewer)
* youtube-dl
* youtube-viewer
* mpv slack(cil media player)
* acpi (client for battery, power, and thermal readings)
* imagemagick (cli image manipulation)
* sysbench (bench markin tool)
* sxiv (image/gif viewer)
* xclip (copy util)
* calibre (ebook reader and converter)
* libreoffice
   - contains `ebook-convert` cli tools
* npm i tldr -g (simplified man pages)
* pip install mdv --user (Terminal Markdown viewer)
* pip install grip --user (Markdown viewer)
* diff-so-fancy
  - Add config once installed https://github.com/so-fancy/diff-so-fancy
* mpd
* ncmpcpp
  - https://computingforgeeks.com/how-to-configure-mpd-and-ncmpcpp-on-linux/
    (configure mpd and ncmpcpp)
* redshift (eye protection)
  - https://www.maketecheasier.com/protect-eyes-redshift-linux/
* simple-mtpfs (mount andriod device)
* nvidia-dkms nvidia-lts nvidia-settings nvidia-utils lib32-nvidia-utils (graphics driver)
* optimus-manager [aur](switch between onboard graphics and gpu)
* lightdm (display manager)
* lightdm-slick-greeter [aur](lightdm greeter)
* i7z (CPU reporting tool)
* cpupower (CPU frequency scaling)
* thermald [aur] (prevent the overheating of platforms)(thermald.service, which should be started and enabled)
* acpid (delivering ACPI events)
* powertop (monitor processes and show which of them are utilizing the CPU )
* 3.) Run powertop install the "powertop" package and run powertop as root. this tool well make recommendations on what power settings to enable on you're system it will even enable them for you temporally untill next boot and it will give you an idea how cool you can get you're system. After reading up and trying many options I've ended up getting around 5-6 hours of battery life and running almost dead cold X3
* i8kutils[aur](manual fan control)
* crystal (programming language)
* shards (crystal package manager)
* gopass (cli password manager)
* adb (andriod flashing tool)
* zenity (vim colour picker dependecies)
* gucharmap (gnome character map, view fonts and icons)

# Extra
## Set qutebrowser as default
`xdg-settings set default-web-browser org.qutebrowser.qutebrowser.desktop`

## Switch off bluetooth from starting automatically
`systemctl status bluetooth.target`

## NVIM
```
once nvim has been installed and configured open nvim
and run :checkhealth
https://github.com/neoclide/coc.nvim/wiki/Install-coc.nvim
```

## Arch linux switching kernals with systemd boot
- https://bbs.archlinux.org/viewtopic.php?id=235116
 
## Arch linux dell inspiron nvme - install guide
- https://gist.github.com/binaerbaum/535884a7f5b8a8697557

 
# Powertop 
## Automatically tune power saving settings
https://wiki.archlinux.org/index.php/Powertop#Usage

`sudo powertop --auto-tune`
You can use the `--auto-tune` feature from powertop which sets all tunable options to their GOOD setting. This can be combined with systemd service to have the tunables set on boot. Remember to enable/start the service.

`/etc/systemd/system/powertop.service`
```sh
[Unit]
Description=Powertop tunings

[Service]
Type=exec
ExecStart=/usr/bin/powertop --auto-tune
RemainAfterExit=true

[Install]
WantedBy=multi-user.target
```

## Manually tune power saving settings
https://dabase.com/blog/2013/Systemd_powertop_tunables/
https://wiki.archlinux.org/index.php/Powertop
https://wiki.archlinux.org/index.php/Power_management#Power_saving


1. Open powertop and press `tab` and look at the tunables
```sh
sudo powertop
```

2. Save tunables to html
```sh
sudo powertop -r power_report.html
```

3. Extract the tunable settings from the html
```sh
awk -F '</?td ?>' '/tune/ { print $4 }' power_report.html > tunables.txt
```

4. Remove any new lines from `tunables.txt`

5. Save the following code as `rewrite.sh` scipt in the same dir
```sh
cleanup() {
    echo $1 | tr -d "';"
}
while read _ arg _ dev
do
    echo w $(cleanup $dev) - - - - $(cleanup $arg)
done < tunables.txt
```

6. Convert the tunables into systemd format config

```sh
bash rewrite.sh > /tmp/power-savings.conf
```

6. Open the file `/tmp/power-savings.conf` and make sure it looks ok

It should look something like this now:
```sh
w /sys/class/scsi_host/host0/link_power_management_policy - - - - min_power
w /proc/sys/kernel/nmi_watchdog - - - - 0
w /proc/sys/vm/dirty_writeback_centisecs - - - - 1500
w /sys/module/snd_hda_intel/parameters/power_save - - - - 1
w /sys/bus/usb/devices/3-1/power/control - - - - auto
w /sys/bus/pci/devices/0000:0e:00.0/power/control - - - - auto
```

7. Move it to the right place
```sh
sudo mv /tmp/power-savings.conf /etc/tmpfiles.d/power-savings.conf
```

8. Reboot

9. Chech that there are no bad rules
```sh
  sudo powertop
```


## Preview
![alt text](wm-preview.png "herbstluftwm")

