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
pkgver=2.11.1
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
        1000-Enable-subpixel-hinting.patch
        1001-Low-pass-filter-gibson-coeffs.patch
        1002-Enable-subpixel-rendering.patch
        freetype2.sh
)
sha256sums=('3333ae7cfda88429c97a7ae63b7d01ab398076c3b67182e960e5684050f2c5c8'
            'SKIP'
            '739a67083b810c04e5cb87fa7e5a7819983410307e3d38d8f2a334c23085a5c2'
            '778a084b84215fbe62dafaed1dd7ebcdbd35c5c7af681d2789b5fe37764ceadd'
            '8e0fc429ad153fff05604735d254542ffc6070704ba07fff31122a19db3947c8'
            '0607ac8176d4f08bcfb78d07bdc2c66fcbe7dfde6c82a0e98d6e625597442fd0'
            '162895e2ba5dd17b6583110eb83b858e378411f3c2d2c8fda571f473af69f9ca'
            '6d059feaeb519aa29086a7c967ff0d31648c8c2adcbbe2fdfa8d9a50152b89cb'
            'f7f8e09c44f7552c883846e9a6a1efc50377c4932234e74adc4a8ff750606467')
validpgpkeys=('58E0C111E39F5408C5D3EC76C1A60EACE707FDA5') # Werner Lemberg <wl@gnu.org>

prepare() {
  cd freetype-${pkgver}
  # Patches from [extra]
  patch -Np1 -i ../0001-Enable-table-validation-modules.patch
  patch -Np1 -i ../0003-Enable-long-PCF-family-names.patch

  # PKGBUILD specific
  #patch -Np1 -i ../1000-Disable-subpixel-hinting.patch
  patch -Np1 -i ../1000-Enable-subpixel-hinting.patch
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
  install=freetype2.install
  backup=(etc/profile.d/freetype2.sh)

  cd freetype-${pkgver}
  make DESTDIR="${pkgdir}" install
  cd ..
  install -Dt "$pkgdir/etc/profile.d" -m644 freetype2.sh
  install -Dt "$pkgdir/usr/share/aclocal" -m644 \
    freetype-$pkgver/builds/unix/freetype2.m4
}
