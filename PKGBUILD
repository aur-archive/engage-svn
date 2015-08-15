# Contributor: fancris3 <fancris3 at aol.com>
# Contributor: fbianconi <fbianconi at gmail.com>

# Maintainer: Moritz Maxeiner <moritz@ucworks.org>

pkgname=engage-svn
pkgver=82790
pkgrel=1
pkgdesc="Enlightenment e17 module: A taskbar and app-launcher dock, which makes use of composite."
arch=('i686' 'x86_64')
url="http://svn.enlightenment.org/svn/e/trunk/E-MODULES-EXTRA/engage/"
license=('MIT')
depends=('enlightenment17')
makedepends=('subversion')
provides=('engage')
options=('!libtool')
conflicts=('e-modules-extra')

_svntrunk=http://svn.enlightenment.org/svn/e/trunk/E-MODULES-EXTRA/engage/
_svnmod=engage

build() {
  cd "$srcdir"

  msg "Connecting to SVN server...."
  if [ -d "$_svnmod/.svn" ]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  ./autogen.sh --prefix=/usr
  make
}

package() {
  cd "$srcdir/$_svnmod-build"
  make DESTDIR="$pkgdir/" install

  install -D -m644 COPYING $pkgdir/usr/share/licenses/$pkgname/COPYING
  install -D -m644 COPYING-PLAIN $pkgdir/usr/share/licenses/$pkgname/COPYING-PLAIN
}
