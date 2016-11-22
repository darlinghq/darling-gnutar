project(gnutar)

cmake_minimum_required(VERSION 2.4.0)

if(COMMAND cmake_policy)
	cmake_policy(SET CMP0003 NEW)
endif(COMMAND cmake_policy)

include(darling_exe)
add_definitions(-DTARGET_OS_MAC=1)
add_definitions(-D__APPLE__ -D__DYNAMIC__)
add_definitions(-DHAVE_CONFIG_H)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -D_POSIX_C_SOURCE -nostdinc -fPIC")
set(CMAKE_EXE_LINKER_FLAGS "-nodefaultlibs -nostdlib -Wl,--version-script=${DARLING_TOP_DIRECTORY}/darwin.map")

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(BEFORE ${CMAKE_CURRENT_SOURCE_DIR}/lib)
include_directories(${DARLING_TOP_DIRECTORY}/src/libc/include/FreeBSD)
include_directories(${DARLING_TOP_DIRECTORY}/src/libc/include/NetBSD)
include_directories(${DARLING_TOP_DIRECTORY}/src/libc/gen)
include_directories(${DARLING_TOP_DIRECTORY}/src/libc/darwin)
include_directories(${DARLING_TOP_DIRECTORY}/src/libc/stdtime/FreeBSD)
include_directories(${DARLING_TOP_DIRECTORY}/src/launchd/liblaunch)
include_directories(${DARLING_TOP_DIRECTORY}/src/external/libdispatch)
include_directories(${DARLING_TOP_DIRECTORY}/src/external/zlib)
include_directories(${DARLING_TOP_DIRECTORY}/src/external/bzip2)
include_directories(${DARLING_TOP_DIRECTORY}/src/copyfile)
include_directories(${DARLING_TOP_DIRECTORY}/src/libiconv/include)

include(InstallSymlink)
set(BINARY_PACKAGING_MODE ON)

set(gnutar_sources
	lib/allocsa.c
	lib/argmatch.c
	lib/argp-ba.c
	lib/argp-eexst.c
	lib/argp-fmtstream.c
	lib/argp-fs-xinl.c
	lib/argp-help.c
	lib/argp-parse.c
	lib/argp-pin.c
	lib/argp-pv.c
	lib/argp-pvh.c
	lib/argp-xinl.c
	lib/asnprintf.c
	lib/backupfile.c
	lib/basename.c
	lib/canonicalize-lgpl.c
	lib/chdir-long.c
	lib/closeout.c
	lib/close-stream.c
	lib/creat-safer.c
	lib/dirname.c
	lib/dup-safer.c
	lib/error.c
	lib/exclude.c
	lib/exitfail.c
	lib/fd-safer.c
	lib/fnmatch.c
	lib/__fpending.c
	lib/fstatat.c
	lib/full-write.c
	lib/getcwd.c
	lib/getdate.c
	lib/getopt1.c
	lib/getopt.c
	lib/gettime.c
	lib/hash.c
	lib/human.c
	lib/imaxtostr.c
	lib/localcharset.c
	lib/lstat.c
	lib/mbchar.c
	lib/mbscasecmp.c
	lib/mempcpy.c
	lib/memrchr.c
	lib/mktime.c
	lib/modechange.c
	lib/obstack.c
	lib/offtostr.c
	lib/openat-die.c
	lib/openat-proc.c
	lib/open-safer.c
	lib/paxerror.c
	lib/paxexit.c
	lib/paxnames.c
	lib/pipe-safer.c
	lib/prepargs.c
	lib/printf-args.c
	lib/printf-parse.c
	lib/quotearg.c
	lib/quote.c
	lib/regex.c
	lib/rpmatch.c
	lib/rtapelib.c
	lib/safe-read.c
	lib/safe-write.c
	lib/save-cwd.c
	lib/savedir.c
	lib/stdopen.c
	lib/strchrnul.c
	lib/stripslash.c
	lib/strnlen1.c
	lib/tempname.c
	lib/uinttostr.c
	lib/umaxtostr.c
	lib/unlinkdir.c
	lib/utimens.c
	lib/vasnprintf.c
	lib/version-etc.c
	lib/version-etc-fsf.c
	lib/xgetcwd.c
	lib/xmalloc.c
	lib/xstrndup.c
	lib/xstrtol.c
	lib/xstrtoul.c
	lib/xstrtoumax.c

	src/buffer.c
	src/compare.c
	src/create.c
	src/delete.c
	src/extract.c
	src/incremen.c
	src/list.c
	src/misc.c
	src/names.c
	src/sparse.c
	src/system.c
	src/tar.c
	src/transform.c
	src/update.c
	src/utf8.c
	src/xheader.c

)

add_darling_executable(gnutar ${gnutar_sources})

install(TARGETS gnutar
	DESTINATION libexec/darling/usr/bin)

install(FILES ../gnutar.1 DESTINATION libexec/darling/usr/share/man/man1)
install(FILES ../gnurmt.8 DESTINATION libexec/darling/usr/share/man/man8)
