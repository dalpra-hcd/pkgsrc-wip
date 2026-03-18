# $NetBSD$

DISTNAME=	mattermost-${PKGVER}
PKGVER=		11.5.1

CATEGORIES=	www
MASTER_SITES=	${MASTER_SITE_GITHUB:=mattermost/}
GITHUB_TAG=	v${PKGVERSION_NOREV}

MAINTAINER=	pkgsrc-users@NetBSD.org
HOMEPAGE=	https://github.com/mattermost/mattermost
COMMENT=	Web based collaboration platform
LICENSE=	gnu-lgpl-v3 AND apache-2.0

WRKSRC=		${WRKDIR}/mattermost-${PKGVER}/server

PKG_SYSCONFSUBDIR=	mattermost

#GO_VERSION_REQD=	125

.include "go-modules.mk"

# This needs to come before bsd.prefs.mk
.include "../../lang/go/go-vars.mk"

.include "../../mk/bsd.prefs.mk"

BUILD_DEFS+=		VARBASE MATTERMOST_USER MATTERMOST_GROUP

MATTERMOST_USER?=	mattermost
MATTERMOST_GROUP?=	mattermost

PKG_USERS_VARS+=	MATTERMOST_USER
PKG_GROUPS_VARS+=	MATTERMOST_GROUP
PKG_GROUPS=		${MATTERMOST_GROUP}
PKG_USERS=		${MATTERMOST_USER}:${MATTERMOST_GROUP}

PKG_GECOS.${MATTERMOST_USER}=	MATTERMOST collaboration server
PKG_HOME.${MATTERMOST_USER}=	${MATTERMOST_DATADIR}
PKG_SHELL.${MATTERMOST_USER}=	${NOLOGIN}

RCD_SCRIPTS+=		mattermost
FILES_SUBST+=		MATTERMOST_USER=${MATTERMOST_USER:Q}
FILES_SUBST+=		MATTERMOST_GROUP=${MATTERMOST_GROUP:Q}
#FILES_SUBST+=		MATTERMOST_DATADIR=${MATTERMOST_DATADIR:Q}
#FILES_SUBST+=		MATTERMOST_LOGDIR=${MATTERMOST_LOGDIR:Q}

# From Arch package
MAKE_ENV+=	BUILD_ENTERPRISE=false

GOFLAGS+=	-ldflags=" \
	-X github.com/mattermost/mattermost/server/public/model.BuildNumber=${PKGVERSION} \
	-X github.com/mattermost/mattermost/server/public/model.BuildHash=none \
	-X github.com/mattermost/mattermost/server/public/model.BuildHashEnterprise=none \
	-X github.com/mattermost/mattermost/server/public/model.BuildEnterpriseReady=false"

INSTALLATION_DIRS+=	sbin

.include "go-modules.mk"

.include "../../lang/go/go-module.mk"

.include "../../graphics/png/buildlink3.mk"

.include "../../mk/bsd.pkg.mk"
