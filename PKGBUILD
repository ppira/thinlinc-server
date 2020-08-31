# Maintainer: Cebtenzzre <cebtenzzre (at) gmail (dot) com>

pkgname=thinlinc-server
pkgver=4.12.0
pkgrel=1
pkgdesc="Cendio ThinLinc Linux remote desktop server"
arch=('i686' 'x86_64')
url="http://www.cendio.com/"
license=('custom')
install=${pkgname}.install
#depends=('python2' 'xorg-xauth'
#         'xdg-utils' 'hicolor-icon-theme')
optdepends=('nfs-utils: Local drive redirection'
            'python2-ldap: LDAP integration tools'
            'pcsclite: Smartcard tunneling')
_archive_name=tl-${pkgver}-server
source=("${_archive_name}.zip::https://www.cendio.com/downloads/server/download.py"
        'LICENSE')
sha256sums=('7a2f5f34fe5067d3932c7231ae63571dad8a67aaf8323df695d49933b93825d2'
            '179583f1e2f61a9a75a99bbe8bb988e35a0216fc2ddcbd4c85ad8bdc70c3149e')

_extract_dir="extract"

build()
{
    cd "${srcdir}/${_archive_name}/packages"
    mkdir -p "${_extract_dir}"

    for rpm in *${CARCH}*rpm *noarch*rpm; do
        bsdtar -C "${_extract_dir}" -xf "${rpm}"
    done
}

package()
{
    cd "${srcdir}/${_archive_name}/packages/${_extract_dir}"
    cp -aR etc/ opt/ usr/ var/ "$pkgdir"

    install -dm755 "$pkgdir"/usr/lib
    cp -aR lib64/* "$pkgdir"/usr/lib

    cd "$srcdir"
    install -Dm644 LICENSE             "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
