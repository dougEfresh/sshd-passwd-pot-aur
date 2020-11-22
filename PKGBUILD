# Maintainer: "Douglas Chimento" dougEfresh
pkgname=sshd-passwd-pot
pkgver=8.4.1p1
pkgrel=1
epoch=1
pkgdesc="${pkgname}"
arch=('any')
url="https://github.com/dougEfresh/dougEfresh/${pkgname}"
license=('custom')
options=('!strip')
source=("git+https://github.com/dougEfresh/${pkgname}.git#tag=v$pkgver" ${pkgname}.service)
sha256sums=('SKIP' 'SKIP')
depends=('glibc' 'krb5' 'openssl' 'libedit' 'ldns' 'libxcrypt' 'libcrypt.so' 'zlib' 'json-c')
makedepends=('libfido2' 'json-c')
checkdepends=('inetutils')
install=$pkgname.install

prepare() {
	cd "${srcdir}/${pkgname}"
	autoreconf
}

build() {
	cd "${srcdir}/${pkgname}"
	./configure 	--prefix=/opt/${pkgname} \
		--disable-strip \
		--with-security-key-builtin \
		--with-ssl-engine \
		--with-privsep-user=nobody \
		--with-md5-passwords \
		--with-pid-dir=/run \
		--with-audit-passwd-url=yes \
		--with-default-path='/usr/local/sbin:/usr/local/bin:/usr/bin' 
	make -j $(nproc)
}

package() {
    cd "${srcdir}/${pkgname}"
    make DESTDIR="${pkgdir}" install
    cd "${srcdir}"
    install -Dm644 "${pkgname}".service -t ${pkgdir}/etc/systemd/system/
}





