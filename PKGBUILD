pkgname=mlbviewer
pkgver=2013
pkgrel=7
_pkgver="${pkgver}-sf-${pkgrel}"
pkgdesc="A collection of tools to view and listen to streaming baseball games from mlb.tv."
arch=('any')
url="http://sourceforge.net/projects/mlbviewer/"
license=('GPLv2')
makedepends=('libconfig')

source=("http://downloads.sourceforge.net/project/${pkgname}/${pkgname}/${pkgver}/${pkgname}${_pkgver}.tar.gz")
sha1sums=('2df0e8517ca7bb78e266b428060bcf4a7bc42b3a')


build () {
  # mlbhls for nexdef
  cd $srcdir
  svn co https://mlbtv-hls-nexdef.googlecode.com/svn/branches/experimental mlbhls
  cd mlbhls
  make
}

package () {
  cd "$srcdir/${pkgname}${_pkgver}"

  install -vd $pkgdir/usr/bin
  install -vd $pkgdir/usr/lib/${pkgname}

  # install and symlink main executables
  for f in listings play viewer; do
    sed -i 's:#!/usr/bin/env python:#!/usr/bin/env python2:g' mlb${f}.py

    install -vm755 mlb${f}.py $pkgdir/usr/lib/mlb${f}

    ln -s /usr/lib/${pkgname}/mlb${f}.py $pkgdir/usr/bin/mlb${f}
  done

  # main program libs and utils
  cp -a MLBviewer test $pkgdir/usr/lib/${pkgname}

  # documentation
  install -vd $pkgdir/usr/share/doc/${pkgname}
  install -vm644 MLBPLAY-HELP README REQUIREMENTS-${pkgver}.txt TOOLS $pkgdir/usr/share/doc/${pkgname}

  # mlbhls
  install -vm755 $srcdir/mlbhls/mlbhls $pkgdir/usr/bin
}

# vim:set ts=2 sw=2 et:
