# PKGBUILD For Liska Base Systems

# Contributor: Janorovic Volkov <janorovicvolkov@gmail.com>
# Maintainer: Janorovic Volkov <janorovicvolkov@gmail.com>

pkgname=base
pkgver=1.0.0
pkgrel=1
pkgdesc="Liska Base Systems"
arch=('x86_64')
license=('General Public License v3 or Later')
depends=('bash' 'bzip2' 'coreutils' 'file' 'filesystem' 'findutils' 'gawk' 
         'gcc-libs' 'gettext' 'glibc' 'grep' 'gzip' 'iproute2' 'iputils' 
         'licenses' 'lkpm' 'lkchroot' 'pciutils' 'procps-ng' 'psmisc' 'sed' 
         'shadow' 'systemd' 'systemd-sysvcompat' 'tar' 'util-linux' 'xz' 
         'ca-certificates' 'nghttp3' 'nghttp2' 'openssl')
options=('!strip' '!debug')

package() {
    lkpm -i --root="${pkgdir}" ${depends[@]} --noconfirm
    rm -f "${pkgdir}"/.{MTREE,INSTALL,BUILDINFO}
    if [ -f "${pkgdir}/var/lib/lkpm/db.json" ]; then
        sed -i "s|${pkgdir}||g" "${pkgdir}/var/lib/lkpm/db.json"
    fi
    rm -rf "${pkgdir}/var/cache/lkpm"
}