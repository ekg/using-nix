# nix single-user setup

Nix is a nice way to build and manage software.
It works best when installed system wide in a multi-user setup.
But you can also run it in a chroot, which can be helpful on systems where you don't have root (like HPC clusters...)

## setup

0. Install cargo and the rust buildchain.
1. `cargo install nix-user-chroot`
2. Copy `nix-it` and `nix-zsh` into your path.

## tmux takeover

Bonus: set tmux to drop you into the nix chroot by default.
This avoids requiring any change of shell.
Also, if the env or chroot system gets messed up, we won't lose shell access.

```
echo 'set-option -g default-shell $HOME/bin/nix-zsh' >>~/.tmux.conf
```

## usage

Run commands in the nix chroot using `nix-it`, or drop into a `zsh` shell in the chroot with `nix-zsh`.

You can install and use software from nix channels listed in `~/.nix-channels`.

```
nix-it nix-env -i hello
nix-it hello
```

Remove software with `nix-env -e <package>`, e.g. `nix-env -e hello` in this case.

## building software

Nix makes it easy to build software based on package expressions written in the nix expression language.
By default, we'll use information in `default.nix` in the current working directory.

```
nix-build
nix-env -i ./result
```
