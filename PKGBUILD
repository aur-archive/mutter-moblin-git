# Maintainer: Alex Anthony <alex.anthony28991@googlemail.com>

pkgname=mutter-moblin-git
_pkgname=mutter-moblin
pkgver=20090901
pkgrel=1
pkgdesc="The Moblin plugin for mutter."
arch=('i686' 'x86_64')
url="http://www.moblin.org"
license=('GPL')
depends=('mutter4moblin-git' 'nbtk-git' 'gtk2' 'gconf' 'mojito-git' 
'jana-git' 
'libsoup' 'evolution-data-server' 'gnome-menus')
#'moblin-web-browser-git')
makedepends=('git')
optdepends=('dates: events in myzone'
            'tasks: tasks in myzone')
provides=($_pkgname)
conflicts=($_pkgname)
_gitroot=git://git.moblin.org/${_pkgname}
_gitname=${_pkgname}
options=()
groups=('moblin-git')

build() {
  cd $startdir/src
  msg "Connecting to moblin.org git server...."
  rm  -rf $startdir/src/$_gitname-build

  if [[ -d $_gitname ]]; then
   cd $_gitname || return 1
   git pull origin || return 1
    else
   git clone $_gitroot $_gitname || return 1
     fi
  msg " checkout done."
  cd $srcdir || return 1
  cp -r $_gitname $_gitname-build

   cd $_gitname-build || return 1

    ./autogen.sh --prefix=/usr --sysconfdir=/etc --localstatedir=/var \
    --enable-ahoghill \
    --enable-people || return 1
#    --enable-netpanel || return 1
    make || return 1
    make DESTDIR=$pkgdir install || return 1

    # Merge gconf schemas in a single file
#    install -d m755 $pkgdir/usr/share/gconf/schemas || return 1
#    gconf-merge-schema $pkgdir/usr/share/gconf/schemas/epiphany.schemas 
#        $pkgdir/etc/gconf/schemas/*.schemas || return 1
#    rm -rf $pkgdir/etc
}
