trackpad setting
keyboard setting
install brew
brew bundle

- iterm setting

color theme
https://github.com/MartinSeeler/iterm2-material-design

Preference - General -Working Directory - Reuse previous seesion's directory

https://coderwall.com/p/ds2dha/word-line-deletion-and-navigation-shortcuts-in-iterm2


- fish setting

set fish as default shell
echo `which fish` | sudo tee -a /etc/shells
chsh -s `which fish`

install fisherman
z
fzf
docker-completion
laughedelic/pisces
omf/thefuck

fish theme
mars
eclm
fisher omf/theme-mars

h.fish

set -x HOMEBREW_GITHUB_API_TOKEN <TOKEN>

alias


- Git (TBD)
ssh-keygen
https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/
add ssh key to github

https://git-scm.com/book/ko/v2/Git의-기초-Git-Alias
git alias

- asdf
https://medium.com/empex/elixir-version-management-with-asdf-34af3a5245ab

* before install erlang, run `brew install wxmac`. https://github.com/asdf-vm/asdf-erlang#before-asdf-install

add below to config.fish
source /usr/local/opt/asdf/asdf.fish

asdf plugin-add erlang https://github.com/asdf-vm/asdf-erlang
asdf plugin-add elixir https://github.com/asdf-vm/asdf-elixir
asdf plugin-add nodejs https://github.com/asdf-vm/asdf-nodejs
# Imports Node.js release team's OpenPGP keys to main keyring
bash ~/.asdf/plugins/nodejs/bin/import-release-team-keyring

asdf install {package} {version}
asdf global {package} {version}

- docker

change memory

- set computer name

https://apple.stackexchange.com/questions/30552/os-x-computer-name-not-matching-what-shows-on-terminal
