include ../Makefile.include
DEPS= Makefile

# lib name, version
LIBNAME=libjpeg-turbo
VERSION=1.4.2
SOURCE=$(LIBNAME)-$(VERSION)
ARCHIVE=$(LIBNAME)-$(VERSION).tar.gz

# configuration settings
CONFIGURE=./configure --prefix=$(PREFIX) \
  --with-jpeg8

export CFLAGS=-O3

LIBDYLIB=$(SOURCE)/.libs/libjpeg.a

CLEAN_FILES=$(ARCHIVE) $(SOURCE)

all: .installed

$(TARBALLS_LOCATION)/$(ARCHIVE):
	$(RETRIEVE_TOOL) $(RETRIEVE_TOOL_FLAGS) $(BASE_URL)/$(ARCHIVE)

$(SOURCE): $(TARBALLS_LOCATION)/$(ARCHIVE) $(DEPS)
	rm -rf $(SOURCE)
	$(ARCHIVE_TOOL) $(ARCHIVE_TOOL_FLAGS) $(TARBALLS_LOCATION)/$(ARCHIVE)
	echo $(SOURCE) > .gitignore
	cd $(SOURCE); autoreconf -vif
	cd $(SOURCE); $(CONFIGURE)

$(LIBDYLIB): $(SOURCE)
	make -j 1 -C $(SOURCE)

.installed: $(LIBDYLIB)
	make -C $(SOURCE) install
	touch $@

clean:
	make -C $(SOURCE) clean
	rm -f .installed

distclean::
	rm -rf $(SOURCE) .installed
