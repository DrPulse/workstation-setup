# workstation-setup

Steps and commands after installation to be set and ready in a WSL instance or complete workstation. This repo mainly focus on software and the customization of the shell and prompt.

## Software

These packages are usually in the repositories of the distribution, use the package manager of your liking.
For Debian & Ubuntu derivatives I prefer nala over apt. It's just a front-end to apt, more readable, faster and nicer to use. Feel free to replace nala with apt if you are not using it. [Here is the repository](https://gitlab.com/volian/nala)

```sh
sudo apt install nala
```

### Deb packages

- WSL

```text
bat curl git htop ncdu neofetch nodejs npm python3-pip rsync thefuck tldr vim wget zip fzf
```

- Workstation

```text
bat curl firefox flatpak git gparted gufw htop ncdu neofetch nodejs npm python3-pip rsync software-properties-common timeshift thefuck tldr vim wget zip fzf
```

- Gaming:

### Flatpak packages

- Workstation

```sh
flatpak install flathub io.missioncenter.MissionCenter com.github.tchx84.Flatseal com.visualstudio.code org.onlyoffice.desktopeditors org.videolan.VLC org.filezillaproject.Filezilla com.getpostman.Postman org.kde.krita com.usebottles.bottles com.github.jeromerobert.pdfarranger
```

- Gaming

```sh
flatpak install flathub com.valvesoftware.Steam com.discordapp.Discord com.heroicgameslauncher.hgl net.lutris.Lutris
```

## Shell

<details>
<summary><b>Bash</b></summary>

Installed by default, I don't customize it, just the .bashrc.
</details>

<details>
<summary><b>ZSH</b></summary>

Prefered shell, not using oh-my-zsh. I prefer to include plugins manually in the .zshrc.

### [Installation](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)

1. Installation:
ZSH is available through a lot of package managers (apt, pacman, dnf...) check documentation. For debian based distros :

    ```sh
    sudo nala install zsh
    ```

2. Verify installation by running `zsh --version`
3. Make it the default shell with `chsh -s $(which zsh)` or `sudo lchsh $USER` if the distro is Fedora.
4. Log out and log back in again to use your new default shell.
5. Test that it worked with `echo $SHELL`. Expected result: `/bin/zsh` or similar.
6. Test with `$SHELL --version`. Expected result: 'zsh 5.8' or similar

### Plugins

- [autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)

```sh
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions
echo "source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
```

- [syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

```sh
git clone https://github.com/zsh-users/zsh-syntax-highlighting ~/.zsh/zsh-syntax-highlighting
echo "source ~/.zsh/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
```

- tab completions - add `autoload -Uz compinit && compinit` to your `.zshrc` file

</details>

## Prompt

### Fonts

Usually prompts needs [Nerdfonts](https://www.nerdfonts.com/)

Information about fonts folders :

- `/usr/local/share/fonts/` to install fonts system-wide
- `~/.local/share/fonts/` or `~/.fonts` to install fonts just for the current user

Download with cli:

- `wget "font url"`
- `unzip "zip file" -d ~/.fonts`
- `fc-cache -fv`

Download with gui:

- Download a Nerdfont from the website
- Unzip the file
- Install the font with distro utility or by moving the files in the directortories mentionned in the cli way.

### Prompts

- [Starship](https://starship.rs/)
Prefered prompt, cross shell, only one config in a single file to to.

1. Installation
Starship is available through some package managers (pacman, dnf, brew, nix) and with cargo. Check documentation. Otherwise :

    ```sh
    curl -sS https://starship.rs/install.sh | sh
    ```

2. Shell setup
Starship is usually initialized at the end of a shell configuration.
    - Bash: ```echo 'eval "$(starship init bash)"' >> ~/.bashrc```
    - ZSH : ```echo 'eval "$(starship init zsh)"' >> ~/.zshrc```
    - Others : check the documentation
3. Configuration
Starship uses a single TOML file to store the configuration, create the following firectory and file :

```sh
mkdir -p ~/.config && touch ~/.config/starship.toml
```

Then edit the file according to the documentation or replace it with your own file.

- [Powerlevel10k](https://github.com/romkatv/powerlevel10k)
Faster than Starship but only usable with zsh. Easier to configure through wizard configuration.

powerlevel10k requires the MesloLGS NerdFont in the regular, bold, italic and bold italic variant to work, or the symbols won't work.

1. Installation
powerlevel10k can be installed in many ways like with homebrew, oh my zsh, yay... heck documentation. Otherwise:

```sh
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
source ~/.zshrc
```

The configuration wizard should be triggered. If not, type `p10k configure`. If it still doesn't work, refer to the installation documentation.
2. Configuration

In the wizard, choose the configuration you want and only type digits and never enter, it will skip steps.
The configuration is stored in the `~/.p10k.zsh` file.

The wizard can be re triggered with the command `p10k configure`. It's easier to change the configuration that way, even though you can modify the file, it's quiet long.

## Dotfiles

Dotfiles are niceto have in a dedicated repo. I prefer to use [chezmoi](https://www.chezmoi.io/) to sync them accross workstations.

1. Installation
chezmoi can be installed in many ways like with homebrew, nix, pacman... check documentation. Otherwise there are two ways:.
    - curl : ```sh -c "$(curl -fsLS get.chezmoi.io)"```
    - wget : ```sh -c "$(wget -qO- get.chezmoi.io)"```
Note : If you already have a repository set up, you can append `-- init --apply $GITHUB_USERNAME` to the installation command to pull the files from the repo.

2. Verify the installation
source your shell file and run `chezmoi`. Expected result : chezmoi help page or similar.

3. Chezmoi usage
If you didn't pull files from a repository, run `chezmoi init`

    - add files with `chezmoi add *file*`
    - run `chezmoi cd`
    - add files in git and commit them
    - create a github repository if you didn't and push the files

You can find more informations on my [dotfiles repository](https://github.com/DrPulse/dotfiles)

## DE customization

Depanding on the Desktop Environment, some additional software can be needed to customize it.
<details>
<summary><b>Gnome</b></summary>

### Gnome software

```text
gnome-tweaks gnome-shell-extensions
```

```sh
flatpak install com.mattjakeman.ExtensionManager io.github.realmazharhussain.GdmSettings
```

### Extensions

- [Blur my shell](https://extensions.gnome.org/extension/3193/blur-my-shell/)
- [Caffeine](https://extensions.gnome.org/extension/517/caffeine/)
- GDM Settings - Installed with flatpak
- [Net Speed Simplified](https://extensions.gnome.org/extension/3724/net-speed-simplified/)
- [User Themes](https://extensions.gnome.org/extension/19/user-themes/)
- [Vitals](https://extensions.gnome.org/extension/1460/vitals/)

</details>

<details>
<summary><b>Plasma</b></summary>

</details>
