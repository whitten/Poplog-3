

all: Makefile make configure.ac config.h system.ph

clean:
	rm -f config make configure.ac
	rm -rf autom4te.cache
	rm -f config.log config.sample config.status configure config.h


system.ph: config.h Makefile
	echo "\n;;; This file created automatically by make. Don't edit by hand!\n\n" > system.ph
	grep '#define' config.h | egrep 'PACKAGE_VERSION|SIZEOF_SIZE_T' | awk '{print "constant", "SYS_"$$2, "=", $$3, ";"}' >> system.ph

# See http://www.gnu.org/software/autoconf/manual/html_node/Automatic-Remaking.html#Automatic-Remaking

configure: configure.ac
	autoconf

# autoheader might not change config.h.in, so touch a stamp file.
# don't clean these two
config.h.in: stamp-h.in
stamp-h.in: configure.ac
	autoheader
	echo timestamp > stamp-h.in

Makefile config.h make: Makefile.in config.status make.in
	./config.status

config.status: configure stamp-h.in
	# ./config.status --recheck
	./configure -no-create --no-recursion

