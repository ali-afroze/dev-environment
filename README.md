<span style="font-size: 32px; font-weight: bold; background-color: #2EC0F9; color: #fff; padding: 10px; border-radius: 2px; width: 100%; display: block; text-align: center;">💻 Dev Environment and Tools</span>
This reposiory contains all my terminal configurations, IDE configurations, and other tools that I use to develop. I am planning to add instructions for Mac, Windows, and Linux. This `Readme.md` will be a step by step guide on building a development environment from scratch.

<span style="font-size: 28px; font-weight: bold; background-color: #E36397; color: #fff; padding: 10px; border-radius: 2px; width: 100%; display: block; text-align: center;">🖥️ For Mac</span>
This setup uses `wezterm` as terminal emulator, and `zsh` as shell and `cursor` as IDE. Cursor takes and runs with settings of VSCode. So cutomizing VSCode lets us use it with cursor.

<div style="padding: 10px 0px;"></div>
<div style="font-size: 24px; font-weight: regular; width: fit-content; background-color: #E36397; color: #fff; padding: 8px 32px; display: flex; gap: 10px; align-items: center; border-radius: 2px; text-align: center;">
<svg fill="none" height="24" viewBox="0 0 64 64" width="24" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" id="fi_10792828"><linearGradient id="paint0_linear_1798_2685" gradientUnits="userSpaceOnUse" x1="78.644" x2="25.425" y1="74.123" y2="11.863"><stop offset=".00265844" stop-color="#ff37df"></stop><stop offset="1" stop-color="#6e00ff"></stop></linearGradient><path clip-rule="evenodd" d="m18 2c-8.83656 0-16 7.16344-16 16v28c0 8.8366 7.16344 16 16 16h28c8.8366 0 16-7.1634 16-16v-28c0-8.83656-7.1634-16-16-16zm10 30c0 .567-.2406 1.1073-.6621 1.4866l-10 9c-.821.7389-2.0856.6724-2.8245-.1487-.7389-.821-.6723-2.0856.1487-2.8245l8.3482-7.5134-8.3482-7.5134c-.821-.7389-.8876-2.0035-.1487-2.8245s2.0035-.8876 2.8245-.1487l10 9c.4215.3793.6621.9196.6621 1.4866zm20 11c1.1046 0 2-.8954 2-2s-.8954-2-2-2h-16c-1.1046 0-2 .8954-2 2s.8954 2 2 2z" fill="url(#paint0_linear_1798_2685)" fill-rule="evenodd"></path>
</svg>  
Terminal
</div>
<div style="padding: 10px 0px;"></div>

Wezterm is cross platform terminal emulator written in Rust. The configuration language is `lua`, which make it easier to configure and extend. Wezterm support built in terminal split, which is a game changer. This works really good with `zsh` as it the default shell for mac.

#### Open The Terminal App
Open the default terminal app on macOs.
This setup is specifically for zsh (default) so make sure you are using that.
You can check by doing:
```sh
echo $0
```
You can change to zsh if you have it installed by doing:
```sh
chsh -s /bin/zsh
```
#### Install homebrew
Run the following command:
```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
If necessary, when prompted, enter your password here and press enter. If you haven’t installed the XCode Command Line Tools, when prompted, press enter and homebrew will install this as well.

#### Add To Path (Only Apple Silicon Macbooks)

After installing, add it to the path. This step shouldn’t be necessary on Intel macs.
Run the following command to add the necessary line to `~/.zprofile`:
```sh
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
```
Now source `~/.zprofile` by doing:
```sh
source ~/.zprofile
```
#### Install Wezterm
Run the following command:
```sh
brew install --cask wezterm
```
#### Install Meslo Nerd Font
Run the following command:
```sh
brew install font-meslo-lg-nerd-font
```
#### Setup Wezterm Config File
Next we’ll setup the `~/.wezterm.lua` configuration file to configure Wezterm. This file is written in lua.

First create the config file:
```sh
touch ~/.wezterm.lua
```
Then open it with your editor of choice. I use Neovim, but you can use whatever you prefer.
```sh
nvim ~/.wezterm.lua
```
Or TextEdit:
```sh
open -a TextEdit ~/.wezterm.lua
```
#### Add the configuration to `~/.wezterm.lua`
```lua
-- Pull in the wezterm API
local wezterm = require("wezterm")

