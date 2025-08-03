# Maintainer: @zstg <zestig@duck.com>
pkgname=stratos-waybar-config
pkgver=1.0
pkgrel=1
pkgdesc="Waybar configuration for StratOS"
arch=('any')
license=('GPL3')
depends=('waybar')
source=('.config')
md5sums=('SKIP')

package() {
    install -d "$pkgdir/etc/skel/.config"
    cp -r "$srcdir/.config/waybar" "$pkgdir/etc/skel/.config/"
    echo "Configuration files have been copied to /etc/skel."
    echo "You may copy these files to ~/.config/ and make any changes you wish."
}
