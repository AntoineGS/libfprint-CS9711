# Build from this checkout so the package includes the rebased CS9711 changes.
pkgname=libfprint-cs9711-pr3
pkgver=1.94.100.pr3
pkgrel=1
pkgdesc='CS9711-only libfprint with the Windows-driver PR 3 changes'
arch=('x86_64')
url='https://github.com/AntoineGS/libfprint-CS9711'
license=('LGPL-2.1-or-later')
depends=('glib2' 'glibc' 'gcc-libs' 'libgusb' 'opencv')
makedepends=('meson' 'ninja' 'glib2-devel' 'gobject-introspection' 'doctest')
provides=('libfprint=1.94.100' 'libfprint-2.so')
conflicts=('libfprint')
options=('!debug')

build() {
  meson setup "$srcdir/build" "$startdir" \
    --prefix=/usr \
    --libdir=lib \
    --buildtype=release \
    -Ddrivers=cs9711 \
    -Ddoc=false \
    -Dinstalled-tests=false
  meson compile -C "$srcdir/build"
}

check() {
  meson test -C "$srcdir/build" --print-errorlogs
  "$srcdir/build/libfprint/sigfm/sigfm-tests"
}

package() {
  DESTDIR="$pkgdir" meson install -C "$srcdir/build" --no-rebuild
}
