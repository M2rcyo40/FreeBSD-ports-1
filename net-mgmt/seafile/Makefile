# $FreeBSD$

PORTNAME=	seafile
PORTVERSION=	4.0.6
PORTREVISION=	3
DISTVERSIONPREFIX=	v
DISTVERSIONSUFFIX=	-server
CATEGORIES=	net-mgmt devel

MAINTAINER=	yan_jingfeng@yahoo.com
COMMENT=	Framework for writing networked applications

LICENSE=	GPLv3

BUILD_DEPENDS=	valac:${PORTSDIR}/lang/vala
LIB_DEPENDS=	libsearpc.so:${PORTSDIR}/devel/libsearpc \
		libevhtp.so:${PORTSDIR}/www/libevhtp \
		libzdb.so:${PORTSDIR}/databases/libzdb \
		libcurl.so:${PORTSDIR}/ftp/curl \
		libinotify.so:${PORTSDIR}/devel/libinotify \
		libccnet.so:${PORTSDIR}/net-mgmt/ccnet
RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}eggtestinfo>0:${PORTSDIR}/devel/py-eggtestinfo \
		${PYTHON_PKGNAMEPREFIX}sqlite3>0:${PORTSDIR}/databases/py-sqlite3 \
		${PYTHON_PKGNAMEPREFIX}pillow>0:${PORTSDIR}/graphics/py-pillow \
		bash:${PORTSDIR}/shells/bash

USE_GITHUB=	yes
GH_ACCOUNT=	haiwen

USES=		autoreconf iconv libarchive libtool pathfix pkgconfig python:2 \
		shebangfix
SHEBANG_FILES=	scripts/*.sh scripts/upgrade/*.sh
GNU_CONFIGURE=	yes
USE_OPENSSL=	yes
USE_LDCONFIG=	yes
CONFIGURE_ENV=	SSL_CFLAGS="${OPENSSLINC}" SSL_LIBS="-L${OPENSSLLIB} -lssl -lcrypto"

PATHFIX_MAKEFILEIN=	Makefile.am

CONFIGURE_ARGS=	--enable-server
INSTALL_TARGET=	install-strip
CPPFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib

HAIWENDIR=	www/haiwen
SEAFILE_SERVER=	${HAIWENDIR}/seafile-server
SEABIN=		${SEAFILE_SERVER}/seafile/bin
SEALIB=		${SEAFILE_SERVER}/seafile/lib

SEAFILE_USERNAME?=	www
SEAFILE_GROUPNAME?=	${SEAFILE_USERNAME}

USE_RC_SUBR=	${PORTNAME}	
PLIST_SUB=	SEAFILE_USERNAME=${SEAFILE_USERNAME} \
		SEAFILE_GROUPNAME=${SEAFILE_GROUPNAME} \
		SEAFILE_SERVER=${SEAFILE_SERVER} \
		HAIWENDIR=${HAIWENDIR}

MAKE_JOBS_UNSAFE=	yes

OPTIONS_DEFINE=		FUSE RIAK
OPTIONS_SUB=		yes

FUSE_DESC=		Use file system in userspace
RIAK_DESC=		Use distributed noSQL database

FUSE_CONFIGURE_ENABLE=	fuse
FUSE_LIB_DEPENDS=	libfuse.so:${PORTSDIR}/sysutils/fusefs-libs

RIAK_CONFIGURE_ENABLE=	riak
RIAK_RUN_DEPENDS=	riak:${PORTSDIR}/databases/riak

OPTIONS_DEFAULT=FUSE
.if defined(DFLYVERSION)
OPTIONS_DEFAULT=
.endif

post-install:
	@${MKDIR} ${STAGEDIR}${PREFIX}/${SEABIN} ${STAGEDIR}${PREFIX}/${SEALIB}\
		${STAGEDIR}${PREFIX}/${SEAFILE_SERVER}/seafile/share/doc/seafile \
		${STAGEDIR}${PREFIX}/${SEAFILE_SERVER}/upgrade
.for SERVPROG in seaf-fsck seafserv-gc seaf-fuse seaf-migrate \
	seaf-server seaf-server-init seafile-controller
	if [ -e "${STAGEDIR}${PREFIX}/bin/${SERVPROG}" ]; then \
		${INSTALL_PROGRAM} ${STAGEDIR}${PREFIX}/bin/${SERVPROG} ${STAGEDIR}${PREFIX}/${SEABIN}; \
		${RM} ${STAGEDIR}${PREFIX}/bin/${SERVPROG}; \
	fi
.endfor
	(cd ${STAGEDIR}${PREFIX}/lib && \
		${COPYTREE_SHARE} ${PYTHON_VERSION} ${STAGEDIR}${PREFIX}/${SEALIB})
	@${RM} -rf ${STAGEDIR}${PREFIX}/lib/${PYTHON_VERSION}
	${INSTALL_SCRIPT} ${WRKSRC}/scripts/*.[ps][yh] ${STAGEDIR}${PREFIX}/${SEAFILE_SERVER}
	${INSTALL_SCRIPT} ${WRKSRC}/scripts/upgrade/*.[ps][yh] \
		${STAGEDIR}${PREFIX}/${SEAFILE_SERVER}/upgrade
	${INSTALL_DATA} ${WRKSRC}/doc/seafile-tutorial.doc \
		${STAGEDIR}${PREFIX}/${SEAFILE_SERVER}/seafile/share/doc/seafile/
	(cd ${WRKSRC}/scripts/upgrade && \
		${COPYTREE_SHARE} sql ${STAGEDIR}${PREFIX}/${SEAFILE_SERVER}/upgrade)

.include <bsd.port.mk>
