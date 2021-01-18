license=('GPL2+')
arch=('x86_64')
pkgname=privoxy
pkgver=3.0.29
pkgrel=1
ppkgdesc="Privoxy is a non-caching web proxy with advanced filtering capabilities for enhancing privacy, modifying web page data and HTTP headers, controlling access, and removing ads and other obnoxious Internet junk. Privoxy has a flexible configuration and can be customized to suit individual needs and tastes. It has application for both stand-alone systems and multi-user networks."
depends=()
makedepends=('autoconf' 'make')
url="http://www.privoxy.org/"
source=("${pkgname}-${pkgver}.tar.gz::http://www.privoxy.org/sf-download-mirror/Sources/${pkgver}%20%28stable%29/privoxy-${pkgver}-stable-src.tar.gz")
install=privoxy.install
md5sums=('SKIP')
privoxy_user_group=privoxy

build() {
  sudo useradd --no-create-home ${privoxy_user_group}

  cd privoxy-${pkgver}-stable

  autoheader
  autoconf

  ./configure \
    --prefix=/usr \
    --sysconfdir=/usr/etc/privoxy \
    --with-user=${privoxy_user_group} \
    --with-group=${privoxy_user_group} \
    --with-openssl
  make
}

package() {
  cd privoxy-${pkgver}-stable

  make DESTDIR=${pkgdir} install

  sudo userdel ${privoxy_user_group}
}
