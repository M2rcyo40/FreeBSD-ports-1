# Created by: Hugo Saro <hugo@barafranca.com>
# $FreeBSD$

PORTNAME=	haproxy
DISTVERSION=	1.6-dev6
CATEGORIES=	net www
MASTER_SITES=	http://haproxy.1wt.eu/download/1.6/src/devel/
PKGNAMESUFFIX=	-devel
DISTFILES=	${PORTNAME}-${DISTVERSION}${EXTRACT_SUFX}

MAINTAINER=	demon@FreeBSD.org
COMMENT=	The Reliable, High Performance TCP/HTTP Load Balancer

LICENSE=	GPLv2 LGPL21
LICENSE_COMB=	multi

USES=		cpe gmake
CONFLICTS=	haproxy-[1234567890]\*
USE_RC_SUBR=	haproxy

DEVICEATLAS_VERSION=	2.1
DEVICEATLAS_DISTFILE=	deviceatlas-enterprise-c-${DEVICEATLAS_VERSION}
DEVICEATLAS_REGISTRATION_URL= https://deviceatlas.com/deviceatlas-haproxy-module

OPTIONS_DEFINE=		DOCS EXAMPLES LUA OPENSSL DEVICEATLAS
OPTIONS_RADIO=		PCRE
OPTIONS_RADIO_PCRE=	DPCRE SPCRE
DPCRE_DESC=		Link dynamically
SPCRE_DESC=		Link statically
DEVICEATLAS_DESC=	DeviceAtlas Device Detection support
OPTIONS_DEFAULT=	SPCRE OPENSSL

.include <bsd.port.options.mk>

MAKE_ARGS=	TARGET=freebsd DEFINE=-DFREEBSD_PORTS USE_GETADDRINFO=1 \
		USE_ZLIB=1 CC="${CC}" CFLAGS="${CFLAGS}"

.if ${PORT_OPTIONS:MDPCRE}
LIB_DEPENDS+=	libpcre.so:${PORTSDIR}/devel/pcre
MAKE_ARGS+=	USE_PCRE=1 USE_PCRE_JIT=1
.endif

.if ${PORT_OPTIONS:MSPCRE}
BUILD_DEPENDS+=	${LOCALBASE}/lib/libpcre.a:${PORTSDIR}/devel/pcre
MAKE_ARGS+=	USE_STATIC_PCRE=1 USE_PCRE_JIT=1
.endif

.if ${PORT_OPTIONS:MDEVICEATLAS}
.if !exists(${DISTDIR}/${DEVICEATLAS_DISTFILE}.zip)
IGNORE?=	You must manually fetch the DeviceAtlas Device Detection C API from ${DEVICEATLAS_REGISTRATION_URL} and place it in ${DISTDIR} and then run make again
.else
RESTRICTED=	The redistribution of the DeviceAtlas Device Detection C API is not permitted
DISTFILES+=	${DEVICEATLAS_DISTFILE}.zip
MAKE_ARGS+=	USE_DEVICEATLAS=1 DEVICEATLAS_SRC=${WRKDIR}/deviceatlas-enterprise-c-${DEVICEATLAS_VERSION}
.endif
.if ! ${PORT_OPTIONS:MDPCRE} && ! ${PORT_OPTIONS:MSPCRE}
IGNORE?=	Enable PCRE support to use DeviceAtlas
.endif
.endif

.if ${PORT_OPTIONS:MOPENSSL}
USE_OPENSSL=	yes
MAKE_ARGS+=	USE_OPENSSL=1
.endif

.if ${PORT_OPTIONS:MLUA}
USES+=		lua:53
MAKE_ARGS+=	USE_LUA=1 LUA_INC=${LUA_INCDIR} LUA_LIB=${LUA_LIBDIR} LUA_LIB_NAME=lua-${LUA_VER}
.endif

post-build:
	cd ${WRKSRC}/contrib/halog && ${MAKE_CMD} ${MAKE_ENV}

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/haproxy ${STAGEDIR}${PREFIX}/sbin/
	${INSTALL_PROGRAM} ${WRKSRC}/contrib/halog/halog ${STAGEDIR}${PREFIX}/sbin/
	${INSTALL_MAN} ${WRKSRC}/doc/haproxy.1 ${STAGEDIR}${MAN1PREFIX}/man/man1
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	(cd ${WRKSRC}/doc/ && ${COPYTREE_SHARE} \* ${STAGEDIR}${DOCSDIR})
	${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	(cd ${WRKSRC}/examples/ && ${COPYTREE_SHARE} \* ${STAGEDIR}${EXAMPLESDIR})

.include <bsd.port.mk>
