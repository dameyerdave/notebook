# R

## Install `R`

```bash
xcode-select --install
brew cask install xquartz
brew install r
brew cask install tcl
brew cask doctor
brew cleanup
```

## Install `RStudio`

1. Goto [RStudio download page](https://rstudio.com/products/rstudio/download/#download) and download the `dmg`
2. Install it

## Run `R`

```bash
R -g Tk &
```

## Run an `Rscript`

```bash
Rscript myscript.R
```