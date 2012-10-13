
pkgname=rsync
pkgver=3.0.9
pkgrel=5
pkgdesc="A file transfer program to keep remote files in sync"
arch=('i686' 'x86_64')
url="http://samba.anu.edu.au/rsync/"
license=('GPL3')
depends=('perl')
backup=('etc/rsyncd.conf' 'etc/xinetd.d/rsync')
source=("http://rsync.samba.org/ftp/rsync/$pkgname-$pkgver.tar.gz"
        'rsyncd.conf' 'rsyncd' 'rsync.xinetd' 'rsyncd.service'
        'rsyncd.socket' 'rsyncd@.service')
md5sums=('5ee72266fe2c1822333c407e1761b92b'
         'bce64d122a8e0f86872a4a21a03bc7f3'
         'ba413da4ebca05c57860151fda21efbc'
         'ea3e9277dc908bc51f9eddc0f6b935c1'
         'ec96f9089d71109557cdcaa3f0633ed6'
         'ae4c381e0c02d6132c7f6ded3f473041'
         '53f94e613e0bc502d38dd61bd2cd7636')

build() {
	cd "$srcdir/$pkgname-$pkgver"
	./configure --prefix=/usr --with-included-popt
	make
}

check() {
	cd "$srcdir/$pkgname-$pkgver"
	make test
}

package() {
	cd "$srcdir/$pkgname-$pkgver"
	make DESTDIR="$pkgdir" install
	install -Dm755 ../rsyncd "$pkgdir/etc/rc.d/rsyncd"
	install -Dm644 ../rsyncd.conf "$pkgdir/etc/rsyncd.conf"
	install -Dm644 ../rsync.xinetd "$pkgdir/etc/xinetd.d/rsync"
	install -Dm644 ../rsyncd.service "$pkgdir/usr/lib/systemd/system/rsyncd.service"
	install -m644 ../rsyncd.socket "$pkgdir/usr/lib/systemd/system/rsyncd.socket"
	install -m644 ../rsyncd@.service "$pkgdir/usr/lib/systemd/system/rsyncd@.service"
	install -Dm755 support/rrsync "$pkgdir/usr/lib/rsync/rrsync"
}
