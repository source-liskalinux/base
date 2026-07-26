# PKGBUILD For Liska Base Systems

# Contributor: Janorovic Volkov <janorovicvolkov@gmail.com>
# Maintainer: Janorovic Volkov <janorovicvolkov@gmail.com>

pkgname=base
pkgver=1.0.0
pkgrel=1
pkgdesc="Liska Base Systems"
arch=('x86_64')
license=('General Public License v3 or Later')
depends=('lkpm')
options=('!strip' '!debug')

package() {
    lkpm -i --root="${pkgdir}" bash bzip2 coreutils file filesystem findutils gawk gcc-libs gettext glibc grep gzip iproute2 iputils licenses lkpm lkchroot pciutils procps-ng psmisc sed shadow systemd systemd-sysvcompat tar util-linux xz --noconfirm
    rm -f "${pkgdir}/.MTREE"
    rm -f "${pkgdir}/.INSTALL"
    rm -f "${pkgdir}/.BUILDINFO"
    rm -f "${pkgdir}/var/lib/lkpm/db.json"
    rm -rf "${pkgdir}/var/cache/lkpm"
}