# Created by: Veniamin Gvozdikov <vg@FreeBSD.org>
# $FreeBSD$

PORTNAME=	impressive
PORTVERSION=	0.10.3
PORTREVISION=	7
CATEGORIES=	graphics
MASTER_SITES=	SF/${PORTNAME}/Impressive/${PORTVERSION}/
DISTNAME=	Impressive-${PORTVERSION}

MAINTAINER=	vg@FreeBSD.org
COMMENT=	The stylish way of giving presentations

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/license.txt

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}opengl>=0:${PORTSDIR}/graphics/py-opengl \
		${PYTHON_PKGNAMEPREFIX}pillow>0:${PORTSDIR}/graphics/py-pillow \
		xpdf:${PORTSDIR}/graphics/xpdf \
		pdftk:${PORTSDIR}/print/pdftk \
		xdg-open:${PORTSDIR}/devel/xdg-utils \
		mplayer:${PORTSDIR}/multimedia/mplayer \
		${PYGAME}

USES=		ghostscript:run python
NO_BUILD=	yes
NO_ARCH=	yes
PLIST_FILES=	bin/${PORTNAME} \
		man/man1/${PORTNAME}.1.gz

PORTDOCS=	${PORTNAME}.html demo.pdf

OPTIONS_DEFINE=	DOCS

do-install:
	@${INSTALL_SCRIPT} ${WRKSRC}/${PORTNAME}.py ${STAGEDIR}${PREFIX}/bin/${PORTNAME}
	@${INSTALL_MAN} ${WRKSRC}/${PORTNAME}.1 ${STAGEDIR}${MAN1PREFIX}/man/man1

do-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S|^|${WRKSRC}/|} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
