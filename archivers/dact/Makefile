# Created by: ijliao
# $FreeBSD$

PORTNAME=	dact
PORTVERSION=	0.8.42
PORTREVISION=	2
CATEGORIES=	archivers
MASTER_SITES=	http://www.rkeene.org/files/oss/dact/release/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Dynamic Adaptive Compression Tool

LICENSE=	GPLv2 # or later
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	libmcrypt.so:${PORTSDIR}/security/libmcrypt \
		liblzo2.so:${PORTSDIR}/archivers/lzo2

USES=		gmake desthack
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--libdir=${PREFIX}/lib
CPPFLAGS+=	${CXXFLAGS} -I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib
MAKE_ARGS=	TOBUILD="dact libdact.so dact.conf"

USE_LDCONFIG=	yes

OPTIONS_DEFINE=	DOCS

post-install:
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/${PORTNAME} \
		${STAGEDIR}${PREFIX}/lib/lib${PORTNAME}.so \
		${STAGEDIR}${DATADIR}/*.so
	${MV} ${STAGEDIR}${PREFIX}/etc/${PORTNAME}.conf \
		${STAGEDIR}${PREFIX}/etc/${PORTNAME}.conf.sample
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/Docs/dact.txt ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/README ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
