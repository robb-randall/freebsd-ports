# Created by: Joe Marcus Clarke <marcus@FreeBSD.org>
# $FreeBSD$
#   $MCom: ports/textproc/rarian/Makefile,v 1.12 2008/03/09 21:41:22 mezz Exp $

PORTNAME=	rarian
PORTVERSION=	0.8.1
PORTREVISION=	5
CATEGORIES=	textproc gnome
MASTER_SITES=	GNOME

MAINTAINER=	gnome@FreeBSD.org
COMMENT=	OMF help system based on the Freedesktop specification

LICENSE=	GPLv2+ LGPL21+ ZLIB
LICENSE_COMB=	multi
LICENSE_FILE_GPLv2+ =	${WRKSRC}/COPYING.UTILS
LICENSE_FILE_LGPL21+ =	${WRKSRC}/COPYING.LIB
LICENSE_FILE_ZLIB=	${WRKSRC}/COPYING

BUILD_DEPENDS=	${LOCALBASE}/share/xsl/docbook/xhtml/chunk.xsl:textproc/docbook-xsl \
		bash:shells/bash \
		docbook-xml>0:textproc/docbook-xml
RUN_DEPENDS=	${LOCALBASE}/bin/getopt:misc/getopt \
		${LOCALBASE}/share/xsl/docbook/xhtml/chunk.xsl:textproc/docbook-xsl \
		bash:shells/bash \
		docbook-xml>0:textproc/docbook-xml

USES=		gmake gnome libtool localbase pathfix python tar:bzip2
USE_GNOME=	libxslt
USE_LDCONFIG=	yes
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--localstatedir=/var \
		--with-convert-dir=${LOCALBASE}/share/omf

INSTALL_TARGET=	install-strip

post-patch:
	@${REINPLACE_CMD} -e 's|/lib/rarian|/db/rarian|' \
		${WRKSRC}/util/Makefile.in
	@${REINPLACE_CMD} -e 's|@localstatedir@/lib/rarian|@localstatedir@/db/rarian|g ; \
		s|getopt|${LOCALBASE}/bin/getopt|' \
		${WRKSRC}/util/rarian-sk-config.in \
		${WRKSRC}/util/rarian-sk-extract.in \
		${WRKSRC}/util/rarian-sk-rebuild.in \
		${WRKSRC}/util/rarian-sk-update.in
	@${REINPLACE_CMD} -e 's|/usr/local|${LOCALBASE}|' \
		${WRKSRC}/librarian/rarian-main.c \
		${WRKSRC}/librarian/rarian-man.c \
		${WRKSRC}/librarian/rarian-info.c

.include <bsd.port.mk>
