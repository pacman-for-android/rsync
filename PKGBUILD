# Maintainer: Eric Belanger <eric@archlinux.org>
# Contributor: Judd Vinet <jvinet@zeroflux.org>

pkgname=rsync
pkgver=3.0.3
pkgrel=1
pkgdesc="A file transfer program to keep remote files in sync"
arch=('i686' 'x86_64')
url="http://samba.anu.edu.au/rsync/"
license=('GPL3')
depends=('acl')
backup=('etc/rsyncd.conf' 'etc/xinetd.d/rsync')
source=(http://rsync.samba.org/ftp/rsync/${pkgname}-${pkgver}.tar.gz \
        rsyncd.conf rsyncd rsync.xinetd)
md5sums=('16d41aab9ece435198af222c5415a304' '4395c0591638349b1a7aeaaa4da1f03a'\
         '9de4d03d49f4b5c73ffd67d452716a49' 'ea3e9277dc908bc51f9eddc0f6b935c1')
sha1sums=('c12668eb888e386511299616f6972bec300ed346'
          '48be09294134dfed888818872fe552a59c29147a'
          'ebec275bbd0c11692c91dc59368349601bd9eaf4'
          'fdb99785bc87ee13d77aa90dc1804f3f75dd7fc1')

build() {
  cd ${srcdir}/${pkgname}-${pkgver}
  ./prepare-source || return 1
  ./configure --prefix=/usr --with-included-popt \
              --enable-acl-support --enable-xattr-support || return 1
  make || return 1
  make DESTDIR=${pkgdir} install || return 1
  install -D -m 755 ../rsyncd ${pkgdir}/etc/rc.d/rsyncd || return 1
  install -D -m 644 ../rsyncd.conf ${pkgdir}/etc/rsyncd.conf || return 1
  install -D -m 644 ../rsync.xinetd ${pkgdir}/etc/xinetd.d/rsync || return 1
}