-- This will hold the configuration.
local config = wezterm.config_builder()

-- This is where you actually apply your config choices

config.font = wezterm.font("MesloLGS Nerd Font Mono")
config.font_size = 19

config.enable_tab_bar = false

config.window_decorations = "RESIZE"

config.window_background_opacity = 0.8
config.macos_window_background_blur = 10

-- and finally, return the configuration to wezterm
return config
```
#### Choose a colorscheme
Take a look at the available colorschemes [here](https://wezfurlong.org/wezterm/colorschemes/index.html).
Once you find one you like, you can select a colorscheme for wezterm like so (the highlighted line below):
```lua
config.color_scheme = "Batman"
```
#### Setup custom colors
```lua
-- colorscheme:
config.colors = {
	foreground = "#CBE0F0",
	background = "#011423",
	cursor_bg = "#47FF9C",
	cursor_border = "#47FF9C",
	cursor_fg = "#011423",
	selection_bg = "#033259",
	selection_fg = "#CBE0F0",
	ansi = { "#214969", "#E52E2E", "#44FFB1", "#FFE073", "#0FC5ED", "#a277ff", "#24EAF7", "#24EAF7" },
	brights = { "#214969", "#E52E2E", "#44FFB1", "#FFE073", "#A277FF", "#a277ff", "#24EAF7", "#24EAF7" },
}
```
Save this file and go back to the command line.

#### Install powerlevel10k theme
[Powerlevel10k](https://github.com/romkatv/powerlevel10k) is an awesome theme for zsh.
Install it using: 
```sh
brew install powerlevel10k
```
Then run the command:
```sh
echo "source $(brew --prefix)/share/powerlevel10k/powerlevel10k.zsh-theme" >> ~/.zshrc
```
This will add what you need to `~/.zshrc` to enable it.
Now source `~/.zshrc`:
```sh
source ~/.zshrc
```
The powerlevel10k configuration wizard should show up now.

If you want to open the wizard manually do: p10k configure.

Answer the prompts to make the theme look like you would like it to. For the colors of my coolnight theme to work use either lean (with the 8 colors option) or rainbow.

Save this file and go back to the command line.

#### Fix directory background color (only for p10k rainbow style)
If you’re using the rainbow version of powerlevel10k, I recommend you change the directory background color from blue to black.

Open `~/.p10k.zsh` with your editor of choice.
```sh
open -a TextEdit ~/.p10k.zsh
```
And then look for POWERLEVEL9K_DIR_BACKGROUND and change the color from 4 to 0 like so:
```sh
typeset -g POWERLEVEL9K_DIR_BACKGROUND=0
```
#### Better zsh history completion with up, down arrows
Let’s improve the history completion with the up and down arrows.

Open `~/.zshrc` and add the following to the bottom of this file:
```sh
# history setup
HISTFILE=$HOME/.zhistory
SAVEHIST=1000
HISTSIZE=999
setopt share_history
setopt hist_expire_dups_first
setopt hist_ignore_dups
setopt hist_verify
```
This will allow zsh to save the history to a file and configure how it should do so.

Then go back to the command line and run:
```sh
cat -v
```
Now press on your up and down arrow keys.

Copy the codes that you get as output.

Open the `~/.zshrc` file again and add the following to the bottom of this file:    
```sh
# history search
bindkey '^[[A' history-search-backward
bindkey '^[[B' history-search-forward
```
Replace `^[[A` and `[[B` with the key codes you got for up and down arrow keys if they are different.

#### Setup zsh-autosuggestions plugin
`zsh-autosuggestions` is a plugin for zsh that suggests commands as you type.

First install it using:
```sh
brew install zsh-autosuggestions
```
Then run the following:
```sh
echo "source $(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc
```
Now source `~/.zshrc`:
```sh
source ~/.zshrc
```
Now you can use the plugin! When you get a suggestion and want to use it, use the right arrow key.
#### Setup zsh-syntax-highlighting
`zsh-syntax-highlighting` is a plugin for zsh that highlights the syntax of your commands.

First install it using:
```sh
brew install zsh-syntax-highlighting
```
Then run the following:
```sh
echo "source $(brew --prefix)/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc
```
This adds what you need to `~/.zshrc` to enable the plugin.
Now source `~/.zshrc`:
```sh
source ~/.zshrc
```

#### Install eza (better ls)
[eza](https://github.com/eza-community/eza) is a better version of ls with lots of different options.
Install it:
```sh
brew install eza
```
You can create an alias for it in `~/.zshrc` like so:
```sh
alias ls='eza'
```
Now source `~/.zshrc`:
```sh
source ~/.zshrc
```
#### Install zoxide (better cd)
[zoxide](https://github.com/ajeetdsouza/zoxide) is a better cd command that learns your directory structure.

Install it:
```sh
brew install zoxide
```
Then add the following to `~/.zshrc`:
```sh
eval "$(zoxide init zsh)"

alias cd="z"
```
Now source `~/.zshrc`:
```sh
source ~/.zshrc
```
<div style="padding: 10px 0px;"></div>
<div style="font-size: 24px; font-weight: regular; width: fit-content; background-color: #E36397; color: #fff; padding: 8px 32px; display: flex; gap: 10px; align-items: center; border-radius: 2px; text-align: center;">
<svg xmlns="http://www.w3.org/2000/svg" x="0px" y="0px" width="24" height="24" viewBox="0 0 48 48">
<path fill="#29b6f6" d="M44,11.11v25.78c0,1.27-0.79,2.4-1.98,2.82l-8.82,4.14L34,33V15L33.2,4.15l8.82,4.14 C43.21,8.71,44,9.84,44,11.11z"></path><path fill="#0277bd" d="M9,33.896L34,15V5.353c0-1.198-1.482-1.758-2.275-0.86L4.658,29.239 c-0.9,0.83-0.849,2.267,0.107,3.032c0,0,1.324,1.232,1.803,1.574C7.304,34.37,8.271,34.43,9,33.896z"></path><path fill="#0288d1" d="M9,14.104L34,33v9.647c0,1.198-1.482,1.758-2.275,0.86L4.658,18.761 c-0.9-0.83-0.849-2.267,0.107-3.032c0,0,1.324-1.232,1.803-1.574C7.304,13.63,8.271,13.57,9,14.104z"></path>
</svg> VS Code
</div>
<div style="padding: 10px 0px;"></div>

* Intall extension `Outrun Meets Synthwave` and select color theme `Outrun Electric Meets Synthwave`
* Intall `Aut Icons` extension
* Intall `Custom CSS and JS Loader` extension
* Download Monokai and Nerd Code Font from [Nerd Fonts](https://www.nerdfonts.com/font-downloads). I personally use Fira Code iScript you can get it from here [Fira Code iScript](https://github.com/kencrocken/FiraCodeiScript).
* Open your `settings.json` file and copy paste everything from `vscode/settings.json` file. Make sure to replace `{username}` with your actual username.
* Go to file `"file:///Users/{username}/.vscode/extensions/codevars.outrun-meets-synthwave-0.0.1/synthWaveStyles.css"` in `settings.json` (by `cmd` + `click`) and replace all the css styles with the one in `vscode/style.css` file.
* Reload Custom CSS and JS Loader extension, using `cmd` + `shift` + `p` and select `Reload Extension`
* Note: This will throw up and error, saying you VSCode is broken, just ignore it.

If everything is done properly this is going look something like this. 
![image](https://i.ibb.co/CPPH2hZ/image.png)

Please feel free to customise it from here to your liking.
