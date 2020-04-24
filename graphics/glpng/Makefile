# $OpenBSD: Makefile,v 1.16 2019/07/12 20:46:59 sthen Exp $

COMMENT=	load PNG graphics files and bind them to an OpenGL texture

VERSION=	1.46
GIT_COMMIT=	1079563a36edfe10a5f5d79ad38fe465425b989e
DISTNAME=	${GIT_COMMIT}
PKGNAME=	glpng-${VERSION}
SHARED_LIBS=	glpng 0.0
CATEGORIES=	graphics

HOMEPAGE=	http://www.fifi.org/doc/libglpng-dev/glpng.html

# BSD-like
PERMIT_PACKAGE=	Yes

MASTER_SITES=	https://repo.or.cz/glpng.git/snapshot/

WANTLIB=	z GL png>=5

MODULES=	devel/cmake

LIB_DEPENDS=	graphics/png


TEST_IS_INTERACTIVE=	x11

TEST_DEPENDS=	graphics/freeglut

DIST_SUBDIR=	${PKGNAME}
WRKDIST=	${WRKDIR}/glpng-1079563

MAKE_ENV=	SHLIB_MAJOR=${LIBglpng_VERSION:R} \
		SHLIB_MINOR=${LIBglpng_VERSION:E}
FAKE_FLAGS=	LIBDIR=${LOCALBASE}/lib DEBUGLIBS=no
CFLAGS+=	-I${X11BASE}/include -I${LOCALBASE}/include \
			-I${WRKDIR}/include

post-install:
	${INSTALL_DATA_DIR} ${PREFIX}/share/doc/glpng
	${INSTALL_DATA_DIR} ${PREFIX}/include/GL/
	${INSTALL_DATA} ${WRKDIST}/include/GL/glpng.h \
		${PREFIX}/include/GL
	${INSTALL_DATA} ${WRKDIST}/glpng.htm \
		${PREFIX}/share/doc/glpng/glpng.html

do-test:
	cd ${WRKDIST}/Example \
	&& ${CC} ${CFLAGS} -o Test Test.c -lm -lz \
		-L${X11BASE}/lib -lGL -lGLU -lXi -lXmu \
		-L${LOCALBASE}/lib -lglut \
		-L${WRKBUILD} -lglpng \
	&& LD_LIBRARY_PATH=${WRKSRC} ./Test

.include <bsd.port.mk>
