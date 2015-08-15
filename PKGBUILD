# Maintainer: Andre Bartke

_gccver=4.4.2

pkgname=bcc
pkgver=1.0.45
pkgrel=1
pkgdesc="Gaisler BCC cross-compiler for SPARC V8 LEON processors"
arch=('i686' 'x86_64')
url="http://www.gaisler.com/index.php/products/operating-systems/bcc"
license=('GPL')
options=('!strip')
conflicts=("bcc-dev")
source=("http://gaisler.com/anonftp/bcc/bin/linux/sparc-elf-${_gccver}-${pkgver}.tar.bz2")

if test "$CARCH" == x86_64; then
	depends=("lib32-zlib")
	optdepends=("lib32-ncurses: gdb"
	            "lib32-libx11: gdb")
else
	depends=("zlib")
	optdepends=("ncurses: gdb"
	            "libx11: gdb")
fi

package() {
	mkdir -p $pkgdir/usr/lib/cross-sparc-unknown-elf
	cp -r $srcdir/sparc-elf-$_gccver/* $pkgdir/usr/lib/cross-sparc-unknown-elf

	msg "Cleaning-up cross compiler tree..."
	rm -rf ${pkgdir}/usr/lib/cross-sparc-unknown-elf/{info,man}

	msg "Creating out-of-path executables..."
	mkdir -p ${pkgdir}/usr/lib/cross-sparc-unknown-elf/sparc-elf/bin/
	rm -f ${pkgdir}/usr/lib/cross-sparc-unknown-elf/sparc-elf/bin/*
	cd ${pkgdir}/usr/lib/cross-sparc-unknown-elf/sparc-elf/bin/
	for bin in ${pkgdir}/usr/lib/cross-sparc-unknown-elf/bin/sparc-elf-*; do
		bbin=`basename "$bin"`;
		ln -s "/usr/lib/cross-sparc-unknown-elf/bin/${bbin}" `echo "$bbin" | sed "s#^sparc-elf-##"`;
	done

	msg "Creating /usr/bin symlinks..."
	mkdir -p $pkgdir/usr/bin
	for bin in ${pkgdir}/usr/lib/cross-sparc-unknown-elf/bin/sparc-elf-*; do
		bbin=`basename "$bin"`;
		ln -s "/usr/lib/cross-sparc-unknown-elf/bin/${bbin}" "${pkgdir}/usr/bin/${bbin}";
	done
}

md5sums=('b6bb73190563e567d42f69fa931c1880')

# vim: set noet ci pi sts=0 sw=4 ts=4:
