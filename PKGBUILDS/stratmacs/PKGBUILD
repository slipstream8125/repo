# Maintainer: ZeStig <o0vckutt@duck.com>
# based on https://gitlab.archlinux.org/archlinux/packaging/packages/emacs/-/blob/main/PKGBUILD?ref_type=heads
pkgbase=emacs
pkgname=(emacs emacs-pgtk emacs-lucid emacs-pgtk-nativecomp emacs-lucid-nativecomp)
pkgver=30.1
pkgrel=5
pkgdesc="Wayland-native Emacs build for StratOS"
arch=('x86_64')
url='https://github.com/stratos-linux/stratmacs'
license=('GPL-3.0-or-later')
optdepends=(
    'git'
    'cmake'
    'vterm'
    'mu'
    'ttf-jetbrains-mono'
)
makedepends=(git cmake libgccjit)
depends=(
  gmp poppler-glib gnutls lcms2 libacl.so libasound.so libgccjit
  libdbus-1.so libfontconfig.so libfreetype.so libgdk-3.so
  libgdk_pixbuf-2.0.so libgif.so libgio-2.0.so libglib-2.0.so
  libgobject-2.0.so libgpm.so libgtk-3.so libharfbuzz.so libice
  libjpeg.so libncursesw.so libotf libpango-1.0.so libpng librsvg-2.so
  libsm sqlite libsqlite3.so libsystemd.so libtiff.so
  libtree-sitter.so libwebp.so libwebpdemux.so libxfixes libxml2.so
  m17n-lib zlib libvterm.so
)

source=(
  https://ftp.gnu.org/gnu/emacs/emacs-${pkgver}.tar.xz{,.sig}
  fix-compile.patch::https://github.com/emacs-mirror/emacs/commit/53a5dada413662389a17c551a00d215e51f5049f.patch
)
b2sums=('ad502a2e15a04618f4766ec6e285739cb5bb6f19c5065c3aed03b3e50df590cee382a0331f382de6f13523f1362a4355f65961ce45504f7d33419ea6d04e326f'
        'SKIP'
        'b38ad198ed8975963a05201e2124b8cf2947c6ddb792aaef618d1968d7b0329241235f4ccc69ac62ee43189e20aa70a28254f6c787fa38359c1aae22286df9d1')

prepare() {
  patch -d emacs-${pkgver} -Np1 < fix-compile.patch

  cp -a emacs-${pkgver} ${srcdir}/emacs-${pkgver}-pgtk
  cp -a emacs-${pkgver} ${srcdir}/emacs-${pkgver}-lucid
  cp -a emacs-${pkgver} ${srcdir}/emacs-${pkgver}-pgtk-nativecomp
  cp -a emacs-${pkgver} ${srcdir}/emacs-${pkgver}-lucid-nativecomp
}

_build_emacs_variant() {
  local variant=$1
  shift
  local flags=("$@")

  cd "${srcdir}/emacs-${pkgver}-${variant}"
  export CFLAGS+=" -O2"
  export ac_cv_lib_gif_EGifPutExtensionLast=yes
  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --libexecdir=/usr/lib \
    --localstatedir=/var \
    --with-gnutls \
    --with-tree-sitter \
    --with-png \
    --with-jpeg \
    --without-wide-int \
    --with-sound \
    --with-sqlite3 \
    --with-xpm=ifavailable \
    --with-gif=ifavailable \
    --with-libsystemd \
    --with-dbus \
    --with-pdumper \
    --without-pop \
    --without-mailutils \
    --disable-gc-mark-trace \
    "${flags[@]}"
  make
}

build() {
  _build_emacs_variant pgtk --with-pgtk --without-xwidgets
  _build_emacs_variant lucid --with-x-toolkit=lucid --with-xwidgets
  _build_emacs_variant pgtk-nativecomp --with-pgtk --with-native-compilation --without-xwidgets
  _build_emacs_variant lucid-nativecomp --with-x-toolkit=lucid --with-native-compilation--with-xwidgets
}

_package_emacs_variant() {
  local variant=$1
  local pkgdesc="$2"

  cd "${srcdir}/emacs-${pkgver}-${variant}"
  make DESTDIR="${pkgdir}" install

  # Avoid conflict with ctags package
  mv "${pkgdir}/usr/bin/ctags" "${pkgdir}/usr/bin/ctags.emacs"
  mv "${pkgdir}/usr/share/man/man1/ctags.1.gz" "${pkgdir}/usr/share/man/man1/ctags.emacs.1"

  chown -R root:root "${pkgdir}/usr/share/emacs/${pkgver}"
}

package_emacs() {
  pkgdesc='The extensible, customizable, self-documenting real-time display editor (no toolkit)'
  cd "${srcdir}/emacs-${pkgver}"
  make DESTDIR="${pkgdir}" install

  mv "${pkgdir}/usr/bin/ctags" "${pkgdir}/usr/bin/ctags.emacs"
  mv "${pkgdir}/usr/share/man/man1/ctags.1.gz" "${pkgdir}/usr/share/man/man1/ctags.emacs.1"

  chown -R root:root "${pkgdir}/usr/share/emacs/${pkgver}"
}

package_emacs-pgtk() {
  pkgdesc='Emacs with PGTK (Pure GTK) support for Wayland'
  provides=(emacs)
  conflicts=(emacs)
  _package_emacs_variant pgtk "$pkgdesc"
}

package_emacs-lucid() {
  pkgdesc='Emacs with the classic X11 Lucid toolkit'
  provides=(emacs)
  conflicts=(emacs)
  _package_emacs_variant lucid "$pkgdesc"
}

package_emacs-pgtk-nativecomp() {
  pkgdesc='Emacs with PGTK and native compilation enabled'
  depends+=(libgccjit)
  provides=(emacs)
  conflicts=(emacs)
  _package_emacs_variant pgtk-nativecomp "$pkgdesc"
}

package_emacs-lucid-nativecomp() {
  pkgdesc='Emacs with Lucid X11 toolkit and native compilation'
  depends+=(libgccjit)
  provides=(emacs)
  conflicts=(emacs)
  _package_emacs_variant lucid-nativecomp "$pkgdesc"
}
