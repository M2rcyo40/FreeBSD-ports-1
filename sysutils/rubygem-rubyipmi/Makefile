# Created by: Martin Matuska <mm@FreeBSD.org>
# $FreeBSD$

PORTNAME=	rubyipmi
PORTVERSION=	0.10.0
CATEGORIES=	sysutils rubygems
MASTER_SITES=	RG

MAINTAINER=	ruby@FreeBSD.org
COMMENT=	Command line wrapper for ipmitool and freeipmi

LICENSE=	LGPL21

RUN_DEPENDS=	${LOCALBASE}/sbin/bmc-device:${PORTSDIR}/sysutils/freeipmi

NO_ARCH=	yes

USE_RUBY=	yes
USE_RUBYGEMS=	yes
RUBYGEM_AUTOPLIST=	yes

.include <bsd.port.mk>
