# Fork note

## Quick start

A forked version of `ttyd` having built-in web font and nerd symbol support.

We currently has two embedded fonts: Nerd-patched `JetBrains` font, and Chinese font `Sarasa Mono SC`.

See the [fork note](nerdForkUsage.md) for detailed usage.


## Add custom font

If you want other fonts, the simplest way is to replace the woff2 font file in `html/src/style/webfont` and compile it again.

If you'd like also to change the font name, change the `@font-face` section in `html/src/style/index.scss`,
**and also the ttyd launching command options**.

Only woff2 files are accepted.

## Build

```sh
# shell: posix sh
# depends: libc6-dev, gcc, g++, make, cmake, git, libjson-c-dev, libwebsockets-dev

# access to the temporary directory
cd $(mktemp -d)

# clone repo
git clone --depth=1 https://github.com/2moe/ttyd-nerd
cd ttyd-nerd

mkdir -p build
cd build

cmake .. -DCMAKE_INSTALL_PREFIX=$PWD/dist
make -j
make install

install -Dm755 ./dist/bin/ttyd  ~/.local/bin/ttyd-nerd
```

## Example

```zsh
# shell: zsh

path+=(
  ~/.local/bin
)

font_family=(
  "InconsolataGo Nerd Font"
  JetBrains
  SarasaMono
  # Serif
)

args=(
  #  Allow clients to write to the TTY (readonly by default)
  --writable

  # Send option to client (format: key=value)
  --client-option
  fontFamily=${(j^,^)font_family}

  --client-option
  fontSize=19

  zsh
  --login
)

ttyd-nerd $args
```

---

## Upstream

[wiki](https://github.com/tsl0922/ttyd/wiki)

ttyd is a simple command-line tool for sharing terminal over the web.

![screenshot](./screenshot.gif)