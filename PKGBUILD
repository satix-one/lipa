# Maintainer: Владислав Александрович Зубков <satix@...>
pkgname=lipa
pkgver=0.2.0
pkgrel=1
pkgdesc="Wayland screen translation tool using Quickshell"
arch=('x86_64')
url="https://github.com/satix-one/lipa"
license=('MIT')
depends=('quickshell' 'slurp' 'grim' 'tesseract' 'tesseract-data-rus' 'tesseract-data-eng')
makedepends=('cargo' 'rust')
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('SKIP')
options=('!lto' '!debug')

prepare() {
    cd "$pkgname-$pkgver"
    export RUSTUP_TOOLCHAIN=stable
    cargo fetch --target "$(rustc -vV | grep host | cut -d' ' -f2)"
}

build() {
    cd "$pkgname-$pkgver"
    export RUSTUP_TOOLCHAIN=stable
    export CARGO_TARGET_DIR=target
    cargo build --release --frozen
}

package() {
    cd "$pkgname-$pkgver"
    # Ставим бинарник
    install -Dm755 "target/release/lipa" "$pkgdir/usr/bin/lipa"
    # Ставим QML-файл в системную папку
    install -Dm644 "lipa.qml" "$pkgdir/usr/share/lipa/lipa.qml"
}
