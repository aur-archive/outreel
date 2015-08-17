# Contributer: giacomogiorgianni@gmail.com 

pkgname=outreel
_name=OutReel
pkgver=2.4.20
pkgrel=1
pkgdesc="Outreel is fast and esasy to use video converter from Icefeast.its a beast ffmpeg frondend for your linux system"
arch=('686' 'x86_64')
url="http://outreel.sourceforge.net/"
license=('GPL')
depends=('qt4' 'ffmpeg')
makedepends=('cmake')
source=("http://netcologne.dl.sourceforge.net/project/${pkgname}/${pkgname}_${pkgver}.zip" "outreel.desktop" "outreel-root.desktop" 'icon.png')
md5sums=('d04f3ece44a1c9f604a71d6cac9ef839'
	  '052f1ae97dd1184f819c202e5ab6ae60'
	  'b6053b7261a51e51ad41680b54c6fd3a'
          '36fc93c7f8e81f45494d1635745ff81a')

install=$pkgname.install

package() {
  cd "$srcdir/${pkgname}_${pkgver}"
 
  #localization
  lrelease translations/*.ts
  
  qmake-qt4 $_name.pro -r -config release \
    "CONFIG+=LINUX_INTEGRATED" \
    "INSTALL_ROOT_PATH=$pkgdir/usr/" \
    "LOWERED_APPNAME=$pkgname"
   make
       #make INSTALL_ROOT=${pkgdir} install
  install -D -m755 "$_name"  "${pkgdir}/usr/bin/${pkgname}"
  mkdir $pkgdir/usr/lib && mkdir $pkgdir/usr/lib/icefeast && mkdir $pkgdir/usr/lib/icefeast/outreel
  cp -r $srcdir/${pkgname}_${pkgver}/settings/ffmpeg-gui/*.* $pkgdir/usr/lib/icefeast/outreel
  #cp -r $srcdir/${pkgname}_${pkgver}/ffmpeg-presets/*.* $pkgdir/usr/lib/icefeast/outreel
    
     #ln -s "/usr/bin/ffmpeg" "${pkgdir}/usr/lib/icefeast/outreel/ffmpeg"
  sed -i '2s|/home/suraj/Desktop/ffmpeg-0.10.3/ffmpeg|/usr/bin/ffmpeg|' $srcdir/${pkgname}_${pkgver}/settings/ffmpeg-gui.conf
  cp -r $srcdir/${pkgname}_${pkgver}/settings/ffmpeg-gui.conf $pkgdir/usr/lib/icefeast/outreel
  
  install -Dm644 $startdir/icon.png \
    "$pkgdir/usr/share/pixmaps/$pkgname.png"
  #cp -r $startdir/icon.png $pkgdir/usr/lib/icefeast/outreel/$pkgname.png
  
  install -Dm644 "$startdir/$pkgname.desktop"  "${pkgdir}/usr/share/applications/$pkgname.desktop"
  install -Dm644 "$startdir/$pkgname-root.desktop"  "${pkgdir}/usr/share/applications/$pkgname-root.desktop"
  
}
