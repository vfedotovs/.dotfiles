# .dotfiles
My dotfiles for using stow utility


# Basic stow workflow
1. Create clone repo .dotfiles and clone to ~ folder
2. Go inside folder 
```zsh
cd .dotfiles/
```

3. Manually replicate config file folder structure in .dotfiles in context of stow target dir ~
```zsh 
mkdir git
touch git/.gitconfig
```

4. Perform dry-run of what stow will do
```zsh
stow --adopt -n -v -t ~ git
LINK: .gitconfig => .dotfiles/git/.gitconfig
WARNING: in simulation mode so not modifying filesystem.
```

5. Perform sync  if file .gitconfig in ~ does not exist stow will replace will create .gitconfig with .dotfiles/git/.gitconfig and will create symlink.
```zsh 
stow --adopt -v -t ~ git
LINK: .gitconfig => .dotfiles/git/.gitconfig
```

Another example with zsh config dotfile
```zsh
stow --adopt -n -v -t ~ zsh
MV: .zshrc -> .dotfiles/zsh/.zshrc
LINK: .zshrc => .dotfiles/zsh/.zshrc
WARNING: in simulation mode so not modifying filesystem.

.dotfiles > stow --adopt -v -t ~ zsh
MV: .zshrc -> .dotfiles/zsh/.zshrc
LINK: .zshrc => .dotfiles/zsh/.zshr
```

6. Rremoves symlink from ~/.gitconfig to .dotfiles/git/.gitconfig AND DELETES ~/.gitconfig
```zsh
stow -v -D -t ~ git
UNLINK: .gitconfig
```

Note:
.dotfiles does support for example OS grouping or other types of groupings

```zsh
.dotfiles>tree -a
.
├── git
│   └── .gitconfig
├── linux-ubuntu
│   └── git
│       └── .gitconfig
├── macOS
├── windows
└── zsh
    └── .zshrc
```


Important NOTE: stow does not support / in linux-ubuntu/git folder structure fix stow must be run from linux-ubuntu/ folder

 ```zsh
 .dotfiles> stow --adopt -n -v -t ~ linux-ubuntu/git
stow: ERROR: Slashes are not permitted in package names
```
    
