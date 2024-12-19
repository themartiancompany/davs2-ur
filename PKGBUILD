# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Daniel Bermond <dbermond@archlinux.org>

# NOTE:
# 10-bit depth is not supported currently
# https://github.com/pkuvcl/davs2/blob/1.7/build/linux/configure#L470

_os="$( \
  uname \
    -o)"
_pkg=davs2
pkgname="${_pkg}"
pkgver=1.7
pkgrel=1
arch=(
  'x86_64'
  'i686'
  'arm'
  'aarch64'
  'armv7l'
  'armv6l'
  'mips'
  'powerpc'
  'pentium4'
)
pkgdesc='Open-Source decoder of AVS2-P2/IEEE1857.4 video coding standard'
_http="https://github.com"
_ns="pkuvcl"
url="${http}/${_ns}/${_pkg}"
license=(
  'GPL'
)
depends=(
)
if [[ "${_os}" == "GNU/Linux" ]]; then
  depends+=(
    "glibc"
  )
elif [[ "${_os}" == "Android" ]]; then
  depends+=(
    "ndk-sysroot"
  )
fi
makedepends=(
  'nasm'
)
provides=(
  "lib${_pkg}=${pkgver}"
)
conflicts=(
  "lib${_pkg}"
)
replaces=(
  "lib${_pkg}"
)
options=(
  '!lto'
)
source=(
  "${url}/archive/${pkgver}/${pkgname}-${pkgver}.tar.gz"
)
sha256sums=(
  'b697d0b376a1c7f7eda3a4cc6d29707c8154c4774358303653f0a9727f923cc8'
)

build() {
  local \
    _configure_opts=()
  _configure_opts=(
    --prefix='/usr'
    --enable-shared
    --disable-static
    --bit-depth='8'
    --chroma-format='all'
    --enable-pic
  )
  cd \
    "${_pkg}-${pkgver}/build/linux"
  ./configure \
    "${_configure_opts[@]}"
  make
}

package() {
  make \
    -C \
      "${_pkg}-${pkgver}/build/linux" \
    DESTDIR="${pkgdir}" \
    install-cli \
    install-lib-shared
}
