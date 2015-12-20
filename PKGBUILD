# $Id: PKGBUILD 154427 2015-12-24 06:10:55Z fyan $
# Maintainer : Ionut Biru <ibiru@archlinux.org>

pkgname=lib32-libdbus
_pkgbasename=libdbus
pkgver=1.10.6
pkgrel=1
pkgdesc="DBus library (32-bit)"
arch=('x86_64')
url="http://www.freedesktop.org/Software/dbus"
license=('GPL' 'custom')
depends=('lib32-glibc' 'lib32-expat' 'libdbus')
makedepends=('gcc-multilib' 'lib32-libx11')
provides=('lib32-dbus-core' 'lib32-dbus')
conflicts=('lib32-dbus-core' 'lib32-dbus')
replaces=('lib32-dbus-core' 'lib32-dbus')
source=(http://dbus.freedesktop.org/releases/dbus/dbus-${pkgver}.tar.gz{,.asc})
md5sums=('26d0cf3a1c9782cb0e342101f0450440'
         'SKIP')
validpgpkeys=('DA98F25C0871C49A59EAFF2C4DE8FF2A63C7CC90'  # Simon McVittie <simon.mcvittie@collabora.co.uk>
              '3C8672A0F49637FE064AC30F52A43A1E4B77B059') # Simon McVittie <simon.mcvittie@collabora.co.uk>

build() {
    export CC="gcc -m32"
    export CXX="g++ -m32"
    export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

    cd "${srcdir}/dbus-${pkgver}"

    ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var --libdir=/usr/lib32 \
        --libexecdir=/usr/lib/dbus-1.0 --with-dbus-user=81 \
        --with-system-pid-file=/run/dbus.pid \
        --with-console-auth-dir=/run/console/ \
        --enable-inotify \
        --disable-verbose-mode --disable-static \
        --disable-tests --disable-asserts --disable-systemd

    make
}

package() {
    cd "${srcdir}/dbus-${pkgver}"
    make DESTDIR=${pkgdir} install

    rm -rf "${pkgdir}"/usr/{bin,include,lib,share}
    rm -rf "${pkgdir}"/{etc,var}

    mkdir -p "${pkgdir}/usr/share/licenses"
    ln -s ${_pkgbasename} "${pkgdir}/usr/share/licenses/${pkgname}"
}
