# Created by: Torsten Zühlsdorff <ports@toco-domains.de>
# $FreeBSD$

PORTNAME=	activesupport
PORTVERSION=	4.1.13
CATEGORIES=	devel rubygems
MASTER_SITES=	RG
PKGNAMESUFFIX=	41

MAINTAINER=	ruby@FreeBSD.org
COMMENT=	Utility classes and extension that are required by Rails MVC Framework

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/MIT-LICENSE

RUN_DEPENDS=	rubygem-i18n>=0.6.9:${PORTSDIR}/devel/rubygem-i18n \
		rubygem-json>=1.7.7:${PORTSDIR}/devel/rubygem-json \
		rubygem-minitest>=5.1:${PORTSDIR}/devel/rubygem-minitest \
		rubygem-thread_safe1>=0.1:${PORTSDIR}/devel/rubygem-thread_safe1 \
		rubygem-tzinfo>=1.1:${PORTSDIR}/devel/rubygem-tzinfo

NO_ARCH=	yes
USE_RUBY=	yes
USE_RUBYGEMS=	yes
RUBYGEM_AUTOPLIST=	yes

PORTSCOUT=	limit:^4\.1

.include <bsd.port.mk>
