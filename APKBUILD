# Reference: <https://postmarketos.org/vendorkernel>
# Kernel config based on: arch/arm64/configs/(CHANGEME!)

pkgname=linux-xiaomi-raphael
pkgver=5.19.0
pkgrel=0
pkgdesc="Xiaomi Redmi K20 Pro kernel fork"
arch="aarch64"
_carch="arm64"
_flavor="xiaomi-raphael"
url="https://kernel.org"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native"
makedepends="
	bash
	bc
	bison
	devicepkg-dev
	flex
	openssl-dev
	perl
	
"

# Source
_repository="linux"
 _commit="70a6ca9dc4910fe03a7be3473c907901168822b0"
_config="config-$_flavor.$arch"
source="
	$pkgname-$_commit.tar.gz::https://github.com/sm8150-mainline/$_repository/archive/$_commit.tar.gz
	$_config
"
builddir="$srcdir/$_repository-$_commit"
_outdir="out"

prepare() {
	default_prepare
	REPLACE_GCCH=0
	. downstreamkernel_prepare
}

build() {
	unset LDFLAGS
	make  -j4 O="$_outdir" ARCH="$_carch" CC="${CC:-gcc}" \
		KBUILD_BUILD_VERSION="$((pkgrel + 1 ))-postmarketOS"
}

package() {
	downstreamkernel_package "$builddir" "$pkgdir" "$_carch" \
		"$_flavor" "$_outdir"
}

sha512sums="
2b49193c6768ea666d7cf13d870199dd6acd37a64ada5555eae544c87d240c3fa55a94e8aa2debfee91f3670eec02eb41516fe348fd862ba0f25cd6559d60f47  linux-xiaomi-raphael-253c17d93abaca5d4a3269a72588f547b4b81339.tar.gz
e7398c88b47fc78bf2e237f3b37ef88dc6f1c29bbd9b8c504dbfe1933098a8b260ce80f99b1761c6133e1ed8d0668858961ceacc87f506df79a15e1184fa0e69  config-xiaomi-raphael.aarch64
"
