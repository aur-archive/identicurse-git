# Former maintainer: timttmy <marshall\\dot//cleave\\at//tiscali\\dot//co\\dot//uk>
# Maintainer: Psychedelic Squid <psquid@psquid.net>


pkgname='identicurse-git'
_pkgname=identicurse
pkgver=20130307
pkgrel=10
pkgdesc="Curses-based identi.ca/status.net client - latest git revision"
arch=('any')
url="http://identicurse.net"
license=('GPL3')
depends=('python2' 'ncurses')
provides=('identicurse')
optdepends=('python2-oauth')
makedepends=('git' 'python2-distribute')
#install=(identicurse.install)

# Both of these will work, unless one of the repo hosts is down. Both URLs are
#  provided for convenience, though github is the one enabled by default.
# _gitroot="git://gitorious.org/identicurse/identicurse.git"
_gitroot="git://github.com/identicurse/IdentiCurse.git"

_gitname="identicurse"

package() {
    cd "$srcdir"
    msg "Connecting to GIT server...."

    if [ -d $_gitname ] ; then
        cd $_gitname && git pull origin
        msg "The local files are updated."
    else
        git clone $_gitroot $_gitname
    fi

    msg "GIT checkout done or server timeout"

    cd "$srcdir/$_gitname"

    msg ""

    msg "Starting make..."

    cd $srcdir/$_gitname/statusnet
    python2 setup.py install --prefix=/usr --install-data=/usr/share --root="$pkgdir" || return 1
    cd $srcdir/$_gitname
    python2 setup.py install --prefix=/usr --install-data=/usr/share --root="$pkgdir" || return 1
    install -m 644 $srcdir/$_gitname/README "$pkgdir/usr/lib/python2.7/site-packages/identicurse/README" || return 1
    install -m 644 $srcdir/$_gitname/conf/config.json "$pkgdir/usr/lib/python2.7/site-packages/identicurse/config.json" || return 1
    install -m 644 $srcdir/$_gitname/conf/messages.json "$pkgdir/usr/lib/python2.7/site-packages/identicurse/messages.json" || return 1
}
