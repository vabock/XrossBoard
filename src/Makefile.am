AUTOMAKE_OPTIONS 	= foreign subdir-objects
EXTRA_DIST		= rc
EXTRA_DATA		= $(wildcard rc/*)

bin_PROGRAMS 		= xrossboard

xrossboardexecrcdir	= $(prefix)/share/pixmaps/@PACKAGE@
xrossboardexecrc_DATA	= $(wildcard rc/*)

xrossboardexecscriptdir	= $(datarootdir)/@PACKAGE@/script
xrossboardexecscript_DATA= $(wildcard script/*)

xrossboard_SOURCES 	= extractboardlist.hpp        \
		          main.cpp                    \
		          socketcommunication.cpp     \
		          anchoredresponsepopup.cpp   \
		          xrossboard.cpp               \
		          sqliteaccessor.cpp          \
		          socketcommunication.hpp     \
		          virtualboardlistctrl.cpp    \
		          anchoredresponsepopup.hpp   \
		          xrossboard.hpp               \
		          sqliteaccessor.hpp          \
		          threadcontentbar.cpp        \
		          virtualboardlistctrl.hpp    \
		          datatype.hpp                \
		          xrossboardutil.cpp           \
		          responsewindow.cpp          \
		          threadcontentbar.hpp        \
		          extractboardlist.cpp        \
		          xrossboardutil.hpp           \
		          responsewindow.hpp          \
		          xrossboardimageviewer.cpp    \
		          xrossboardimageviewer.hpp    \
		          imagepanel.cpp	      \
			  imagepanel.hpp	      \
			  settingwindow.cpp	      \
			  settingwindow.hpp	      \
			  otherpanels.cpp	      \
			  otherpanels.hpp	      \
		          drawpane.cpp                \
		          drawpane.hpp                \
		          enums.hpp		      \
		          enumstring.hpp              \
		          xrossboarduiutil.cpp         \
		          xrossboarduiutil.hpp         \
			  ../babel/babel.cpp          \
			  ../babel/babel.h            \
			  ../json11/json11.cpp	      \
			  ../json11/json11.hpp

if USE_WX_WEBVIEW
# wxWebView support
xrossboard_SOURCES += threadcontentwebview.cpp   \
		     threadcontentwebview.hpp

JC_FLAG_STRING	   = `@WX_CONFIG_PATH@ --version=@WX_VERSION_MAJOR@.@WX_VERSION_MINOR@ --libs aui,qa,adv,base,core,html,net,xrc,webview`

# javascript
EXTRA_DIST		+= script
EXTRA_SCRIPTS		= $(wildcard script/*)

else
# Use wxHtmlWindow
xrossboard_SOURCES += threadcontentwindow.cpp    \
		     threadcontentwindow.hpp

JC_FLAG_STRING	   = `@WX_CONFIG_PATH@ --version=@WX_VERSION_MAJOR@.@WX_VERSION_MINOR@ --libs aui,qa,adv,base,core,html,net,xrc`
endif

# common build rule
xrossboard_CXXFLAGS = @CXXFLAGS@ @XML2CFLAGS@ @CRYPTO_CFLAGS@ \
		     -I$(top_builddir)/babel          \
		     -I$(top_builddir)/src/rc

ACLOCAL_AMFLAGS    = -I m4

# For Icon build and library dependency
if USE_WINDRES
# Platform is Windows
xrossboard_LDFLAGS  = $(JC_FLAG_STRING) -s
xrossboard_LDADD    = xrossboard_rc.o @XML2LIBS@ @CRYPTO_LIBS@ $(top_builddir)/cmdline_twitter/libctw.a

xrossboard_rc.o : $(top_builddir)/src/rc/icon.rc
	@WX_RESCOMP@ -i $^ -O coff -o $@

else
# Platform is not Windows
xrossboard_LDFLAGS  = $(JC_FLAG_STRING)
xrossboard_LDADD    = @XML2LIBS@ @CRYPTO_LIBS@ $(top_builddir)/cmdline_twitter/libctw.a

endif

# Build or not
if BUILDING_WXSQLITE3
  xrossboard_CXXFLAGS += -I$(top_builddir)/wxsqlite3
  xrossboard_LDADD    += $(top_builddir)/wxsqlite3/libwxsqlite3.a
endif

if BUILDING_SQLITE3
  xrossboard_CXXFLAGS += -I$(top_builddir)/sqlite3
  xrossboard_LDADD    += $(top_builddir)/sqlite3/libsqlite3.a
else
  xrossboard_LDFLAGS  += -lsqlite3
endif

if BUILDING_CURLPP
  xrossboard_CXXFLAGS += -I$(top_builddir)/curlpp/include
  xrossboard_LDADD    += $(top_builddir)/curlpp/src/curlpp/libcurlpp.la 	          \
		        $(top_builddir)/curlpp/src/utilspp/libutilspp.la 	  \
		        $(top_builddir)/curlpp/src/curlpp/internal/libinternal.la
endif
