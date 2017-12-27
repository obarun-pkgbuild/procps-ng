# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://aur.archlinux.org/packages/procps-ng-nosystemd
# 						Maintainer: Alexey D. <lq07829icatm@rambler.ru>
# 						Contributor: Gaetan Bisson <bisson@archlinux.org>
# 						Contributor: Eric Bélanger <eric@archlinux.org>

pkgname=procps-ng
pkgver=3.3.12
pkgrel=4
pkgdesc='Utilities for monitoring your system and its processes'
url='https://gitlab.com/procps-ng/procps'
license=('GPL' 'LGPL')
arch=('x86_64')
depends=('ncurses')
backup=('etc/sysctl.conf')
source=("https://downloads.sourceforge.net/project/procps-ng/Production/procps-ng-${pkgver}.tar.xz"
        'impossibly-high-memory.patch'
        'sysctl.conf')
sha1sums=('82c0745f150f1385ca01fe7d24f05f74e31c94c6'
          '27e32a557886dafac6e9c55ecf40e3d9a89eace2'
          '674282245d8ab2e09017b8f8cdce20a3ff81e631')
groups=('base')
conflicts=('procps' 'sysvinit-tools' 'sysctl-default-conf')
replaces=('procps' 'sysvinit-tools' 'sysctl-default-conf')
provides=('procps' 'sysvinit-tools')
install=procps-ng.install
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

prepare() {
	cd "${srcdir}/procps-ng-${pkgver}"
	patch -p1 -i ../impossibly-high-memory.patch
	sed 's:<ncursesw/:<:g' -i watch.c
}

build() {
	cd "${srcdir}/procps-ng-${pkgver}"

	./configure \
		--prefix=/usr \
		--exec-prefix=/ \
		--sysconfdir=/etc \
		--libdir=/usr/lib \
		--bindir=/usr/bin \
		--sbindir=/usr/bin \
		--enable-watch8bit \
		--disable-kill \
		--without-systemd
	make
}

package() {
	cd "${srcdir}/procps-ng-${pkgver}"

	make DESTDIR="${pkgdir}" install
	install -Dm644 "sysctl.conf" "$pkgdir/etc/sysctl.conf"

}
