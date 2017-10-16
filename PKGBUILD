
pkgname=rsync
pkgver=3.1.2
pkgrel=5
pkgdesc="A file transfer program to keep remote files in sync"
arch=('i686' 'x86_64')
url="https://rsync.samba.org/"
license=('GPL3')
depends=('perl' 'popt' 'acl')
backup=('etc/rsyncd.conf' 'etc/xinetd.d/rsync')
validpgpkeys=('0048C8B026D4C96F0E589C2F6C859FB14B96A8C5') # Wayne Davison <wayned@users.sourceforge.net>
source=("https://rsync.samba.org/ftp/rsync/$pkgname-$pkgver.tar.gz"{,.asc}
        'rsyncd.conf'
        'rsync.xinetd'
        'rsyncd.service'
        'rsyncd.socket'
        'rsyncd@.service')
sha256sums=('ecfa62a7fa3c4c18b9eccd8c16eaddee4bd308a76ea50b5c02a5840f09c0a1c2'
            'SKIP'
            '733ccb571721433c3a6262c58b658253ca6553bec79c2bdd0011810bb4f2156b'
            'da0ec9ce07bf2edafbc8e44020da29a58038b00c3048a22de57017c56318a767'
            'c6998eaa5f3baa0e02830c182acacbb966187c428f8e42eab087f681f8e3d0a6'
            '551f17407de0e539c8419fc2cd48dd0124eb0253a186690b165b51703ffad1a5'
            '53e9e2546a74ce622f4eabc5590662fc2d0b06467f71f95428ab7926ea7e24c4')

build() {
	cd "$srcdir/$pkgname-$pkgver"

	# rsync requires the bundled zlib to support old-style --compress
	./configure --prefix=/usr \
		--with-included-popt=no \
		--with-included-zlib=yes \
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
