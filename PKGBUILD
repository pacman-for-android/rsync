# Maintainer: Angel Velasquez <angvp@archlinux.org> 
# Contributor: Eric Belanger <eric@archlinux.org>
# Contributor: Judd Vinet <jvinet@zeroflux.org>
# Contributor: Daniel J Griffiths <ghost1227@archlinux.us>
pkgname=rsync
pkgver=3.0.8
pkgrel=2
pkgdesc="A file transfer program to keep remote files in sync"
arch=('i686' 'x86_64')
url="http://samba.anu.edu.au/rsync/"
license=('GPL3')
depends=('acl')
backup=('etc/rsyncd.conf' 'etc/xinetd.d/rsync')
changelog=ChangeLog
source=(http://rsync.samba.org/ftp/rsync/${pkgname}-${pkgver}.tar.gz \
        rsyncd.conf rsyncd rsync.xinetd)
md5sums=('0ee8346ce16bdfe4c88a236e94c752b4'
         '4395c0591638349b1a7aeaaa4da1f03a'
         '7a9ce3b5de97f3aae29b906f93e1d157'
         'ea3e9277dc908bc51f9eddc0f6b935c1')
sha1sums=('10e80173c7e9ed8b8a4dc9e8fdab08402da5f08d'
          '48be09294134dfed888818872fe552a59c29147a'
          'eda623c31d9def454cf8e3e88dcf63de4ca5c08b'
          'fdb99785bc87ee13d77aa90dc1804f3f75dd7fc1')

build() {
	cd ${srcdir}/${pkgname}-${pkgver}
	./prepare-source 
	./configure --prefix=/usr --with-included-popt \
              --enable-acl-support --enable-xattr-support 
	make 
}

package() {
	cd ${srcdir}/${pkgname}-${pkgver}
	make DESTDIR=${pkgdir} install 
	install -Dm755 ../rsyncd ${pkgdir}/etc/rc.d/rsyncd 
	install -Dm644 ../rsyncd.conf ${pkgdir}/etc/rsyncd.conf 
	install -Dm644 ../rsync.xinetd ${pkgdir}/etc/xinetd.d/rsync 
}

