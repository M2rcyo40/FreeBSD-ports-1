# Created by: Carlo Strub <c-s@c-s.li>
# $FreeBSD$

PORTNAME=	bzr-builder
PORTVERSION=	0.7.3
PORTREVISION=	1
CATEGORIES=	devel
MASTER_SITES=	http://launchpadlibrarian.net/100761063/ \
		http://www.c-s.li/ports/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Bzr plugin to construct a bzr branch based on a "recipe"

LICENSE=	GPLv3

BUILD_DEPENDS=	bzr:${PORTSDIR}/devel/bzr
RUN_DEPENDS=	bzr:${PORTSDIR}/devel/bzr

WRKSRC=		${WRKDIR}/${PORTNAME}-${PORTVERSION}

USES=		python
USE_PYTHON=	distutils autoplist

.include <bsd.port.mk>
