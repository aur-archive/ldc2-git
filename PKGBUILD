# Maintainer: Fat Cat <carlos_manuel_83 at hotmail dot com>
# Maintainer: Marenz <aur at supradigital dot org>

pkgname=('ldc2-git')
pkgver=5e598af
pkgrel=1
groups=('devel')
url="http://ldc-developers.github.com/ldc"
license=('BSD' 'GPL')
arch=('i686' 'x86_64')
pkgdesc="A LLVM based compiler for the D programming language (Version 2)"
makedepends=('cmake')
depends=('libconfig' 'llvm>=3.1')
optdepends=('bash-completion: if you want auto-completion when using bash, for ldc.')
provides=('ldc2' 'ldc' 'ldc-git')
backup=('etc/ldc2.conf' 'etc/ldc2.rebuild.conf')
conflicts=('ldc1' 'ldc' 'ldc1-git' 'ldc-git')
makedepends=('git' 'doxygen' 'graphviz')
options=('!emptydirs' 'makeflags' 'zipman')
source=('ldc2.conf' 
        'ldc2.rebuild.conf'
        'ldc::git+https://github.com/ldc-developers/ldc.git')
sha512sums=('97d177bdf5a40f0e1c5caef16d3ddb7d06d75d770ba07ba4a7ec6aa35c21a9e4b4b53d248e713834db7934acc8093545a4a991954c02c2ef86444811b6557d0f'
            '5f4cb59e5d7c42a438eece1fdad37ad3921eab7995d9ad0e5920aaf50b2364d80cb9a7089120a7abd6120376f4129e1a1b9dbe5283309d8febbf0a080003f0dc'
            'SKIP')

pkgver () {
  cd "$srcdir/ldc"
  git describe --always | sed 's/-/./g'
}

build() {
  cd "$srcdir/ldc"

  msg "Cloning the submodules..."
  git submodule init
  git submodule update
  cd ..

  msg "Creating cmake build directory..."
  if [ ! -d build ]; then mkdir build; fi
  cd build
  cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr "$srcdir/ldc"

  msg "Now building..."
  make
}

package() {
  
  cd "$srcdir/build"
  make DESTDIR="$pkgdir/" install
  cp $srcdir/ldc2.conf $pkgdir/etc/ldc2.conf
  cp $srcdir/ldc2.rebuild.conf $pkgdir/etc/ldc2.rebuild.conf
  mkdir -p $pkgdir/usr/share/licenses/ldc2-git
  cp $srcdir/ldc/LICENSE $pkgdir/usr/share/licenses/ldc2-git
}
