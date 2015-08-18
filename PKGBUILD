pkgname=yabause-gtk-svn
pkgver=3106
pkgrel=1
pkgdesc="A Sega Saturn emulator. (svn)"
arch=(i686 x86_64)
license=("GPL")
depends=(gtkglext sdl freeglut mini18n-svn)
makedepends=(subversion)
url="http://yabause.org"
conflicts=(yabause yabause-qt yabause-qt-svn yabause-svn)
provides=(yabause)
replaces=(yabause-svn)
source=("svn+https://yabause.svn.sourceforge.net/svnroot/yabause/trunk/yabause"
"rwx.patch")
md5sums=(SKIP '2f6491ed2cbe88d78253617cfa68b22b')

pkgver() {
	cd "$SRCDEST/${pkgname%-gtk*}"
	svnversion
}

build() {
	cd "${srcdir}/${pkgname%-gtk*}"
	patch -Np1 -i "${srcdir}"/rwx.patch
	cmake \
		-DCMAKE_INSTALL_PREFIX=/usr \
		-DYAB_PORTS=gtk \
		-DYAB_NETWORK=ON \
		-DYAB_OPTIMIZED_DMA=on \
		-DYAB_PERKEYNAME=ON
	make
}

package() {
	cd "${srcdir}/${pkgname%-gtk*}"
	make DESTDIR="${pkgdir}" install
	install -Dm644 COPYING "$pkgdir/usr/share/licenses/yabause/COPYING"
}
