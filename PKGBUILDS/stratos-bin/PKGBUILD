# Maintainer: @zstg <zestig@duck.com>
pkgname=stratos-bin
pkgver=1.0
pkgrel=1
pkgdesc="Core StratOS scripts"
arch=('any')
license=('GPL3')
depends=('bash' 'yay-bin' 'python' 'dialog')
optdepends = (
	'flatpak: Universal package manager'
)
source=()
md5sums=()

package() {
    install -d "$pkgdir/usr/local/bin/"
    cp -a "usr/local/bin/." "$pkgdir/usr/local/bin/"
}
