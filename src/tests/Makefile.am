EXTRA_DIST = \
	hold-stdin print-exitstatus \
	e2e-test e2e-test-server \
	e2e-test-subrs \
	mosh-client mosh-server \
	$(displaytests) \
	emulation-attributes.test

AM_CXXFLAGS = $(WARNING_CXXFLAGS) $(PICKY_CXXFLAGS) $(HARDEN_CFLAGS) $(MISC_CXXFLAGS)
AM_LDFLAGS  = $(HARDEN_LDFLAGS)

displaytests = \
	e2e-success.test \
	e2e-failure.test \
	emulation-ascii-iso-8859.test \
	emulation-80th-column.test \
	emulation-attributes-vt100.test \
	emulation-attributes-16color.test \
	emulation-attributes-256color8.test \
	emulation-attributes-256color248.test \
	emulation-back-tab.test \
	emulation-cursor-motion.test \
	emulation-multiline-scroll.test \
	emulation-wrap-across-frames.test \
	prediction-unicode.test \
	pty-deadlock.test \
	server-network-timeout.test \
	server-signal-timeout.test \
	window-resize.test \
	unicode-combine-fallback-assert.test \
	unicode-later-combining.test \
	window-resize.test

check_PROGRAMS = ocb-aes encrypt-decrypt base64
TESTS = ocb-aes encrypt-decrypt base64 $(displaytests)
XFAIL_TESTS = \
	e2e-failure.test \
	emulation-attributes-256color8.test

base64_vector.cc: $(srcdir)/genbase64.pl
	$(AM_V_GEN)echo '#include "base64_vector.h"' > base64_vector.cc || rm base64_vector.cc
	$(AM_V_GEN)perl $(srcdir)/genbase64.pl >> base64_vector.cc || rm base64_vector.cc

ocb_aes_SOURCES = ocb-aes.cc test_utils.cc test_utils.h
ocb_aes_CPPFLAGS = -I$(srcdir)/../crypto -I$(srcdir)/../util $(CRYPTO_CFLAGS)
ocb_aes_LDADD = ../crypto/libmoshcrypto.a ../util/libmoshutil.a $(CRYPTO_LIBS)

encrypt_decrypt_SOURCES = encrypt-decrypt.cc test_utils.cc test_utils.h
encrypt_decrypt_CPPFLAGS = -I$(srcdir)/../crypto -I$(srcdir)/../util
encrypt_decrypt_LDADD = ../crypto/libmoshcrypto.a ../util/libmoshutil.a $(CRYPTO_LIBS)

base64_SOURCES = base64.cc base64_vector.cc base64_vector.h genbase64.pl
base64_CPPFLAGS = $(ocb_aes_CPPFLAGS)
base64_LDADD = $(ocb_aes_LDADD)

clean-local: clean-local-check
.PHONY: clean-local-check
clean-local-check:
	-for i in $(displaytests); do rm -rf $$i.d/; done

CLEANFILES = base64_vector.cc
