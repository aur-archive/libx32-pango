# $Id: PKGBUILD 72529 2012-06-16 10:19:01Z bluewind $
# Contributor: Pierre Schmitz <pierre@archlinux.de>
# Contributor: Mikko Seppälä <t-r-a-y@mbnet.fi>
# Maintainer: Biru Ionut <ionut@archlinux.ro>
_pkgbasename=pango
pkgname=libx32-$_pkgbasename
pkgver=1.30.1
pkgrel=1.2
pkgdesc="A library for layout and rendering of text (x32 ABI)"
arch=('x86_64')
license=('LGPL')
depends=('libx32-glib2>=2.25.15' 'libx32-cairo>=1.10.0' 'libx32-libxft>=2.1.14'
         'libx32-freetype2>=2.4.2' $_pkgbasename)
makedepends=("gcc-multilib-x32")
options=('!libtool' '!emptydirs')
install=pango.install
source=(http://ftp.gnome.org/pub/gnome/sources/${_pkgbasename}/${pkgver:0:4}/${_pkgbasename}-${pkgver}.tar.xz
        pango-modules-conffile.patch)
url="http://www.pango.org/"
sha256sums=('3a8c061e143c272ddcd5467b3567e970cfbb64d1d1600a8f8e62435556220cbe'
            '4a178b60dd420ae53baeabbecfaaeca4070a4b777b2b3f36d137cd70b5a270c3')

build() {
  export CC="gcc -mx32"
  export CXX="g++ -mx32"
  export PKG_CONFIG_PATH="/usr/libx32/pkgconfig"

  cd "${srcdir}/${_pkgbasename}-${pkgver}"
  patch -p0 < ${srcdir}/pango-modules-conffile.patch
  # No libthai support yet
  ./configure --prefix=/usr --libdir=/usr/libx32 --sysconfdir=/etc \
      --localstatedir=/var --with-included-modules=basic-fc \
      --with-dynamic-modules=arabic-fc,arabic-lang,basic-fc,basic-win32,basic-x,basic-atsui,hangul-fc,hebrew-fc,indic-fc,indic-lang,khmer-fc,syriac-fc,tibetan-fc \
      --disable-introspection
  make
}

package() {
  cd "${srcdir}/${_pkgbasename}-${pkgver}"
  make DESTDIR="${pkgdir}" install
  rm -rf "$pkgdir"/etc
  rm -rf "$pkgdir"/usr/{bin/pango-view,share,include}
  mv "$pkgdir"/usr/bin/pango-querymodules "$pkgdir"/usr/bin/pango-querymodules-x32
}
