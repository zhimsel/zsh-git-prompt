# Informative git prompt for zsh

A `zsh` prompt that displays information about the current git repository. In particular the branch name, difference with remote branch, number of files staged, changed, etc.

(an original idea from this [blog post][]).

## Examples

The prompt may look like the following:

-   `(master:70c2952↑3|✚1)`: on branch `master`, ahead of remote by 3 commits, 1 file changed but not staged
-   `(status:27a73e7|●2)`: on branch `status`, 2 files staged
-   `(master:70c2952|✚7…)`: on branch `master`, 7 files changed, some files untracked
-   `(master:70c2952|✖2✚3)`: on branch `master`, 2 conflicts, 3 files changed
-   `(experimental:0ac9d2b↓2↑3|✔)`: on branch `experimental`; your branch has diverged by 3 commits, remote by 2 commits; the repository is otherwise clean
-   `(:1ab899e|✔)`: not on any branch; parent commit has hash `1ab899e`;
    the repository is otherwise clean

Here is how it could look like when you are ahead by 4 commits, behind by 5 commits, and have 1 staged files, 1 changed but unstaged file, and some untracked files, on branch `dev`:


<img src="https://github.com/olivierverdier/zsh-git-prompt/raw/master/screenshot.png" width=300/>


## Prompt Structure

By default, the general appearance of the prompt is:

```
(<branch:ref><branch tracking>|<local status>)
```

The symbols are as follows:

### Local Status Symbols

|Symbol|Meaning
|------|------|
|✔ |   repository clean
|●n |   there are `n` staged files
|✖n |   there are `n` unmerged files
|✚n |   there are `n` changed but *unstaged* files
|… |   there are some untracked files


### Branch Tracking Symbols

Symbol | Meaning
-------|-------
↑n |   ahead of remote by `n` commits
↓n |   behind remote by `n` commits
↓m↑n |   branches diverged, other by `m` commits, yours by `n` commits


## Install

1.  Clone this repository somewhere on your hard drive.
2.  Source the file `git-prompt.plugin.zsh` from your `~/.zshrc` config file, and
    configure your prompt. So, somewhere in `~/.zshrc`, you should have:

    ```sh
    source path/to/git-prompt.plugin.zsh
    # an example prompt
    PROMPT='%B%m%~%b$(git_super_status) %# '
    ```
    
3.  Go in a git repository and test it!


#### Using frameworks

If you're using antigen, just add the following code to your `~/.zshrc` where you're loading your other zsh plugins.
```sh
    source $HOME/.zsh/antigen/antigen.zsh
    antigen bundle zhimsel/zsh-git-prompt
    antigen apply
    # an example prompt
    PROMPT='%B%m%~%b$(git_super_status) %# '
```

## Customisation

- You may redefine the function `git_super_status` (after the `source` statement) to adapt it to your needs (to change the order in which the information is displayed).
- Define the variable `ZSH_THEME_GIT_PROMPT_CACHE` in order to enable caching.
- You may also change a number of variables (which name start with `ZSH_THEME_GIT_PROMPT_`) to change the appearance of the prompt.  Take a look in the file `zshrc.sh` to see how the function `git_super_status` is defined, and what variables are available.

**Enjoy!**

  [blog post]: http://sebastiancelis.com/2009/nov/16/zsh-prompt-git-users/
  
