# maim

**maim** (**Ma**ke **Im**age) is a utility to take screenshots of my desktop.

- Repo: https://github.com/naelstrof/maim
- AUR: https://www.archlinux.org/packages/community/x86_64/maim

## Commands

### Simple screenshot

Can't get any simpler than this.

```sh
maim ~/image.png
```

### Region screenshot

Takes a screenshot of a region, then copy to the clipboard. Remember of `-s` as interactive **s**election.

```sh
maim -s | xclip -selection clipboard -t image/png
```

### Window screenshot

Takes a screenshot of the current active window. Remember of `-i` as **i**nput window.

```sh
maim -i $(xdotool getactivewindow) ~/image.png
```
