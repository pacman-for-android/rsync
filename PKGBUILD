# Maintainer: Christian Hesse <mail@eworm.de>
# Maintainer: T.J. Townsend <blakkheim@archlinux.org>

pkgname=rsync
_tag='b13e7a8ef4fa430223f66403506fb821caae5cfd' # git rev-parse v${pkgver}
pkgver=3.2.7
pkgrel=4.1
pkgdesc='A fast and versatile file copying tool for remote and local files'
arch=('x86_64' 'aarch64')
url='https://rsync.samba.org/'
license=('GPL3')
depends=('acl' 'libacl.so' 'lz4' 'openssl' 'popt' 'xxhash' 'libxxhash.so'
         'zlib' 'zstd')
optdepends=('python: for rrsync')
makedepends=('git')
backup=('data/etc/rsyncd.conf'
        'data/etc/xinetd.d/rsync')
validpgpkeys=('0048C8B026D4C96F0E589C2F6C859FB14B96A8C5') # Wayne Davison <wayned@users.sourceforge.net>
source=("git+https://github.com/WayneD/rsync#tag=${_tag}?signed"
        'rsyncd.conf')
sha256sums=('SKIP'
            '733ccb571721433c3a6262c58b658253ca6553bec79c2bdd0011810bb4f2156b')

_backports=(
)

_reverts=(
)

prepare() {
  cd ${pkgname}

  local _c
  for _c in "${_backports[@]}"; do
    if [[ $_c == *..* ]]; then
      git log --oneline --reverse "${_c}"
    else
      git log --oneline -1 "${_c}"
    fi
    git cherry-pick -n -m1 "${_c}"
  done
  for _c in "${_reverts[@]}"; do
    git log --oneline -1 "${_c}"
    git revert -n "${_c}"
  done
  sed -i '1s|.*|#!/data/usr/bin/sh|' prepare-source install-sh mkgitver cmd-or-msg
}

build() {
  cd ${pkgname}

  ./configure \
    --prefix=/data/usr \
    --sysconfdir=/data/etc \
    --disable-debug \
    --disable-md2man \
    --with-rrsync \
    --with-included-popt=no \
    --with-included-zlib=no
  make
}

check() {
  cd ${pkgname}

  make test
}

package() {
  cd ${pkgname}

  make DESTDIR="$pkgdir" SHELL=/data/usr/bin/sh install
  install -Dm0644 ../rsyncd.conf "$pkgdir/data/etc/rsyncd.conf"
  install -Dm0644 packaging/lsb/rsync.xinetd "$pkgdir/data/etc/xinetd.d/rsync"
  install -Dm0644 packaging/systemd/rsync.service "$pkgdir/data/usr/lib/systemd/system/rsyncd.service"
  install -Dm0644 packaging/systemd/rsync.socket "$pkgdir/data/usr/lib/systemd/system/rsyncd.socket"
  install -Dm0644 packaging/systemd/rsync@.service "$pkgdir/data/usr/lib/systemd/system/rsyncd@.service"
}
