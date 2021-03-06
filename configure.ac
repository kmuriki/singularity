AC_PREREQ(2.59)
AC_INIT([singularity],[1.0],[gmkurtzer@lbl.gov])
AC_CONFIG_SRCDIR([.])
AC_CONFIG_HEADERS([src/config.h])
AC_CONFIG_MACRO_DIR([.])

if test -z "$prefix" -o "$prefix" = "NONE" ; then
  prefix=${ac_default_prefix}
fi
AC_SUBST(PREFIX, $prefix)

AC_PROG_INSTALL
AM_INIT_AUTOMAKE
AC_PROG_LIBTOOL
AC_PROG_CC

dnl# Add default flags
dnlCFLAGS="-std=gnu99 $CFLAGS"

AC_MSG_CHECKING([for namespace: CLONE_NEWPID])
AC_COMPILE_IFELSE([AC_LANG_PROGRAM([[#define _GNU_SOURCE
                                     #include <sched.h>
                                   ]],
                                   [[unshare(CLONE_NEWPID);]])],
                      [
                          AC_MSG_RESULT([yes])
                          NAMESPACE_DEFINES="$NAMESPACE_DEFINES -DNS_CLONE_NEWPID"
                      ], [
                          AC_MSG_RESULT([no])
                      ]
                  )


AC_MSG_CHECKING([for namespace: CLONE_PID])
AC_COMPILE_IFELSE([AC_LANG_PROGRAM([[#define _GNU_SOURCE
                                     #include <sched.h>
                                   ]],
                                   [[unshare(CLONE_PID);]])],
                      [
                          AC_MSG_RESULT([yes])
                          NAMESPACE_DEFINES="$NAMESPACE_DEFINES -DNS_CLONE_PID"
                      ], [
                          AC_MSG_RESULT([no])
                      ]
                  )


AC_MSG_CHECKING([for namespace: CLONE_FS])
AC_COMPILE_IFELSE([AC_LANG_PROGRAM([[#define _GNU_SOURCE
                                     #include <sched.h>
                                   ]],
                                   [[unshare(CLONE_FS);]])],
                      [
                          AC_MSG_RESULT([yes])
                          NAMESPACE_DEFINES="$NAMESPACE_DEFINES -DNS_CLONE_FS"
                      ], [
                          AC_MSG_RESULT([no])
                      ]
                  )


AC_MSG_CHECKING([for namespace: CLONE_FILES])
AC_COMPILE_IFELSE([AC_LANG_PROGRAM([[#define _GNU_SOURCE
                                     #include <sched.h>
                                   ]],
                                   [[unshare(CLONE_FILES);]])],
                      [
                          AC_MSG_RESULT([yes])
                          NAMESPACE_DEFINES="$NAMESPACE_DEFINES -DNS_CLONE_FILES"
                      ], [
                          AC_MSG_RESULT([no])
                      ]
                  )


AC_MSG_CHECKING([for namespace: CLONE_NEWNS])
AC_COMPILE_IFELSE([AC_LANG_PROGRAM([[#define _GNU_SOURCE
                                     #include <sched.h>
                                   ]],
                                   [[unshare(CLONE_NEWNS);]])],
                      [
                          AC_MSG_RESULT([yes])
                          NAMESPACE_DEFINES="$NAMESPACE_DEFINES -DNS_CLONE_NEWNS"
                      ], [
                          AC_MSG_RESULT([no])
                          echo
                          echo "ERROR!!!!!!"
                          echo
                          echo "This host does not support the CLONE_NEWNS (mount) namespace flag! You"
                          echo "really really really don't want to run Singularity containers without a"
                          echo "Separate mount name namespace! It is possible, but not a great idea."
                          echo
                          echo "Pausing for 5 second so you can digest the severity of this..."
                          echo
                          sleep 5
                      ]
                  )


AC_SUBST(NAMESPACE_DEFINES)


AC_CONFIG_FILES([
   Makefile
   singularity.spec
   src/Makefile
   bin/Makefile
   bin/singularity
   libexec/Makefile
   libexec/mods/Makefile
   libexec/cli/Makefile
])
AC_OUTPUT
