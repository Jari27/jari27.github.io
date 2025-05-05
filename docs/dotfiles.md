# Dotfiles

I have my [dotfiles](https://github.com/jari27/dotfiles) setup with a bare git repository inside my home directory (`~/.dotfiles/`), as described in [this blogpost](https://www.anand-iyer.com/blog/2018/a-simpler-way-to-manage-your-dotfiles/).

### Adding Files: `git add --all` vs `git add`
Since I usually run `gaa` to commit all files, I originally set up my `.gitignore` to automatically excluded everything and then added exceptions.
However, this is extremely annoying when dealing with (nested) directories.
So, I've now shifted to the original suggestion, which is to hide untracked files by default (`dotfiles config --local status.showUntrackedFiles no`) and to commit more precisely.

???+ note "Why using `.gitignore` is annoying"
    Using `.gitignore` is annoying when dealing with directories that are partially ignored.
    For example, when using [Oh My Zsh](https://ohmyz.sh/), there is a folder named `custom` that contains your custom scripts, e.g. `~/.oh-my-zsh/custom/path.zsh`
    This folder also contains `example.zsh`, which I do not want to be committed to my dotfiles repo.
    To include everything inside this path except `example.zsh`, your `.gitignore` has to look like this:

    ```gitignore title=".gitignore"
    /*                             # ignore all files in home
    !.oh-my-zsh/                   # but allow git to see the oh-my-zsh directory
    .oh-my-zsh/*                   # but ignore all files inside
    !.oh-my-zsh/custom/            # but allow git to see the custom directory
    .oh-my-zsh/custom/example.zsh  # but ignore example.zsh
    ```


### Zsh completion for Your Custom dotfiles alias
To get completion working for your setup (which contains an alias like `alias dotfiles='/usr/local/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'`), you need to enable `_git` completions for that command.
You do this by executing the following line (e.g. in `.zshrc`):

```zsh
compdef _git dotfiles
```
