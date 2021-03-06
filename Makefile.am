# Makefile for BitcoinArmory bitcoin wallet
SUBDIRS = cppForSwig

HAVE_GUI = false

EXTRA_DIST = *.py *.md LICENSE LICENSE-ATI LICENSE-MIT \
	nginx_example.conf imgList.xml autogen.sh \
	armoryengine/*.py ui/*.py \
	img/* lang/* dpkgfiles/* \
	windowsbuild/* linuxbuild/* osxbuild/*

ACLOCAL_AMFLAGS = -I m4

lrelease:

qrc_img_resources.py: imgList.xml

copy-script:
	cp cppForSwig/ArmoryDB ./ArmoryDB

# SWIG code and requirements.
if HAVE_GUI
	cp cppForSwig/CppBlockUtils.py ./CppBlockUtils.py
if BUILD_DARWIN
	cp cppForSwig/.libs/libCppBlockUtils.dylib ./_CppBlockUtils.so
else
	cp cppForSwig/.libs/libCppBlockUtils.so ./_CppBlockUtils.so
endif
endif

.PHONY: copy-script lrelease qrc_img_resources.py

all-local: copy-script lrelease qrc_img_resources.py


#target to clean up pre autotools installation left overs
uninstall-old:
	rm -f $(DESTDIR)$(prefix)/bin/ArmoryDB

install-exec-hook: uninstall-old


	mkdir -p $(DESTDIR)$(prefix)/bin
# Sometimes, uninstall-old deletes a valid ArmoryDB. Copy again to be safe.
	cp ArmoryDB $(DESTDIR)$(prefix)/bin

# No need to install test binaries.
if BUILD_TESTS
	rm -f $(DESTDIR)$(prefix)/bin/ContainerTests
	rm -f $(DESTDIR)$(prefix)/bin/CppBlockUtilsTests
	rm -f $(DESTDIR)$(prefix)/bin/DB1kIterTest
endif

# Skip Linux-specific steps on OSX.
if ! BUILD_DARWIN

endif

uninstall-hook: uninstall-old
	rm -rf $(DESTDIR)$(prefix)/lib/armory
	rm -rf $(DESTDIR)$(prefix)/bin/armory
	rm -f  $(DESTDIR)$(prefix)/share/applications/armory*
	rm -rf $(DESTDIR)$(prefix)/share/armory

clean-local:
	rm -f ArmoryDB
	rm -f CppBlockUtils.py
	rm -f _CppBlockUtils.so
	rm -f CppBlockUtils.pyc
