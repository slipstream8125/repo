# Maintainer: @zstg <zestig@duck.com>
pkgname=stratos-starship-config
pkgver=1.0
pkgrel=1
pkgdesc="Starship configuration for StratOS"
arch=('any')
license=('GPL3')
depends=(
    'starship'
)
source=('.config')
md5sums=('SKIP')

package() {
    install -d "$pkgdir/etc/skel/.config"
    cp -r "$srcdir/.config/starship/" "$pkgdir/etc/skel/.config/"
    ln -sf "$srcdir/.config/starship/tokyonight-dark/starship.toml" "$pkgdir/etc/skel/.config/starship.toml"
    echo "Configuration files have been copied to /etc/skel."
    echo "You may copy these files to ~/.config/ and make any changes you wish."
}
