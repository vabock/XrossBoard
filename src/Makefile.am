bin_PROGRAMS      = JaneClone
JaneClone_SOURCES = extractboardlist.hpp        \
					main.cpp                    \
					socketcommunication.cpp     \
					threadcontentwindow.hpp     \
					anchoredresponsepopup.cpp   \
					janeclone.cpp               \
					metakitaccessor.cpp         \
					socketcommunication.hpp     \
					virtualboardlistctrl.cpp    \
					anchoredresponsepopup.hpp   \
					janeclone.hpp               \
					metakitaccessor.hpp         \
					threadcontentbar.cpp        \
					virtualboardlistctrl.hpp    \
					datatype.hpp                \
					janecloneutil.cpp           \
					responsewindow.cpp          \
					threadcontentbar.hpp        \
					extractboardlist.cpp        \
					janecloneutil.hpp           \
					responsewindow.hpp          \
					threadcontentwindow.cpp

JaneClone_CXXFLAGS = @CXXFLAGS@ @XML2CFLAGS@ -I../libwxnkf/libwxnkf -I../libwxnkf/include -I../libmk4/include -I../rc
JaneClone_LDADD    = @LIBS@ @XML2LIBS@ ../libmk4/libmk4/libmk4.la ../libmk4/libmk4/libmk4.la
ACLOCAL_AMFLAGS    = -I m4

if USE_WINDRES
JaneClone_LDADD += JaneClone_rc.o
endif

if USE_WINDRES
JaneClone_rc.o : ../rc/icon.rc
	@WX_RESCOMP@ -i $^ -O coff -o $@
endif