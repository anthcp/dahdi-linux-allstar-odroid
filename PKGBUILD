# Maintainer : Xavier Devlamynck <magicrhesus@ouranos.be>
# Contributor: Jonathan Liu <net147@gmail.com>
# Contributor: VK2ACP <anthcp@gmail.com>

pkgname=dahdi-allstar
pkgver=2.9.1.1
pkgver_tools=2.9.1
pkgrel=1
pkgdesc="DAHDI drivers for Asterisk with allstar mods"
arch=('armv7h')
url="http://www.asterisk.org/"
license=('GPL2')
depends=('linux' 'libusb' 'perl' 'alsa-lib' 'alsa-oss')
makedepends=('binutils' 'autoconf' 'linux-headers')
conflicts=('zaptel')
install="${pkgname}.install"
source=("http://downloads.asterisk.org/pub/telephony/dahdi-linux-complete/releases/dahdi-linux-complete-${pkgver}+${pkgver_tools}.tar.gz"
        "Makefile.patch"
        "dahdi-allstar.service"
	"dahdi-allstar.patch"
	"dahdi-kernel.patch"
	"allstar.conf")
sha1sums=('8a1b99aec5fb5b05f443aba8ce96d732703ee67b'
          '2c32963f71423a3591602b1863c714d92e2afcc5'
          'd37e37c67726cc64ce8b668217db625e2e9d9e9e'
          '9489be6115ff3ce9d1154ce94e35038815b2dcf2'
          '1cccdfdbad84f1bb791d3961fd659cb7b0259677'
          '256db4f27f9ddd40e18f860e59d744f99e4bf94d')
build() {
  cd "${srcdir}/dahdi-linux-complete-${pkgver}+${pkgver_tools}"
  patch -p0 -i "${srcdir}/Makefile.patch" "${srcdir}/dahdi-linux-complete-${pkgver}+${pkgver_tools}/Makefile"
  patch -p1 -i "${srcdir}/dahdi-allstar.patch"
  patch -p1 -i "${srcdir}/dahdi-kernel.patch"
  make DESTDIR="${pkgdir}" all
}

package() {
  cd "${srcdir}/dahdi-linux-complete-${pkgver}+${pkgver_tools}"
  make DYNFS=1 DESTDIR="${pkgdir}" install
  mkdir "${pkgdir}/etc/modules-load.d"
  cp "${srcdir}/allstar.conf" "${pkgdir}/etc/modules-load.d/allstar.conf"
}
# vim:set ts=2 sw=2 et:
