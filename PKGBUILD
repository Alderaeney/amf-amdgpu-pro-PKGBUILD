# Maintainer: sariaaskort@tuta.io
DLAGENTS=("https::/usr/bin/curl -k -o %o %u")

pkgname=(amf-amdgpu-pro)
pkgver=25.20
pkgrel=399
pkgdesc='AMD AMF Multimedia Library'
arch=(x86_64)
license=(custom)
url='https://www.amd.com/en/support/kb/release-notes/rn-amdgpu-unified-linux-22-40'
depends=()
source_x86_64=("https://repo.radeon.com/amf/${pkgver}/ubuntu/pool/main/noble/${pkgname}_${pkgver}-${pkgrel}_amd64.deb"  "https://repo.radeon.com/amf/${pkgver}/ubuntu/pool/main/noble/libamdenc-amdgpu-pro_${pkgver}-${pkgrel}_amd64.deb")
sha256sums_x86_64=(3ed0507345840a9cc87cacf272ca40a0dcce82ff2b72e6e9cd6b10b9c80c9bd3 6d00f97e221d9c3cfbc9af912d6a1244a6a097858db5b232b830eab213c57b40)
noextract=(libamdenc-amdgpu-pro_${pkgver}-${pkgrel}_amd64.deb ${pkgname}_${pkgver}-${pkgrel}_amd64.deb)

# extracts a debian package
# $1: deb file to extract
extract_deb() {
    local tmpdir="$(basename "${1%.deb}")"
    rm -Rf "$tmpdir"
    mkdir "$tmpdir"
    cd "$tmpdir"
    ar x "$1"
    tar -C "${pkgdir}" -xf data.tar.xz
}

# move ubuntu specific /usr/lib/x86_64-linux-gnu to /usr/lib
# $1: debian package library dir (goes from opt/amdgpu or opt/amdgpu-pro and from x86_64 or i386)
# $2: arch package library dir (goes to usr/lib or usr/lib32)
move_libdir() {
    local deb_libdir="$1"
    local arch_libdir="$2"

    if [ -d "${pkgdir}/${deb_libdir}" ]; then
        if [ ! -d "${pkgdir}/${arch_libdir}" ]; then
            mkdir -p "${pkgdir}/${arch_libdir}"
        fi
        mv -t "${pkgdir}/${arch_libdir}/" "${pkgdir}/${deb_libdir}"/*
        find ${pkgdir} -type d -empty -delete
    fi
}

# move copyright file to proper place and remove debian changelog
move_copyright() {
    find ${pkgdir}/usr/share/doc -name "changelog.Debian.gz" -delete
    mkdir -p ${pkgdir}/usr/share/licenses/${pkgname}
    find ${pkgdir}/usr/share/doc -name "copyright" -exec mv {} ${pkgdir}/usr/share/licenses/${pkgname} \;
    find ${pkgdir}/usr/share/doc -type d -empty -delete
}

package() {
    pkgdesc="AMDGPU Pro Advanced Multimedia Framework"
    license=('custom: AMDGPU-PRO EULA')

    extract_deb "${srcdir}"/${pkgname}_${pkgver}-${pkgrel}_amd64.deb
    extract_deb "${srcdir}"/libamdenc-amdgpu-pro_${pkgver}-${pkgrel}_amd64.deb

    move_libdir "opt/amf/lib/x86_64-linux-gnu" "usr/lib"
    move_copyright
}
