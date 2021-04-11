project(gnutar)

cmake_minimum_required(VERSION 3.10)

if(COMMAND cmake_policy)
	cmake_policy(SET CMP0003 NEW)
endif(COMMAND cmake_policy)

add_compile_definitions(
	HAVE_CONFIG_H
	_FORTIFY_SOURCE=0
)

# Hide warnings
add_definitions(
	-Wno-format-security
	-Wno-format-extra-args
	-Wno-string-plus-int
	-Wno-shift-negative-value
	-Wno-tautological-compare
	-Wno-incompatible-pointer-types-discards-qualifiers
	-Wno-implicit-function-declaration
)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -nostdinc -fPIC")

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../gen)
include_directories(BEFORE
	${CMAKE_CURRENT_SOURCE_DIR}/../gen/lib
	${CMAKE_CURRENT_SOURCE_DIR}/lib
)

include(InstallSymlink)
set(BINARY_PACKAGING_MODE ON)

add_darling_static_library(libgnutar FAT SOURCES
	lib/__fpending.c
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
	lib/close-stream.c
	lib/closeout.c
	lib/creat-safer.c
	lib/dirname.c
	lib/dup-safer.c
	lib/error.c
	lib/exclude.c
	lib/exitfail.c
	lib/fd-safer.c
	lib/fnmatch.c
	lib/fstatat.c
	lib/full-write.c
	lib/getcwd.c
	lib/getdate.c
	lib/getopt.c
	lib/getopt1.c
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
	lib/open-safer.c
	lib/openat-die.c
	lib/openat-proc.c
	lib/paxerror.c
	lib/paxexit.c
	lib/paxnames.c
	lib/pipe-safer.c
	lib/prepargs.c
	lib/printf-args.c
	lib/printf-parse.c
	lib/quote.c
	lib/quotearg.c
	lib/regex.c
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
	lib/version-etc-fsf.c
	lib/version-etc.c
	lib/xalloc-die.c
	lib/xgetcwd.c
	lib/xmalloc.c
	lib/xstrndup.c
	lib/xstrtol.c
	lib/xstrtoul.c
	lib/xstrtoumax.c
)
set_target_properties(libgnutar PROPERTIES
	OUTPUT_NAME gnutar
)

add_darling_executable(gnutar
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
target_link_libraries(gnutar
	libgnutar
	iconv
)

install(TARGETS gnutar DESTINATION libexec/darling/usr/bin)

install(FILES ../gnutar.1 DESTINATION libexec/darling/usr/share/man/man1)
install(FILES ../gnurmt.8 DESTINATION libexec/darling/usr/share/man/man8)
