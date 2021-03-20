# Maintainer: Harpo Roeder <roederharpo@protonmail.ch>

pkgname='ebpfsnitch'
pkgver=0.1.0
pkgrel=1
pkgdesc='eBPF based Application Firewall'
arch=('x86_64')
license=('BSD3')

provides=('ebpfsnitch' 'ebpfsnitchd')

depends=(
    'cmake'
    'clang'
    'bpf'
    'libbpf'
    'libnetfilter_queue'
    'spdlog'
    'boost'
    'libmnl'
    'nlohmann-json'
    'python3'
    'python-pyqt5'
    'conntrack-tools'
)

source=("https://github.com/harporoeder/ebpfsnitch/archive/refs/tags/$pkgver.tar.gz")
sha256sums=('7e9a8cc5d15afdeb5f87e904c9e5406d5bef1d1de51601b577d2fc83de5c19ab')

build() {
    cd "$srcdir/ebpfsnitch-$pkgver"
    mkdir build && cd build
    cmake -D CMAKE_INSTALL_PREFIX="/usr/bin" ..
    make
}

package() {
    cd "$srcdir/ebpfsnitch-$pkgver/build"
    make DESTDIR="$pkgdir/" install
    cd "$srcdir/ebpfsnitch-$pkgver/ui"
    python setup.py install --root="$pkgdir/"
    cd "$srcdir/ebpfsnitch-$pkgver"
    install -Dm644 ebpfsnitchd.service -t "$pkgdir/usr/lib/systemd/system"
}
