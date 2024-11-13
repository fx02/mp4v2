#
#  LIVE mp4v2 library
#
#  Created by Zvonimir Buzanic
#  2023-11-13
#
# after building mp4v2 copy this Makefile and debian directory to mp4v2-2.x.x/deb/
# autoreconf -i
# cmake .
# make
# cd deb/
# make deb

VERSION=2.1
RELEASE=3

NAME=mp4v2
ME=${NAME}-${VERSION}.${RELEASE}
ARCH:=${shell uname -m}
prefix?=/usr/local
libdir=${prefix}/lib
incdir=${prefix}/include
INSTALL?=install -c
INSTALL_DATA=${INSTALL} -m 644
LIBLIVEINCL=-I..
COMMENT=Live mp4v2 library.

deb:
	rm -rf ${ME}
	mkdir -p ${ME}/${libdir}/pkgconfig/ ${ME}/${incdir}/mp4v2/ ${ME}/DEBIAN/
	${INSTALL} -m 775 debian/* ${ME}/DEBIAN/
	sed -i -e "s/%%VERSION%%/${VERSION}.${RELEASE}/g" ${ME}/DEBIAN/control
	${INSTALL} -m 755 ../include/mp4v2/*.* ${ME}/${incdir}/mp4v2/
	${INSTALL} -m 755 ../libmp4v2.so ${ME}/${libdir}/
	ln -s ${ME}/${libdir}/libmp4v2.so ${ME}/${libdir}/libmp4v2.so.2.1.3
	ln -s ${ME}/${libdir}/libmp4v2.so ${ME}/${libdir}/libmp4v2.so.2
	${INSTALL} -m 755 ../mp4v2.pc ${ME}/${libdir}/pkgconfig/mp4v2.pc
	dpkg-deb --build ${ME}

clean:
	rm -rf ${ME} ${ME}.deb
