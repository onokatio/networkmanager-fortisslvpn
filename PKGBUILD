# Maintainer: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>
# Contributor: Ionut Biru <ibiru@archlinux.org>

pkgname=networkmanager-fortisslvpn-git
pkgver=1.2.11dev+22+g2b8a288
pkgrel=1
pkgdesc="NetworkManager VPN plugin for SSL VPN"
url="https://wiki.gnome.org/Projects/NetworkManager"
arch=(x86_64)
license=(GPLv2)
depends=(libnm openfortivpn)
makedepends=(git)
#optdepends=('libnma: GUI support')
source=("git+https://gitlab.gnome.org/GNOME/NetworkManager-fortisslvpn.git")
sha256sums=('SKIP')

pkgver() {
  cd NetworkManager-fortisslvpn
  git describe --tags | sed 's/-dev/dev/;s/-/+/g'
}

prepare() {
  cd NetworkManager-fortisslvpn

  intltoolize --automake --copy
  autoreconf -fvi
}

build() {
  cd NetworkManager-fortisslvpn
  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var \
    --libexecdir=/usr/lib --disable-static
  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool
  make
}

package() {
  cd NetworkManager-fortisslvpn
  make DESTDIR="$pkgdir" install dbusservicedir=/usr/share/dbus-1/system.d
}

# vim:set sw=2 et:
