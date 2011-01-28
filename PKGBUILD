# Maintainer: Angel Velasquez <angvp@archlinux.org> 
# Contributor: Eric Belanger <eric@archlinux.org>
# Contributor: Judd Vinet <jvinet@zeroflux.org>
# Contributor: Daniel J Griffiths <ghost1227@archlinux.us>
pkgname=rsync
pkgver=3.0.7
pkgrel=2
pkgdesc="A file transfer program to keep remote files in sync"
arch=('i686' 'x86_64')
url="http://samba.anu.edu.au/rsync/"
license=('GPL3')
depends=('acl')
backup=('etc/rsyncd.conf' 'etc/xinetd.d/rsync')
source=(http://rsync.samba.org/ftp/rsync/${pkgname}-${pkgver}.tar.gz \
        rsyncd.conf rsyncd rsync.xinetd)
md5sums=('b53525900817cf1ba7ad3a516ab5bfe9'
         '4395c0591638349b1a7aeaaa4da1f03a'
         '3d8f90ac8467ff6af28754584a61fd11'
         'ea3e9277dc908bc51f9eddc0f6b935c1')
sha1sums=('63426a1bc71991d93159cd522521fbacdafb7a61'
          '48be09294134dfed888818872fe552a59c29147a'
          '357af5648eb4ecf84cc6b1de1cd79d21eca3a518'
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

