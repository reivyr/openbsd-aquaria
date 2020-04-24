# $OpenBSD: Makefile.template,v 1.77 2018/02/09 17:08:33 sthen Exp $

# TODO:
# AQUARIA_DEFAULT_DATA_DIR:STRING=
# AQUARIA_DEMO_BUILD:BOOL=OFF
# AQUARIA_EXTRA_DATA_DIR:STRING=
# right now needs AQUARIA_DATA_PATH to be set
# needs graphics/glpng update to be recognized by cmake
# XInput/DInput joystick not recognized

COMMENT =	open-source fork of aquaria, an underwater action game

V = 1.2.20190905
DISTNAME =	aquaria-${V}

GH_ACCOUNT =	AquariaOSE
GH_PROJECT =	Aquaria
GH_COMMIT =	988db94b729b2867cedd246493a0234c561516c8

# for libtool- or cmake-based ports, have a look at WRKBUILD/shared_libs.log
#SHARED_LIBS =	???

CATEGORIES =	games

MAINTAINER =	Thomas Frohwein <frohwein@ymail.com>

#GPLv2
PERMIT_PACKAGE =	Yes

COMPILER = base-clang ports-gcc

WANTLIB += ${COMPILER_LIBCXX} SDL2 c m ogg openal png
WANTLIB += tinyxml2 vorbis vorbisfile z
WANTLIB += ftgl glpng
WANTLIB += lua5.1

MODULES =	devel/cmake \
		lang/lua
#RUN_DEPENDS =		???
LIB_DEPENDS =	audio/openal \
		audio/libvorbis \
		audio/libogg \
		devel/sdl2 \
		graphics/png \
		textproc/tinyxml2 \
		graphics/ftgl \
		graphics/glpng

#MAKE_FLAGS =		???
#MAKE_ENV =		???
#FAKE_FLAGS =		???
#TEST_FLAGS =		???

#SEPARATE_BUILD =	Yes (build in a directory other than WRKSRC)
#SEPARATE_BUILD =	flavored (distinct flavors may share a common WRKSRC)
#USE_GMAKE =		Yes
#USE_GROFF =		Yes
#CONFIGURE_STYLE =
#CONFIGURE_SCRIPT =	??? (if other than configure)
CONFIGURE_ARGS =	-DAQUARIA_INTERNAL_FREETYPE=OFF \
			-DAQUARIA_INTERNAL_LUA=OFF \
			-DAQUARIA_INTERNAL_OGGVORBIS=OFF \
			-DAQUARIA_INTERNAL_PNG=OFF \
			-DAQUARIA_INTERNAL_ZLIB=OFF \
			-DAQUARIA_USE_SDL2=ON \
			-DAQUARIA_INTERNAL_FTGL=OFF \
			-DAQUARIA_INTERNAL_GLPNG=OFF
#CONFIGURE_ENV =	???

#TEST_IS_INTERACTIVE =		Yes

#NO_TEST =		Yes

#CFLAGS =		???
#LDFLAGS =		???
#MAKE_FILE =		???
#PKG_ARCH =		??? (* for arch-independent packages)
#WRKDIST =		??? if other than ${WRKDIR}/${DISTNAME}
#WRKSRC =		??? if other than ${WRKDIST}
#WRKBUILD =		??? if other than ${WRKSRC}
#WRKCONF =		??? if other than ${WRKBUILD}

#ALL_TARGET =		???
#INSTALL_TARGET =	???
#TEST_TARGET =		???

AQUARIA_SHARE_DIR =	${PREFIX}/share/aquaria

post-extract:
	rm ${WRKSRC}/ExternalLibs/SDL12/include/SDL_config.h.orig

do-install:
	${INSTALL_PROGRAM} ${WRKBUILD}/aquaria ${PREFIX}/bin
	${INSTALL_DATA_DIR} ${AQUARIA_SHARE_DIR}
	cp -Rp ${WRKSRC}/files ${WRKSRC}/game_scripts ${AQUARIA_SHARE_DIR}
	chown -R ${SHAREOWN}:${SHAREGRP} ${AQUARIA_SHARE_DIR}

.include <bsd.port.mk>
