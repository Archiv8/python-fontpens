#!/bin/bash

# Created from the original PKGBUILD by Guillaume Horel <guillaume.horel@gmail.com> and William Turner <willtur.will@gmail.com>

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors

# Maintainer: Ross Clark <https://github.com/Archiv8/python-booleanoperations/discussions>
# Contributor: Ross Clark <https://github.com/Archiv8/python-booleanoperations/discussions>

# Upstream test suite has a circular dependency (it uses fontparts which in turn depends on this library) and thus cannot be run by default without blocking installation until first building without tests.
BUILDENV+=(!check)

_langname=python
_pacname=fontpens
_relname=fontPens

pkgname=${_langname}-${_pacname}
pkgver=0.2.4
pkgrel=3
pkgdesc='A collection of classes implementing the pen protocol for manipulating glyphs'
arch=(any)
url='https://github.com/robotools/fontpens'
license=(BSD)
depends=(
  "python-fonttools"
)
makedepends=(
  "python-setuptools"
)
checkdepends=(
  "python-fontparts"
  "python-pytest"
)
_zipname="${_relname}-${pkgver}"
source=(
  "https://files.pythonhosted.org/packages/source/${_relname::1}/${_relname}/${_zipname}.zip"
)
sha512sums=(
  '0155ab6d43d00ae14e325b93e4e40f3d240cd9ea13945e724a91054b5a6edd1a4a74f1244100b18aa8905029651080c930b3341aa881be970a2459f2a374e009'
)

build() {

  cd "${_zipname}"

  python setup.py build
}

check() {

  cd "${_zipname}"

  PYTHONPATH=Lib pytest Lib
}

package() {

  cd "${_zipname}"

  python setup.py install --root="${pkgdir}" --optimize=1 --skip-build

  install -Dm0644 -t "${pkgdir}/usr/share/licenses/${pkgname}/" LICENSE.txt
}
