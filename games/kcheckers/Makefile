# Created by: arved
# $FreeBSD$

PORTNAME=	kcheckers
PORTVERSION=	0.8.1
PORTREVISION=	1
CATEGORIES=	games
MASTER_SITES=	SF/qcheckers/${PORTNAME}/${PORTVERSION}

MAINTAINER=	johans@FreeBSD.org
COMMENT=	Qt version of the classic boardgame checkers

USES=		qmake
USE_QT4=	corelib gui moc_build rcc_build

post-patch:
	@${REINPLACE_CMD} -e 's|/usr/local|${PREFIX}|' ${WRKSRC}/common.h
	@${REINPLACE_CMD} -e 's|..PREFIX/share/kcheckers|${DATADIR}|' \
		-e 's|..PREFIX|${PREFIX}|' ${WRKSRC}/kcheckers.pro

.include <bsd.port.mk>
