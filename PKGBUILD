# Contributer: Mikkel Kroman <mk@maero.dk> Skydrome <irc.freenode.net>
# Maintainer:  Ingamedeo <ingamedeo@gmail.com>

pkgname=mineserver-git
pkgver=20120804
pkgrel=1
url=('https://github.com/fador/mineserver')
pkgdesc="Custom Minecraft Beta server software written in C++ ... Now works with Raspberry Pi!!"
depends=('libnoise' 'libevent' 'zlib' 'openssl')
makedepends=('git' 'cmake')
arch=('i686' 'x86_64' 'armv6l')
license=("BSD")
provides=('mineserver')
source=()
install=mineserver.install

_gitname="mineserver"
_gitroot="git://github.com/fador/mineserver.git"

build() {
    cd ${srcdir}
    msg "Connecting to GIT ($_gitroot)..."
    if [ -d ${_gitname} ]; then
        cd ${_gitname} && git pull origin
        msg "The local files of $_gitname were updated."
    else
        git clone --depth 1 ${_gitroot}
        msg "GIT checkout done or server timeout"
    fi

    msg "Starting compile..."
    cd ${_gitname}
        cmake -DCMAKE_BUILD_TYPE=Release .
	sed -i 's/\(^.*$\)/\1 -lrt -lpthread/' src/CMakeFiles/mineserver.dir/link.txt
        make all
}

package() {
    mkdir -p ${pkgdir}/usr/{bin,share/mineserver}
    cd ${srcdir}/${_gitname}
        cp bin/mineserver ${pkgdir}/usr/bin/
        cp bin/{banned,motd,permissions,roles,rules,whitelist}.txt ${pkgdir}/usr/share/mineserver/
        cp bin/{commands,config,ENABLED_RECIPES,item_alias}.cfg ${pkgdir}/usr/share/mineserver/
        cp -r bin/plugins bin/recipes ${pkgdir}/usr/share/mineserver/
}
