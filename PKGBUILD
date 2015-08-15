# Contributor: Julian Leyh <julian@vgai.de>

pkgname=gtkada-svn
pkgver=213435
pkgrel=1
pkgdesc="GtkAda is a Gtk2+ binding for Ada using the OOP and other features of this programming language"
arch=('i686' 'x86_64')
url="http://libre.adacore.com/libre/tools/GtkAda/"
license=('GMGPL')
depends=('gtk3' 'gcc-ada')
makedepends=('subversion')
provides=('gtkada')
source=()
md5sums=()

_svntrunk=http://svn.eu.adacore.com/anonsvn/Dev/trunk/GtkAda
_svnmod=GtkAda

build() {
  cd "$srcdir"
  msg "Connecting to SVN server...."

  if [[ -d "$_svnmod/.svn" ]]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  #
  # BUILD
  #
  ./configure --prefix=/usr --with-GL=no
  make
}
package() {
  cd "$srcdir/$_svnmod-build"
  make DESTDIR="$pkgdir/" install
}
