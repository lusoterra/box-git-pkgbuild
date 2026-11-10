# Maintainer: Lev <lev@lusosterone.net>

pkgname=box-git
pkgver=r269.97dfba2
pkgrel=1
pkgdesc='Booru client for local archives and online boorus (Qt6, git)'
arch=('x86_64')
url='https://github.com/lusoterra/box'
license=('GPL-3.0-or-later')
depends=('qt6-base' 'qt6-multimedia' 'qt6-svg' 'qt6-webengine'
         'hicolor-icon-theme')
makedepends=('cmake' 'git' 'qt6-tools')
provides=('box')
conflicts=('box')
source=("$pkgname::git+https://github.com/lusoterra/box.git")
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
	cmake --build build
}

package() {
	DESTDIR="$pkgdir" cmake --install build
}
