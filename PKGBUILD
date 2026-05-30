# Maintainer: sariaaskort@tuta.io
pkgname=(amf-amdgpu-pro)
pkgver=26.10
pkgrel=489
pkgdesc='AMD AMF Multimedia Library'
arch=(x86_64)
license=(custom)
url='https://www.amd.com/en/support/kb/release-notes/rn-amdgpu-unified-linux-22-40'
source_x86_64=("https://repo.radeon.com/amf/${pkgver}/rhel/10.0/packages/main/x86_64/amf-amdgpu-pro-${pkgver}.${pkgrel}-1.x86_64.rpm"  "https://repo.radeon.com/amf/${pkgver}/rhel/10.0/packages/main/x86_64/libamdenc-amdgpu-pro-${pkgver}.${pkgrel}-1.x86_64.rpm")
sha256sums_x86_64=(5f60239c785ebef1e14459af3569a362cf21078b8d4caf75be050d4dbf2867b2 38e476183b8b72de5f4cb18b20ceb5c353c4e7706c92f1a415fecc9681382244)

package() {
    mkdir -p ${pkgdir}/opt/amf/lib64

    for f in $(find opt/amf/lib64 -type f); do
        mv "$f" "$pkgdir"/opt/amf/lib64/;
    done

    for f in $(find opt/amf/lib64 -type l); do
        mv "$f" "$pkgdir"/opt/amf/lib64/;
    done

    mv opt/amf/share "$pkgdir"/opt/amf

    mkdir -p ${pkgdir}/etc/ld.so.conf.d/

    mv etc/ld.so.conf.d/libamdenc-amdgpu-pro-libs.conf ${pkgdir}/etc/ld.so.conf.d/

    mv opt/amf/vcn-check ${pkgdir}/opt/amf/
}

post_install() {
    ldconfig
}
