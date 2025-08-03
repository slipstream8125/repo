# Maintainer: @zstg <zestig@duck.com>
pkgname=stratos-kitty-config
pkgver=1.0
pkgrel=1
pkgdesc="Kitty configuration for StratOS"
arch=('any')
license=('GPL3')
depends=(
    'kitty'
    'ttf-jetbrains-mono'
    'ttf-jetbrains-mono-nerd'
)
source=()
install=stratos-kitty-config.install

prepare() {
	cp -r "$startdir/.config/" "$srcdir/"
}

package() {
    install -d "$pkgdir/etc/skel/.config"
    cp -r "$srcdir/.config/kitty/" "$pkgdir/etc/skel/.config/"
}
