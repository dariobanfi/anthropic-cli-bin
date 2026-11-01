# Maintainer: Dario Banfi <hello@dariobanfi.com>

pkgname=anthropic-cli-bin
_pkgname=anthropic-cli
pkgver=2.4.0
pkgrel=1
pkgdesc="The official CLI for the Claude API (ant)"
arch=('x86_64' 'aarch64' 'i686' 'armv6h')
url="https://github.com/anthropics/anthropic-cli"
license=('MIT')
provides=("$_pkgname=$pkgver")
conflicts=("$_pkgname" 'ant')
options=('!strip' '!debug')

_relurl="$url/releases/download/v$pkgver"

source=("LICENSE-$pkgver::https://raw.githubusercontent.com/anthropics/$_pkgname/v$pkgver/LICENSE")
source_x86_64=("$_pkgname-$pkgver-x86_64.tar.gz::$_relurl/ant_${pkgver}_linux_amd64.tar.gz")
source_aarch64=("$_pkgname-$pkgver-aarch64.tar.gz::$_relurl/ant_${pkgver}_linux_arm64.tar.gz")
source_i686=("$_pkgname-$pkgver-i686.tar.gz::$_relurl/ant_${pkgver}_linux_386.tar.gz")
source_armv6h=("$_pkgname-$pkgver-armv6h.tar.gz::$_relurl/ant_${pkgver}_linux_armv6.tar.gz")

sha256sums=('7fc343be7ec189b803c1872267cbaf0381b12ffdb22d972b8ea7b21b262ba563')
sha256sums_x86_64=('45434d2721f801638340cc6f12277af32791c8cf3707134f690557e58a14d447')
sha256sums_aarch64=('88cc2d3d582e20a5aa17234f2409596a70b5e8afd6a35372d6a784e7a708c5a3')
sha256sums_i686=('ae0e08c0f6bf7964c59300b23c6ddb10b2feb5da87195a2ec14a58734eee9a30')
sha256sums_armv6h=('1e7973a00a6040fae56aba06930c33aa89910e491c5e1db68aff2bafa1079f09')

package() {
	install -Dm755 "$srcdir/ant" "$pkgdir/usr/bin/ant"

	# Completions are sourced, not executed; drop upstream's shebangs so they
	# are not mistaken for scripts requiring bash/fish at runtime.
	sed '1{/^#!/d}' "$srcdir/completions/ant.bash" |
		install -Dm644 /dev/stdin "$pkgdir/usr/share/bash-completion/completions/ant"
	sed '1{/^#!/d}' "$srcdir/completions/ant.fish" |
		install -Dm644 /dev/stdin "$pkgdir/usr/share/fish/vendor_completions.d/ant.fish"
	install -Dm644 "$srcdir/completions/ant.zsh" \
		"$pkgdir/usr/share/zsh/site-functions/_ant"

	install -Dm644 "$srcdir/man/man1/ant.1.gz" \
		"$pkgdir/usr/share/man/man1/ant.1.gz"

	install -Dm644 "$srcdir/LICENSE-$pkgver" \
		"$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
