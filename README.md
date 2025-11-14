<picture>
   <img alt="Preview of Arch Ascii Art Plymouth Theme" src="https://github.com/tn3w/plymouth-theme-arch-ascii/releases/download/img/preview.png"></img>
</picture>

<h2 align="center">Plymouth Theme: Arch Ascii Art</h2>
<p align="center">Arch Ascii Art is a <strong>Plymouth theme</strong> featuring a centered <strong>rainbow-colored Arch Linux ASCII art</strong> logo with password input functionality.</p>

Quick Install (if Plymouth is already installed and configured):

```bash
yay -S plymouth-theme-arch-ascii
sudo plymouth-set-default-theme arch-ascii-art
sudo mkinitcpio -P
```

## Features

- **Rainbow Arch ASCII Art**: The iconic Arch Linux logo displayed in rainbow colors (red, orange, yellow, green, blue, purple)
- **Centered Layout**: ASCII art is perfectly centered on the screen
- **Password Input**: Real password input field with bullet characters for encryption passphrases
- **Encryption Focus**: Specifically designed for disk encryption unlock screens

## 🚀 Installation

**Prerequisites:**

1. Install Plymouth:
    ```bash
    sudo pacman -S plymouth
    ```
2. Configure mkinitcpio hooks for LUKS with Plymouth:

    DIY: Open `/etc/mkinitcpio.conf`, `plymouth` must be placed after `base udev` and before `encrypt` in the HOOKS array to display the boot splash during LUKS decryption.

    Command:

    ```bash
    sudo sed -i '/^HOOKS=/ {/plymouth/! s/udev/udev plymouth/}' /etc/mkinitcpio.conf
    ```

3. Configure GRUB for Plymouth:

    DIY: Open `/etc/default/grub`, add `splash` to the `GRUB_CMDLINE_LINUX_DEFAULT` line.

    Command:

    ```bash
    sudo sed -i '/^GRUB_CMDLINE_LINUX_DEFAULT=/ {/splash/! s/"$/ splash"/}' /etc/default/grub
    sudo grub-mkconfig -o /boot/grub/grub.cfg
    ```

4. Rebuild initramfs:
    ```bash
    sudo mkinitcpio -P
    ```

**A. Use AUR helpers**

1. Install with an AUR helper (e.g. yay, paru):

```bash
yay -S plymouth-theme-arch-ascii

# or install with paru
# paru -S plymouth-theme-arch-ascii
```

2. Set the theme as default:

```bash
sudo plymouth-set-default-theme arch-ascii-art
```

3. Update initramfs:

```bash
sudo mkinitcpio -P
```

**B. Use git**

1. Clone the repository to your machine:

    ```bash
    sudo git clone https://github.com/tn3w/plymouth-theme-arch-ascii.git
    ```

2. Copy the theme directory to Plymouth themes location:

    ```bash
    sudo cp -r plymouth-theme-arch-ascii /usr/share/plymouth/themes/arch-ascii-art
    ```

3. Set the theme as default:

    ```bash
    sudo plymouth-set-default-theme arch-ascii-art
    ```

4. Update initramfs:
    ```bash
    sudo mkinitcpio -P
    ```

## Files

- `arch-ascii-art.script` - Main theme script with rainbow colors and password functionality
- `arch-ascii-art.plymouth` - Theme configuration file
- `PKGBUILD` - Arch Linux package build script for AUR
- `.SRCINFO` - AUR package metadata file
- `LICENSE` - MIT License file
- `README.md` - This documentation

## Color Scheme

The ASCII art uses a rainbow gradient:

- **Red**: Top 3 lines
- **Orange**: Lines 4-6
- **Yellow**: Lines 7-9
- **Green**: Lines 10-13
- **Blue**: Lines 14-16
- **Purple**: Bottom 3 lines

## Usage

This theme will automatically display during:

- System boot (if set as default)
- Disk encryption password prompts
- Other Plymouth-managed system events

The password input appears below the ASCII art with a prompt and bullet characters for each typed character.

## Testing

To test the theme without rebooting:

```bash
sudo plymouthd --debug --debug-file=/tmp/plymouth-debug.log
sudo plymouth --show-splash
sudo plymouth --ask-for-password
sudo plymouth --quit
```

## Compatibility

- Compatible with Plymouth script plugin
- Designed for modern screen resolutions
- Works with all standard Plymouth functionality

## License

MIT License

Copyright (c) 2025 TN3W

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
