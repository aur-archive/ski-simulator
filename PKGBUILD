# Maintainer: Patryk Kowalczyk < patryk at kowalczyk dot ws>

pkgname=ski-simulator
pkgver=1.3.2
pkgrel=7
pkgdesc="An Itanium (ia64) simulator"
arch=('i686' 'x86_64')
url="http://ski.sourceforge.net/"
license=('GPL')
depends=("ncurses" "elfutils")
makedepends=("bison" "autoconf" "libtool" "flex" "gawk" "gperf" "automake" "gtk2")
options=(libtool)
source=(http://freefr.dl.sourceforge.net/project/ski/ski/$pkgver/ski-$pkgver.tar.gz
	ski-1.3.2-AC_C_BIGENDIAN.patch
	ski-1.3.2-configure-withval.patch
	ski-1.3.2-gtk-linkage.patch
	ski-1.3.2-no-local-ltdl.patch
	ski-1.3.2-remove-hayes.patch
	ski-1.3.2-syscall-linux-includes.patch
)

build() {
  cd "$srcdir/ski-$pkgver"
  patch -p1 < ../ski-1.3.2-syscall-linux-includes.patch || return 1
  patch -p1 < ../ski-1.3.2-remove-hayes.patch || return 1
  patch -p1 < ../ski-1.3.2-no-local-ltdl.patch || return 1
  patch -p1 < ../ski-1.3.2-AC_C_BIGENDIAN.patch || return 1
  patch -p1 < ../ski-1.3.2-configure-withval.patch || return 1
  patch -p1 < ../ski-1.3.2-gtk-linkage.patch || return 1
   rm -rf libltdl src/ltdl.[ch] macros/ltdl.m4
  
  #NOCONFIGURE="yes" 
  AT_M4DIR="macros" aclocal
  automake --add-missing
#  macros/autogen.sh 

  ./configure --prefix=/usr --without-included-ltdl || return 1
#  sed -i '/<asm\/page.h>/d' src/linux/syscall-linux.c
  make || return 1
}

package(){
  cd "$srcdir/ski-$pkgver"

  make DESTDIR="$pkgdir/" install
}
md5sums=('fa511f222d246e9a7578106db75fd6a5'
         'e45ccf94bd7ed24f02fd19eb5bb32ec7'
         '1eae1482f41db3c59bd524a5c360d172'
         '33155068e849a318aa3afa3364984141'
         'e2a186b67ec9270bff1a662e145d4106'
         'c3bf77f1ab94590a6d1b168a68ac6042'
         '1a8c0ca74574b23ea5f08c264c97c820')

