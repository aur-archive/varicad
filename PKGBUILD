#!/bin/bash

# Maintainer: titep <alex.foster-30go6gp@yopmail.com>
pkgname=varicad
_pkgname=varicad2015
pkgver=2015.2.02
_pkgver=${pkgver#*.}
pkgrel=1
pkgdesc="VariCAD -- 3D&2D CAD system"
arch=('i686' 'x86_64')
url="http://www.varicad.com"
license=('unknown')
depends=('hicolor-icon-theme' 'mesa' 'gtk2' 'desktop-file-utils' 'xdg-utils')
backup=('opt/VariCAD/lib/varicad.lck')
install=$pkgname.install
source=($pkgname-$pkgver.tar.gz)

case $CARCH in
  i686)
    source=("http://www.varicad.com/userdata/files/release/en/${_pkgname}-en_${_pkgver}_i386.deb")
    _pkgname1=${_pkgname}-en_${_pkgver}_i386.deb
md5sums=('c53928ea0154ee2fd9b67886c0b493d3')
    ;;
  x86_64)
    source=("http://www.varicad.com/userdata/files/release/en/${_pkgname}-en_${_pkgver}_amd64.deb")
    _pkgname1=${_pkgname}-en_${_pkgver}_amd64.deb
md5sums=('58d1df8e7d3999fb3c9de8926838c15b')
    ;;
esac
noextract=(${_pkgname1})

package() {
  cd "$srcdir" || return 1
  ar p ${_pkgname1} data.tar.gz | tar zx || return 1
  tar -c opt | tar -x -C ${pkgdir} || return 1
  tar -c usr | tar -x -C ${pkgdir} || return 1

  if [ ! -f ${pkgdir}/opt/VariCAD/lib/varicad.lck ]; then
	touch ${pkgdir}/opt/VariCAD/lib/varicad.lck
	chown root.root ${pkgdir}/opt/VariCAD/lib/varicad.lck
	chmod a+rw ${pkgdir}/opt/VariCAD/lib/varicad.lck
  fi

cat <<EOF > ${pkgdir}/opt/VariCAD/desktop/varicad.xml
<?xml version="1.0" encoding="UTF-8"?>
<mime-info xmlns="http://www.freedesktop.org/standards/shared-mime-info">
   <mime-type type="application/x-varicad">
      <comment>VariCAD Drawing</comment>
      <comment xml:lang="en">VariCAD Drawing</comment>
      <glob pattern="*.dwb"/>
      <glob pattern="*.stp"/>
      <glob pattern="*.step"/>
      <glob pattern="*.dwg"/>
      <glob pattern="*.igs"/>
      <glob pattern="*.iges"/>
      <glob pattern="*.dxf"/>
      <icon name="varicad"/>
   </mime-type> 
</mime-info>
EOF

  for i in 16 22 32 48
  do
	install -d "$pkgdir/usr/share/icons/hicolor/"$i"x"$i"/mimetypes"
	cp ${pkgdir}/opt/VariCAD/desktop/varicad_"${i}"x"${i}".png "$pkgdir/usr/share/icons/hicolor/"$i"x"$i"/mimetypes/varicad.png"
  done

  install -D -m 0644 ${pkgdir}/opt/VariCAD/desktop/varicad.desktop "$pkgdir/usr/share/applications/varicad.desktop"
  install -D -m 0644 ${pkgdir}/opt/VariCAD/desktop/varicad.xml "$pkgdir/usr/share/mime/packages/varicad.xml"
}

# vim:set ts=2 sw=2 et:
