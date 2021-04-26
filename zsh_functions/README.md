# ZSH Functions

## Set a function path

In order to load the *zsh* functions easily, you should store them in a fixed path relative to your home directory. In my case, I opted for `~/.zfunc`. In order to read the function path at start, and lazy load the autoload functionality, you can do as follows:

```bash
# First, create the path
mkdir ~/.zfunc

# And then edit the .zshrc file with your favourite text exitor
vi ~/.zshrc
```

Add these lines at the end of your `.zshrc` file:

```bash
# Add function path to FPATH
fpath=( ~/.zfunc "${fpath[@]}" )
autoload -U $fpath[1]/*(:t)
```

Save your changes, and restart your terminal. You should now be able to execute all functions within the `.zfunc` directory.

## Functions in this folder

### kubeconf-select

Function created based on the *fish* implementation of `kubectl-select` created by Hans Kristian Flaatten, available [here](https://github.com/Starefossen/dotfiles/blob/master/.config/fish/functions/kubectl-select.fish).

This is, however, running as a function in *zsh* and renamed to `kubeconfig-select` as that is the work the function is doing. It works like this:

1. Create your kube config file and name it `config.appendix` where *appendix* can be whatever you want (but should make sense to you).
2. Issue the following command to symbolically link the *appendix* config file as your current kube config.

```bash
kubeconf-select appendix
```

3. The script will then execute the following:
   1. Read the *appendix* and the current working directory into variables
   2. Symbolically link the `config.appendix` as `config` in the `~/.kube` directory
   3. `cd` to the working directory set in a.
