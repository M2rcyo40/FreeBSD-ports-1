# Created by: Koop Mast <kwm@FreeBSD.org>
# $FreeBSD$

PORTNAME=	aisleriot
PORTVERSION=	3.16.2
CATEGORIES=	games gnome
MASTER_SITES=	GNOME
DIST_SUBDIR=	gnome3

MAINTAINER=	gnome@FreeBSD.org
COMMENT=	Collection of patience games written in guile scheme

BUILD_DEPENDS=	itstool:${PORTSDIR}/textproc/itstool \
		appdata-validate:${PORTSDIR}/devel/appstream-glib \
		bash:${PORTSDIR}/shells/bash
LIB_DEPENDS=	libguile-2.0.so:${PORTSDIR}/lang/guile2 \
		libcanberra-gtk3.so:${PORTSDIR}/audio/libcanberra-gtk3

CONFLICTS=	sol-*
PORTSCOUT=	limitw:1,even

USES=		desktop-file-utils gettext gmake pathfix pkgconfig tar:xz
USE_GNOME=	gconf2 gtk30 intlhack librsvg2 libxml2:build
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--with-card-theme-formats=svg \
		--with-guile=2.0
# work around because configure needs bash
CONFIGURE_SHELL=${LOCALBASE}/bin/bash

GCONF_SCHEMAS=	aisleriot.schemas
GLIB_SCHEMAS=	org.gnome.Patience.WindowState.gschema.xml

.include <bsd.port.mk>
