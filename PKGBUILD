# Maintainer: Roger Coll <rogercoll at protonmail dot com>

pkgname=otelcol-contrib
pkgver=0.145.0
pkgrel=1
pkgdesc="OpenTelemetry Collector Contrib distribution"
arch=('x86_64')
url="https://github.com/open-telemetry/opentelemetry-collector-contrib"
license=('APACHE')
groups=('open-telemetry')
makedepends=(
    go
    git
    systemd
)
backup=(
    etc/$pkgname/$pkgname.yaml
    etc/$pkgname/$pkgname.conf
    etc/$pkgname/config.yaml
)
install=$pkgname.install
source=("${pkgname}-${pkgver}.tar.gz::$url/archive/refs/tags/v${pkgver}.tar.gz"
    "$pkgname.service"
    "$pkgname.conf"
    "config.yaml"
    "enable-cgo-netcgo.patch"
)
sha512sums=('519e6f3f75fc8a7ebbd44ab46c5649a2fd939864dac5b594d4e689ca889e6a1138a6b74b9c76a072032a0b6362c05af42689e1fe5dae0939d79a4d8d6f7f5f5b'
            'fb92f18756b964add1f24fe5f69a5a9f8ca68424304c99b65b6d0809a51f8389e42be36df3d8277abd53072074a176c1b65b038d3208c44adf067d27e8fdf578'
            'cc316fc0df97be7872813281564de1041f82febd45b827b8d03e0588dcbeaf6760beca22c9b2c80a449125be463b10125a6038233d1976056757f05f03ac117a'
            'b58d73af1224b99ba9e9c8d7bd41e44f6d551612e1fc9dfc182b8c05d7fa80e23e9c5f74a4429c0d983ca6389e3eb1a22733d94ece6b4f0f1839a571ab73fd1d'
            'a5853cfcc966b68df59ae6273a1c8a87cc36a401929452c152e9abb0a30d2d99cced36707b9a8f8b98293c88a3f1552c0f5bfb31e0766ce6396c9e0811e4d111')

prepare() {
    cd "opentelemetry-collector-contrib-$pkgver"
    patch -p1 -i "${srcdir}/enable-cgo-netcgo.patch"
}

build() {
	cd "opentelemetry-collector-contrib-$pkgver"
        make otelcontribcol SRC_ROOT=${PWD}
}


package() {
    install -Dm644 $pkgname.service "$pkgdir/usr/lib/systemd/system/$pkgname.service"
    install -Dm644 $pkgname.conf "$pkgdir/etc/$pkgname/$pkgname.conf"
    install -Dm644 config.yaml "$pkgdir/etc/$pkgname/config.yaml"
    cd "opentelemetry-collector-contrib-$pkgver"
    install -Dm755 bin/otelcontribcol_linux_amd64 "$pkgdir/usr/bin/$pkgname"
}
