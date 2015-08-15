# Contributor: Kamil Stachowski <kamil.stachowski@gmail.com>

pkgname=fuzzytime
pkgver=0.7.7
pkgrel=1
pkgdesc="A clock and timer that tell the time in a more human way (the 'ten past six'-style)"
url='http://github.com/caminoix/fuzzytime/tree/master'
arch=('i686' 'x86_64')
license=('GPL')
depends=('ghc' 'haskell-cmdargs')
makedepends=('git')
optdepends=('alsa-utils: sound support')
provides=('fuzzytime')
conflicts=()
replaces=()
source=()
md5sums=()

_gitroot='git://github.com/caminoix/fuzzytime.git'

build() {
	msg "Connecting to Git server..."
	if [ -d "$srcdir/$pkgname" ]; then
		cd "$srcdir/$pkgname" && git pull origin || return 1
	else
		git clone "$_gitroot" || return 1
	fi
	msg "Git checkout done or server timeout"
	cd "$srcdir/$pkgname"
	runhaskell Setup.hs configure --prefix=/usr --docdir=/usr/share/doc/$pkgname -O
	runhaskell Setup.hs build
}

package() {
	cd "$srcdir/$pkgname"
	runhaskell Setup.hs copy --destdir=${pkgdir}
	install -D -m644 src/fuzzytime.1 "$pkgdir/usr/share/man/man1/fuzzytime.1"
	install -D -m644 src/sound.wav "$pkgdir/usr/share/fuzzytime/sound.wav"
}
