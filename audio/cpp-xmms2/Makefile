# Created by: Alexander Botero-Lowry <alex@foxybanana.com>
# $FreeBSD$

PORTREVISION=	8
CATEGORIES=	audio
PKGNAMEPREFIX=	cpp-

MAINTAINER=	madpilot@FreeBSD.org
COMMENT=	C++ Bindings for XMMS2

LIB_DEPENDS+=	libboost_signals.so:${PORTSDIR}/devel/boost-libs \
		libxmmsclient.so:${PORTSDIR}/audio/xmms2

MASTERDIR=	${.CURDIR}/../xmms2
USE_LDCONFIG=	yes
USE_GNOME=	glib20

PLIST=		${.CURDIR}/pkg-plist

XMMS2_SLAVE=	cpp

.include "${MASTERDIR}/Makefile"
