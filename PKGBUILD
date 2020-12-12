# Maintainer: Andrzej Rybczak <andrzej@rybczak.net>
# Contributor: Bruno Pagani (a.k.a. ArchangeGabriel) <bruno.n.pagani@gmail.com>
# Contributor: jeckhack <jeckhack/gmail/com>
# Contributor: Marcin (CTRL) Wieczorek <marcin@marcin.co>
# Contributor: frames <markkuehn at outlook dot com>
# Contributor: Estevao Valadao <estevao@archlinux-br.org>
# Contributor: Tetsumaki <http://goo.gl/YMBdA>
# Contributor: Dave Reisner <d@falconindy.com>
# Contributor: Lee.MaRS <leemars@gmail.com>
# Contributor: freedom

pkgname=freetype2-classic
pkgver=2.10.2
pkgrel=1
pkgdesc="Font rasterization library with classic (v35) interpreter, subpixel rendering and modified filter coefficients (Gibson)"
arch=(x86_64)
license=('GPL')
url="https://www.freetype.org/"
    # adding harfbuzz for improved OpenType features auto-hinting
    # introduces a cycle dep to harfbuzz depending on freetype wanted by upstream
depends=('zlib' 'bzip2' 'sh' 'libpng' 'harfbuzz')
makedepends=('libx11')
conflicts=('freetype2')
provides=('freetype2' 'libfreetype.so')
source=(https://download-mirror.savannah.gnu.org/releases/freetype/freetype-${pkgver}.tar.xz{,.sig}
        0001-Enable-table-validation-modules.patch
        0003-Enable-long-PCF-family-names.patch
        1000-Disable-subpixel-hinting.patch
        1001-Low-pass-filter-gibson-coeffs.patch
        1002-Enable-subpixel-rendering.patch
)
sha1sums=('b074d5c34dc0e3cc150be6e7aa6b07c9ec4ed875'
          'SKIP'
          '46fd67e6a594f6c2c473b9321ba64913984ba42f'
          'af76172be8135e74391b7ad1b82c2124ae0ad86c'
          '59331e00ecf12504b5258f6dd04e29ac8a9874b0'
          '90c401227f50ae75ed4b3db411d3a27814dcd5bf'
          '769ee34c98e78d1e6182476704ddec85f92da394')
validpgpkeys=('58E0C111E39F5408C5D3EC76C1A60EACE707FDA5')

prepare() {
  cd freetype-${pkgver}
  # Patches from [extra]
  patch -Np1 -i ../0001-Enable-table-validation-modules.patch
  patch -Np1 -i ../0003-Enable-long-PCF-family-names.patch

  # PKGBUILD specific
  patch -Np1 -i ../1000-Disable-subpixel-hinting.patch
  patch -Np1 -i ../1001-Low-pass-filter-gibson-coeffs.patch
  patch -Np1 -i ../1002-Enable-subpixel-rendering.patch
}

build() {
  cd freetype-${pkgver}
  ./configure --prefix=/usr --disable-static
  make
}

check() {
  cd freetype-${pkgver}
  make -k check
}

package() {
  cd freetype-${pkgver}
  make DESTDIR="${pkgdir}" install
}
