# Created by: David Thiel <lx@FreeBSD.org>
# $FreeBSD$

PORTNAME=	pytone
PORTVERSION=	3.0.3
PORTREVISION=	1
CATEGORIES=	audio python
MASTER_SITES=	http://www.luga.de/pytone/download/ \
		http://redundancy.redundancy.org/mirror/
DISTNAME=	PyTone-${PORTVERSION}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Music jukebox written in Python with a curses GUI

LICENSE=	GPLv2

LIB_DEPENDS=	libao.so:${PORTSDIR}/audio/libao
RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}sqlite3>0:${PORTSDIR}/databases/py-sqlite3 \
		${PYTHON_PKGNAMEPREFIX}mutagen>0:${PORTSDIR}/audio/py-mutagen
		

USES=		ncurses python:2
USE_PYTHON=	autoplist distutils

CFLAGS+=	-I${LOCALBASE}/include

SUB_FILES=	pkg-message

PLIST_FILES=	etc/pytonerc.sample

OPTIONS_DEFINE=		MAD MPG123 MPG321 VORBIS
OPTIONS_DEFAULT=	MAD VORBIS

MAD_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}mad>0:${PORTSDIR}/audio/py-mad
MPG123_RUN_DEPENDS=	mpg123:${PORTSDIR}/audio/mpg123
MPG321_DESC=		MP3 decoding support via mpg321
MPG321_RUN_DEPENDS=	mpg321:${PORTSDIR}/audio/mpg321
VORBIS_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}vorbis>0:${PORTSDIR}/audio/py-vorbis

post-patch:
.for i in pytone pytonectl
	@${REINPLACE_CMD} -e \
		's|^python |${PYTHON_CMD} | ; \
		 s|src/|${PYTHONPREFIX_SITELIBDIR}/pytone/|' ${WRKSRC}/${i}
.endfor

post-install:
	${INSTALL_DATA} ${WRKSRC}/conf/pytonerc ${STAGEDIR}${PREFIX}/etc/pytonerc.sample
	@${STRIP_CMD} ${STAGEDIR}${PYTHONPREFIX_SITELIBDIR}/pytone/*.so

.include <bsd.port.mk>
