# PKGBUILD For Liska Base Systems

# Contributor: Janorovic Volkov <janorovicvolkov@gmail.com>
# Maintainer: Janorovic Volkov <janorovicvolkov@gmail.com>

pkgname=base
pkgver=1
pkgrel=1
pkgdesc="Liska Base Systems Monolithic Bundle"
arch=('x86_64')
license=('General Public License v3 or Later')
depends=('bash' 'bzip2' 'coreutils' 'file' 'filesystem' 'findutils' 'gawk' 
         'gcc-libs' 'gettext' 'glibc' 'grep' 'gzip' 'iproute2' 'iputils' 
         'licenses' 'lkpm' 'lkchroot' 'pciutils' 'procps-ng' 'psmisc' 'sed' 
         'shadow' 'systemd' 'systemd-sysvcompat' 'tar' 'util-linux' 'xz' 
         'ca-certificates' 'ca-certificates-utils' 'openssl' 'libnghttp3' 
         'libnghttp2' 'libpsl' 'libidn2' 'brotli' 'busybox' 'cpio' 'nano'
         'inetutils' 'libverto' 'lkinit')
options=('!strip' '!debug')

package() {
    local queue=("${depends[@]}")
    local processed=()
    in_array() {
        local e match="$1"
        shift
        for e; do [[ "$e" == "$match" ]] && return 0; done
        return 1
    }
    echo "===> [INFO]: Resolving base system dependencies recursively..."
    while [ ${#queue[@]} -gt 0 ]; do
        local pkg="${queue[0]}"
        queue=("${queue[@]:1}")
        if [[ "$pkg" == *.so* ]]; then
            continue
        fi
        if in_array "$pkg" "${processed[@]}"; then
            continue
        fi
        echo "===> [INFO]: Installing core package into base bundle: ${pkg}"
        if lkpm -i --root="${pkgdir}" "$pkg" --noconfirm; then
            processed+=("$pkg")
        else
            echo "===> [ERR]: Failed to install $pkg, skipping..."
            continue
        fi
        local missing_deps
        missing_deps=$(lkpm -l "$pkg" --root="${pkgdir}" 2>/dev/null | grep "(missing)" | sed 's/>//g' | sed 's/(missing)//g' | awk '{print $1}')
        for dep in $missing_deps; do
            if [[ -n "$dep" && ! "$dep" == *.so* ]]; then
                if ! in_array "$dep" "${processed[@]}" && ! in_array "$dep" "${queue[@]}"; then
                    echo "  -> Found missing sub-dependency: $dep (adding to queue)"
                    queue+=("$dep")
                fi
            fi
        done
    done
    rm -f "${pkgdir}"/.{MTREE,INSTALL,BUILDINFO}
    if [ -f "${pkgdir}/var/lib/lkpm/db.json" ]; then
        sed -i "s|${pkgdir}||g" "${pkgdir}/var/lib/lkpm/db.json"
        mv "${pkgdir}/var/lib/lkpm/db.json" "${pkgdir}/var/lib/lkpm/db.base.json"
    fi
    rm -rf "${pkgdir}/var/cache/lkpm"
}