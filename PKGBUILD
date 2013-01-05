# Maintainer: Christopher Reimer <c[dot]reimer[at]googlemail[dot]com>
pkgname=vdr-live
pkgver=20120325
_gitver=94a0a21
_vdrapi=1.7.35
pkgrel=4
pkgdesc="Adds the possibility to control VDR and some of it's plugins by a web interface."
url="http://projects.vdr-developer.org/projects/plg-live"
arch=('x86_64' 'i686')
license=('GPL2')
depends=('pcre' 'tntnet' "vdr-api=${_vdrapi}")
install="$pkgname.install"
_plugname=$(echo $pkgname | sed 's/vdr-//g')
replaces=("vdr-plugin-$_plugname")
conflicts=("vdr-plugin-$_plugname")
source=("http://projects.vdr-developer.org/git/vdr-plugin-$_plugname.git/snapshot/vdr-plugin-$_plugname-$_gitver.tar.bz2"
        'live_1.7.28_fix.diff'
        'live-1.7.30-fhs.diff')
md5sums=('7a4037544bf31babd13b823afebf4f33'
         '74167417d121da69f1bd06235324440f'
         'c77cdbb3289ddc8e838cbe98178789de')

package() {
  cd "${srcdir}/vdr-plugin-${_plugname}-${_gitver}"

  patch -p1 -i ${srcdir}/live_1.7.28_fix.diff
  patch -p1 -i ${srcdir}/live-1.7.30-fhs.diff

  mkdir -p $pkgdir/usr/lib/vdr/plugins
  make CFLAGS="$(pkg-config vdr --variable=cflags)" \
       CXXFLAGS="$(pkg-config vdr --variable=cxxflags)" \
       VDRDIR="/usr/include/vdr" \
       LIBDIR="$pkgdir/$(pkg-config vdr --variable=libdir)" \
       LOCALEDIR="$pkgdir/$(pkg-config vdr --variable=locdir)"

  mkdir -p $pkgdir/usr/share/vdr/plugins
  cp -r live $pkgdir/usr/share/vdr/plugins
}
