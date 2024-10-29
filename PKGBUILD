# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Johannes Löthberg <johannes@kyriasis.com>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=imagesize
pkgname="${_py}-${_pkg}"
pkgver=1.4.1
pkgrel=5
_pkgdesc=(
  'Analyzes JPEG/JPEG 2000/PNG/GIF/TIFF/SVG/Netpbm/WebP'
  'image headers and returns image size or DPI'
)
pkgdesc="${_pkgdesc[*]}"
_http="https://github.com"
_ns="shibukawa"
url="${_http}/${_ns}/${_pkg}_py"
arch=(
  'any'
)
license=(
  'MIT'
)
depends=(
  'python'
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-wheel"
)
_pypi="https://files.pythonhosted.org/packages/source"
source=(
  "${_pypi}/${_pkg::1}/${_pkg}/${_pkg}-${pkgver}.tar.gz"
)
sha256sums=(
  '69150444affb9cb0d5cc5a92b3676f0b2fb7cd9ae39e947a5e11a36b4497cd4a'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --skip-dependency-check \
    --no-isolation
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      unittest \
        discover \
        -v
}

package() {
  local \
    _site_packages
  _site_packages=$( \
    "${py}" \
      -c \
        "import site; print(site.getsitepackages()[0])")
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  # Symlink license file
  install \
    -d \
      "${pkgdir}/usr/share/licenses/${pkgname}"
  ln \
    -s \
    "${_site_packages}/${_pkg}-${pkgver}.dist-info/LICENSE.rst" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.rst"
}
