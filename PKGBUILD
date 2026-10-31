# Maintainer: lev
# box-git - build the public box repository as a pacman package.
#
# This file is meant to live in its own AUR-style repo; it no longer
# builds the surrounding working tree. For local incremental installs use
# scripts/install-latest.sh in the box source repo instead (no full
# package rebuild).

pkgname=box-git
pkgver=r134.6c4ce56
pkgrel=1
pkgdesc='Booru client for local archives and online boorus (Qt6, git)'
arch=('x86_64')
url='https://git.lusosterone.net/lev/box'
license=('GPL-3.0-or-later')
depends=('qt6-base' 'qt6-multimedia' 'qt6-svg' 'qt6-webengine'
         'hicolor-icon-theme')
makedepends=('cmake' 'git' 'qt6-tools')
provides=('box')
conflicts=('box')
source=("$pkgname::git+https://git.lusosterone.net/lev/box.git")
sha256sums=('SKIP')

pkgver() {
	cd "$srcdir/$pkgname"
	if desc=$(git describe --long --tags --abbrev=7 2>/dev/null); then
		printf '%s' "$desc" |
			sed 's/^v//; s/\([^-]*-g\)/r\1/; s/-/./g'
	else
		printf 'r%s.%s' "$(git rev-list --count HEAD)" \
			"$(git rev-parse --short=7 HEAD)"
	fi
}

build() {
	cmake -B build -S "$srcdir/$pkgname" \
		-DCMAKE_BUILD_TYPE=Release \
		-DCMAKE_INSTALL_PREFIX=/usr
	cmake --build build -j"$(nproc)"
}

package() {
	DESTDIR="$pkgdir" cmake --install build
}
