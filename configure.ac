AC_INIT(README)
AC_CANONICAL_SYSTEM

MAJOR_VERSION=0
MINOR_VERSION=2
MICRO_VERSION=0
VERSION=$MAJOR_VERSION.$MINOR_VERSION.$MICRO_VERSION
                                                                                
AM_INIT_AUTOMAKE(daap-sharp, $VERSION)
                                                                                
AC_SUBST(MAJOR_VERSION)
AC_SUBST(MINOR_VERSION)
AC_SUBST(MICRO_VERSION)
AC_SUBST(VERSION)
                                                                                
AC_DEFINE_UNQUOTED(MAJOR_VERSION, $MAJOR_VERSION, [Major Version Number])
AC_DEFINE_UNQUOTED(MINOR_VERSION, $MINOR_VERSION, [Minor Version Number])
AC_DEFINE_UNQUOTED(MICRO_VERSION, $MICRO_VERSION, [Micro Version Number])

AM_MAINTAINER_MODE

dnl Mono	   
AC_PATH_PROG(MONO, mono)
if test "x$MONO" = "x" ; then
   AC_MSG_ERROR([Can not find "mono" in your PATH])
fi

dnl mcs	   
AC_PATH_PROG(MCS, mcs)
if test "x$MCS" = "x" ; then
   AC_MSG_ERROR([Can not find "mcs" in your PATH])
fi

PKG_CHECK_MODULES(AVAHI, avahi-sharp >= 0.6)

PKG_CHECK_MODULES(ENTAGGED, entagged-sharp, have_entagged=yes, have_entagged=no)
AM_CONDITIONAL(HAVE_ENTAGGED, test "x$have_entagged" = "xyes")

PKG_CHECK_MODULES(MONODOC, monodoc >= 1.1.9, have_monodoc=yes, have_monodoc=no)

if test "x$have_monodoc" = "xyes"; then
    AC_PATH_PROG(MONODOCER, monodocer)
    AC_PATH_PROG(MDASSEMBLER, mdassembler)

    MONODOC_DIR=`$PKG_CONFIG --variable=sourcesdir monodoc`
    AC_SUBST(MONODOC_DIR)
fi
AM_CONDITIONAL(HAVE_MONODOC, test "x$have_monodoc" = "xyes")

AC_PATH_PROG(GACUTIL, gacutil, no)
if test "x$GACUTIL" = "xno"; then
  AC_MSG_ERROR([You need to install gacutil])
fi


AC_OUTPUT([
Makefile
daap-sharp.pc
src/Makefile
sample/Makefile
])

echo
echo "daap-sharp prefix:    $prefix"
echo "build documentation:  $have_monodoc"
echo