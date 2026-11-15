# Maintainer: Dario Banfi <hello@dariobanfi.com>

pkgname=anthropic-cli-bin
_pkgname=anthropic-cli
pkgver=2.9.0
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
sha256sums_x86_64=('69158f6a17e92e8e559e0061bea2530ac5b60976fb6d697673136d110ebe351f')
sha256sums_aarch64=('2bbccb2861c647cbad708d83921dfc3e0689233fc0f50be4745df3e973166cc9')
sha256sums_i686=('7569d39f60c439fad899ea00bc69ddbda2de2c04f7080421606a9476538ed927')
sha256sums_armv6h=('f52b7fc3e1be516c25c544488e51af69b97fffb749f2db3e7152479f14f43682')

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
