# Original PKGBUILD By: Bart De Vries <devriesb at gmail dot com>
# Contributor: Furkan Kardame <furkan@fkardame.com>
# Maintainer: Henning Thiemann <hthiemann@hthiemann.tech>

pkgname=chromium-docker
pkgdesc='Chromium Docker Image builder with widevine'
pkgver=4.10.1610.6
pkgrel=1
#list od current images https://dl.google.com/dl/edgedl/chromeos/recovery/recovery.conf
_chromeos_ver=12739.111.0
_chromeos_file="chromeos_${_chromeos_ver}_elm_recovery_stable-channel_mp-v2.bin"
_rootfs_img="ROOT-A.img"
_libwidevine="libwidevinecdm.so"
_docker_image="docker-chromium-armhf"
_commit=c135114b417f41fc6d1bce2ccb09845d1cd08e9c
arch=('aarch64')
url='https://www.widevine.com/'
license=('custom')
depends=('gcc-libs' 'glib2' 'glibc' 'nspr' 'nss' 'xorg-xhost' 'docker' 'git')
makedepends=('p7zip')
options=('!strip')
install=$pkgname.install
source=("chrome-eula_text.html::https://www.google.com/intl/en/chrome/privacy/eula_text.html"
        "https://dl.google.com/dl/edgedl/chromeos/recovery/chromeos_${_chromeos_ver}_elm_recovery_stable-channel_mp-v2.bin.zip"
        "${_docker_image}.zip::https://github.com/spikerguy/${_docker_image}/archive/${_commit}.zip"
        "chromium.png"
        "Chromium.desktop")
noextract=("${_chromeos_file}.zip")
sha256sums=('070fe30eb8a85cc3302c54aa8d14af4f'
            '46d7705abe7857ff7e48ef717b3b9c86'
            '0111c7d9dfbdd935aecdd7cde18ab508'
            'a2334d75c927fee54458b26bb8703734'
            '4e7e4f65cb3b95c8327dc103c36d92dd')
            
prepare() {
  #gcc ../get_cdm_version.c -o get_cdm_version -ldl
  7z e ../${_chromeos_file}.zip -y
  7z e ${_chromeos_file} ${_rootfs_img} -y
  7z e ${_rootfs_img} ${_libwidevine} -r -y
  cp ${_libwidevine} ${_docker_image}-${_commit}/widevine

 }

 package() {
    mkdir -p "${pkgdir}"/usr/share/chromium-docker/
    mkdir -p "${pkgdir}"/usr/share/applications/
  cp -r "${_docker_image}-${_commit}"/* -t "${pkgdir}/usr/share/chromium-docker"
  #install -Dm644 ${_libwidevine} -t "$pkgdir/usr/lib/chromium/"
  install -Dm644 ../chrome-eula_text.html "$pkgdir/usr/share/licenses/$pkgname/eula_text.html"
  install -Dm644 ../chrome-eula_text.html chromium.png "$pkgdir/usr/share/chromium-docker/"
  install -Dm644 Chromium.desktop "$pkgdir/usr/share/applications/"
}
 
