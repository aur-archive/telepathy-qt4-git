# Maintainer: George Brooke <george+arch.aur@george-brooke.co.uk>
# Contributor: Laurent Carlier <lordheavym@gmail.com>

pkgname=telepathy-qt4-git
pkgver=20120507
pkgrel=1
pkgdesc="A library for Qt-based Telepathy clients"
arch=('i686' 'x86_64')
url="http://telepathy.freedesktop.org"
license=('LGPL')
depends=('qt' 'telepathy-farstream')
makedepends=('libxslt' 'python2' 'cmake' 'git' 'doxygen')
conflicts=('telepathy-qt4')
provides=('telepathy-qt4')
options=('!libtool')

_gitroot="git://git.collabora.co.uk/git/freedesktop.org-mirror/telepathy/telepathy-qt4.git"
_gitname="telepathy-qt4"

build() {
  cd ${srcdir}

  msg "Connecting to the GIT server...."
  
  if [[ -d ${srcdir}/$_gitname ]] ; then
    cd $_gitname
    git checkout -- .
    git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot
  fi
  
  msg "GIT checkout done"
  msg "Patching..."
  cd ${srcdir}/${_gitname}

  msg "Starting configure..."

  rm -rf ${srcdir}/build && mkdir ${srcdir}/build
  cd ${srcdir}/build

  cmake ../$_gitname \
      -DCMAKE_INSTALL_PREFIX=/usr \
      -DPYTHON_EXECUTABLE=/usr/bin/python2
  
  msg "Starting make..."
  make
}

package() {
  cd ${srcdir}/build

  make DESTDIR="$pkgdir" install
}
