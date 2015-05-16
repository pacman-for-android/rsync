
pkgname=rsync
pkgver=3.1.1
pkgrel=4
pkgdesc="A file transfer program to keep remote files in sync"
arch=('i686' 'x86_64')
url="http://rsync.samba.org/"
license=('GPL3')
depends=('perl' 'popt' 'acl' 'zlib')
backup=('etc/rsyncd.conf' 'etc/xinetd.d/rsync')
source=("http://rsync.samba.org/ftp/rsync/$pkgname-$pkgver.tar.gz"
        "http://rsync.samba.org/ftp/rsync/$pkgname-$pkgver.tar.gz.asc"
        'rsyncd.conf' 'rsync.xinetd' 'rsyncd.service'
        'rsyncd.socket' 'rsyncd@.service')
md5sums=('43bd6676f0b404326eee2d63be3cdcfe'
         'SKIP'
         'bce64d122a8e0f86872a4a21a03bc7f3'
         'ea3e9277dc908bc51f9eddc0f6b935c1'
         'f90ba7f3717028769d6f230a2402b5aa'
         'ae4c381e0c02d6132c7f6ded3f473041'
         '53f94e613e0bc502d38dd61bd2cd7636')
validpgpkeys=('0048C8B026D4C96F0E589C2F6C859FB14B96A8C5')

build() {
	cd "$srcdir/$pkgname-$pkgver"
	./configure --prefix=/usr \
		--with-included-popt=no \
		--disable-debug
	make
}

check() {
	cd "$srcdir/$pkgname-$pkgver"
	make test
}

package() {
	cd "$srcdir/$pkgname-$pkgver"
	make DESTDIR="$pkgdir" install
	install -Dm644 ../rsyncd.conf "$pkgdir/etc/rsyncd.conf"
	install -Dm644 ../rsync.xinetd "$pkgdir/etc/xinetd.d/rsync"
	install -Dm644 ../rsyncd.service "$pkgdir/usr/lib/systemd/system/rsyncd.service"
	install -m644 ../rsyncd.socket "$pkgdir/usr/lib/systemd/system/rsyncd.socket"
	install -m644 ../rsyncd@.service "$pkgdir/usr/lib/systemd/system/rsyncd@.service"
	install -Dm755 support/rrsync "$pkgdir/usr/lib/rsync/rrsync"
}
