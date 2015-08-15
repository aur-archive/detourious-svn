# Maintainer: Andy Ross <spiffyspaceman88@yahoo.com>
pkgname=detourious-svn
pkgver=80018
pkgrel=2
pkgdesc="Detourious theme for E17 (with support for GTK2/GTK3)"
arch=('any')
url="http://svn.enlightenment.org/svn/e/trunk/THEMES/detourious/"
license=('GPL')
depends=('edje')
makedepends=('subversion')

_svntrunk=http://svn.enlightenment.org/svn/e/trunk/THEMES/detourious/
_svnmod=detourious

build() {
  cd "$srcdir"
  msg "Connecting to SVN server...."

  if [[ -d "$_svnmod/.svn" ]]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"

  cd "$srcdir/$_svnmod-build"
  make
}

package() {
  cd $srcdir/$_svnmod-build
  install -Dm644 $_svnmod.edj $pkgdir/usr/share/enlightenment/data/themes/$_svnmod.edj
  install -Dm644 $_svnmod-dark.edj $pkgdir/usr/share/enlightenment/data/themes/$_svnmod-dark.edj
  install -Dm644 $_svnmod-illume.edj $pkgdir/usr/share/enlightenment/data/themes/$_svnmod-illume.edj
  install -Dm644 $_svnmod-elm.edj $pkgdir/usr/share/elementary/themes/$_svnmod-elm.edj
  mkdir -p $pkgdir/usr/share/themes/Detourious
  mv $srcdir/$_svnmod-build/gtk/detourious/gtk-2.0 $pkgdir/usr/share/themes/Detourious/gtk-2.0
  mv $srcdir/$_svnmod-build/gtk/detourious/gtk-3.0 $pkgdir/usr/share/themes/Detourious/gtk-3.0
}