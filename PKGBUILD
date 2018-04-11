# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://aur.archlinux.org/packages/procps-ng-nosystemd
# 						Maintainer: Alexey D. <lq07829icatm@rambler.ru>
# 						Contributor: Gaetan Bisson <bisson@archlinux.org>
# 						Contributor: Eric Bélanger <eric@archlinux.org>

pkgname=procps-ng
pkgver=3.3.13
pkgrel=2
pkgdesc='Utilities for monitoring your system and its processes'
url='https://gitlab.com/procps-ng/procps'
license=('GPL' 'LGPL')
arch=('x86_64')
depends=('ncurses')
backup=('etc/sysctl.conf')
source=("https://downloads.sourceforge.net/project/procps-ng/Production/procps-ng-${pkgver}.tar.xz"
       'sysctl.conf')
sha1sums=('295cd8381170b0948f4dd2978374716755873ae3'
          '674282245d8ab2e09017b8f8cdce20a3ff81e631')
groups=('base')
conflicts=('procps' 'sysvinit-tools')
replaces=('procps' 'sysvinit-tools')
provides=('procps' 'sysvinit-tools')
install=procps-ng.install
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

prepare() {
	cd $pkgname-$pkgver
	sed 's:<ncursesw/:<:g' -i watch.c
}

build() {
	cd  "$pkgname-$pkgver"
	
	./configure \
		--prefix=/usr \
		--exec-prefix=/ \
		--sysconfdir=/etc \
		--libdir=/usr/lib \
		--bindir=/usr/bin \
		--sbindir=/usr/bin \
		--enable-watch8bit \
		--disable-kill \
		--disable-modern-top \
		--without-systemd
	make
}

package() {
	cd  "$pkgname-$pkgver"

	make DESTDIR="${pkgdir}" install
	install -Dm644 "sysctl.conf" "$pkgdir/etc/sysctl.conf"

}
