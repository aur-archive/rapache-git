# Maintainer:       Aleksandar Blagotić <aca.blagotic_at_gmail.com>
# Based on work by: Florian Breitwieser <florian.bw_at_gmail.com>

pkgname=rapache-git
pkgver=20121121
pkgrel=1
pkgdesc="R embedded inside Apache"
arch=('i686' 'x86_64')
url="https://github.com/jeffreyhorner/rapache"
license=('Apache License Version 2.0')
depends=('apache' 'r' 'perl-libapreq2')
makedepends=('git' 'make')
install="$pkgname.install"
conflicts=('rapache')

_gitroot="git://github.com/jeffreyhorner/rapache.git"

build() {
  cd "$srcdir"

  if [ -d $pkgname ]; then
    cd $pkgname && git pull origin master
  else
    git clone $_gitroot $pkgname
  fi
}

package() {
  cd "$srcdir/$pkgname"

  ./configure --with-R=$(which R) --with-apache2-apxs=$(which apxs) --with-
  make || return 1
  install -m 755 -D .libs/mod_R.so $pkgdir/etc/httpd/modules/mod_R.so || return 1
}
