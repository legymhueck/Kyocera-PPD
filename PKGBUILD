pkgname=kyocera-ppds-ksl84
pkgver=8.4
pkgrel=1
# Supported printer models are listed in ppd-models.txt (one per line).
# Examples: FS-3900DN, Mita_FS-3820N, Mita_KM-5035.
pkgdesc="Kyocera Linux PPD collection (KSL 8.4)"
arch=('any')
url='https://www.kyoceradocumentsolutions.com/'
license=('custom')
depends=('cups')
makedepends=('libarchive')
source=('Linux_PPDs_KSL8_4.zip::https://www.kyoceradocumentsolutions.eu/content/dam/download-center-cf/eu/drivers/all/Linux_PPDs_KSL8_4_zip.download.zip')
noextract=('Linux_PPDs_KSL8_4.zip')
sha256sums=('5e79034c9f92d5b656dcbf8967ebdf2007e28f3fefad97b9e8215aa7ef673c60')

package() {
  local srcroot="${srcdir}/ppd-src"
  local ppdroot

  mkdir -p "${srcroot}"
  bsdtar -xf "${srcdir}/Linux_PPDs_KSL8_4.zip" -C "${srcroot}"

  ppdroot="$(find "${srcroot}" -mindepth 1 -maxdepth 1 -type d -name 'PPD*_KSL_8.4' | head -n 1)"
  if [[ -z "${ppdroot}" ]]; then
    echo "Unable to locate extracted PPD directory under ${srcroot}" >&2
    return 1
  fi

  while IFS= read -r -d '' ppd; do
    local rel
    rel="${ppd#${ppdroot}/}"
    install -Dm644 "${ppd}" "${pkgdir}/usr/share/ppd/kyocera/${rel}"
  done < <(find "${ppdroot}" -type f -iname '*.ppd' -print0 | sort -z)
}
