# Maintainer: Christopher Arndt <aur -at- chrisarndt -dot- de>

pkgname='pigpio'
pkgver=500
pkgrel=1
pkgdesc="A C and Python library and system service for controlling GPIOs on a Raspberry Pi"
url="http://abyz.me.uk/rpi/pigpio/"
license=('custom:UNLICENSE')
arch=('i686' 'x86_64' 'aarch64' 'armv7h')
depends=('python')
provides=("python-${pkgname}")
conflicts=("python-${pkgname}")
source=("${pkgname}-${pkgver}.tar.gz")
sha256sums=('d6ac12c3d842eac01f06d43f21b5d55b3f0e1fdc805f47aecba111a4b91c54ee')
# source=("${pkgname}-${pkgver}.tar.gz::https://github.com/zrel/pigpio/blob/main/pigpio-${pkgver}.tar.gz")
# sha256sums=('07d8d5c0d16c1ef35e3c3d55ad1bfe2ee58853eba88b0ff62e8d3b1523d863a7')


prepare() {
  cd "${pkgname}-${pkgver}"
  sed -e 's/ -lrt//' -i Makefile
  sed -e 's/-Wl/\$(LDFLAGS)/' -i Makefile
  sed -e 's/\$(CC) -o/\$(CC) $(LDFLAGS) -o/' -i Makefile
  sed -e '/which python2/d' -i Makefile
  sed -e '/\/opt/d' -i Makefile
  sed -e 's|\$(prefix)/man|\$(prefix)/share/man|' -i Makefile
  sed -e 's|/usr/bin/pigpiod|/usr/bin/pigpiod -k|' -i util/pigpiod.service
}

build() {
  cd "${pkgname}-${pkgver}"
  make
}

package() {
  cd "${pkgname}-${pkgver}"
  make prefix=/usr DESTDIR="${pkgdir}" install
  install -Dm644 util/pigpiod.service -t "${pkgdir}/usr/lib/systemd/system"
  install -Dm644 UNLICENCE -t "${pkgdir}/usr/share/licenses//${pkgname}"
}
