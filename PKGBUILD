# PKGBUILD For Liska Base Systems

# Contributor: Janorovic Volkov <janorovicvolkov@gmail.com>
# Maintainer: Janorovic Volkov <janorovicvolkov@gmail.com>

pkgname=base
pkgver=1.0.0
pkgrel=1
pkgdesc="Liska Base Systems"
arch=('x86_64')
license=('General Public License v3 or Later')
depend=('lkpm')
package() {
    sudo lkpm -i --root=${srcdir} bash bzip2 coreutils file filesystem findutils gawk gcc-libs gettext glibc grep gzip iproute2 iputils licenses lkpm lkchroot pciutils procps-ng psmisc sed shadow systemd systemd-sysvcompat tar util-linux xz --noconfirm
}
