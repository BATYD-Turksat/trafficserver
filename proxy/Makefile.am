# proxy Makefile.am
#
#  Licensed to the Apache Software Foundation (ASF) under one
#  or more contributor license agreements.  See the NOTICE file
#  distributed with this work for additional information
#  regarding copyright ownership.  The ASF licenses this file
#  to you under the Apache License, Version 2.0 (the
#  "License"); you may not use this file except in compliance
#  with the License.  You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
#  Unless required by applicable law or agreed to in writing, software
#  distributed under the License is distributed on an "AS IS" BASIS,
#  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#  See the License for the specific language governing permissions and
#  limitations under the License.

# Note that hdrs is targeted from ../Makefile.am
SUBDIRS = congest http http2 spdy logging config
noinst_LIBRARIES =
bin_PROGRAMS = \
  traffic_server \
  traffic_logcat \
  traffic_logstats \
  traffic_sac

noinst_PROGRAMS = \
  test_xml_parser

TESTS = \
  tests/test_logstats_json \
  tests/test_logstats_summary \
  test_xml_parser

AM_CPPFLAGS = \
  $(iocore_include_dirs) \
  -I$(top_srcdir)/lib/records \
  -I$(top_srcdir)/lib/ts \
  -I$(srcdir)/http \
  -I$(srcdir)/spdy \
  -I$(srcdir)/logging \
  -I$(srcdir)/http/remap  \
  -I$(srcdir)/hdrs \
  -I$(srcdir)/shared \
  -I$(top_srcdir)/mgmt \
  -I$(top_srcdir)/mgmt/utils \
  -I$(top_srcdir)/proxy/api/ts \
  -I$(top_srcdir)/lib \
  -I$(top_builddir)/lib

noinst_HEADERS = \
  ConfigParse.h \
  Show.h

# These are currently built separate, as part of building the lib/ tree, using
# the normal LuaJIT build system. We are using the .o's directly, instead of the
# luajit.a to avoid the linker from optimizing symbols away. We could maybe
# switch to using the luajit.so, but that involves making sure it installs safely
# and cleanly.
LUAJIT = \
  lib_aux.o \
  lib_base.o \
  lib_bit.o \
  lib_debug.o \
  lib_ffi.o \
  lib_init.o \
  lib_io.o \
  lib_jit.o \
  lib_math.o \
  lib_os.o \
  lib_package.o \
  lib_string.o \
  lib_table.o \
  lj_alloc.o \
  lj_api.o \
  lj_asm.o \
  lj_bc.o \
  lj_bcread.o \
  lj_bcwrite.o \
  lj_carith.o \
  lj_ccall.o \
  lj_ccallback.o \
  lj_cconv.o \
  lj_cdata.o \
  lj_char.o \
  lj_clib.o \
  lj_cparse.o \
  lj_crecord.o \
  lj_ctype.o \
  lj_debug.o \
  lj_dispatch.o \
  lj_err.o \
  lj_ffrecord.o \
  lj_func.o \
  lj_gc.o \
  lj_gdbjit.o \
  lj_ir.o \
  lj_lex.o \
  lj_lib.o \
  lj_load.o \
  lj_mcode.o \
  lj_meta.o \
  lj_obj.o \
  lj_opt_dce.o \
  lj_opt_fold.o \
  lj_opt_loop.o \
  lj_opt_mem.o \
  lj_opt_narrow.o \
  lj_opt_sink.o \
  lj_opt_split.o \
  lj_parse.o \
  lj_record.o \
  lj_snap.o \
  lj_state.o \
  lj_str.o \
  lj_strscan.o \
  lj_tab.o \
  lj_trace.o \
  lj_udata.o \
  lj_vm.o \
  lj_vmevent.o \
  lj_vmmath.o

if STATIC_LIBTS
    which_libts = $(top_builddir)/lib/ts/.libs/libtsutil.a
else
    which_libts = $(top_builddir)/lib/ts/libtsutil.la
endif

EXTRA_DIST = InkAPITestTool.cc example_alarm_bin.sh example_prep.sh

traffic_server_SOURCES = \
  AbstractBuffer.cc \
  AbstractBuffer.h \
  CacheControl.cc \
  CacheControl.h \
  ControlBase.cc \
  ControlBase.h \
  ControlMatcher.cc \
  ControlMatcher.h \
  CoreUtils.cc \
  CoreUtils.h \
  DynamicStats.h \
  EventName.cc \
  FetchSM.cc \
  HttpTransStats.h \
  ICP.cc \
  ICP.h \
  ICPConfig.cc \
  ICPProcessor.cc \
  ICPProcessor.h \
  ICPStats.cc \
  ICPevents.h \
  ICPlog.h \
  IPAllow.cc \
  IPAllow.h \
  InkAPI.cc \
  InkAPIInternal.h \
  InkIOCoreAPI.cc \
  Main.cc \
  Main.h \
  ParentSelection.cc \
  ParentSelection.h \
  Plugin.cc \
  Plugin.h \
  PluginVC.cc \
  PluginVC.h \
  Prefetch.cc \
  Prefetch.h \
  ProtocolProbeSessionAccept.cc \
  ProtocolProbeSessionAccept.h \
  ProxyClientSession.cc \
  ProxyClientSession.h \
  ReverseProxy.cc \
  ReverseProxy.h \
  SocksProxy.cc \
  StatPages.cc \
  StatPages.h \
  StatSystem.cc \
  StatSystem.h \
  Transform.cc \
  Transform.h \
  TransformInternal.h \
  Update.cc \
  Update.h

if BUILD_TESTS
  traffic_server_SOURCES +=  InkAPITest.cc  \
    RegressionSM.h \
    RegressionSM.cc
endif

traffic_server_LDFLAGS = @EXTRA_CXX_LDFLAGS@ @LIBTOOL_LINK_FLAGS@
traffic_server_LDADD = \
  http/libhttp.a \
  http2/libhttp2.a \
  spdy/libspdy.a \
  http/remap/libhttp_remap.a \
  congest/libCongestionControl.a \
  logging/liblogging.a \
  logging/liblogcollation.a \
  hdrs/libhdrs.a  \
  shared/liberror.a  \
  shared/libdiagsconfig.a  \
  shared/libsignals.a \
  shared/libxml.a \
  $(top_builddir)/mgmt/libmgmt_p.la \
  $(top_builddir)/iocore/utils/libinkutils.a \
  $(top_builddir)/iocore/cluster/libinkcluster.a \
  $(top_builddir)/iocore/dns/libinkdns.a \
  $(top_builddir)/iocore/hostdb/libinkhostdb.a \
  $(top_builddir)/iocore/dns/libinkdns.a \
  $(top_builddir)/iocore/cluster/libinkcluster.a \
  $(top_builddir)/iocore/cache/libinkcache.a \
  $(top_builddir)/iocore/aio/libinkaio.a \
  $(top_builddir)/iocore/net/libinknet.a \
  $(top_builddir)/iocore/eventsystem/libinkevent.a \
  $(top_builddir)/lib/records/librecords_p.a \
  $(top_builddir)/iocore/eventsystem/libinkevent.a \
  $(which_libts) \
  @HWLOC_LIBS@ \
  @LIBPCRE@ \
  @OPENSSL_LIBS@ \
  @LIBTCL@ \
  @LIBEXPAT@ \
  @LIBDEMANGLE@ \
  @LIBCAP@ \
  @LIBRESOLV@ \
  @LIBZ@ \
  @LIBLZMA@ \
  @LIBPROFILER@ \
  @SPDYLAY_LIBS@ \
  -lm

if BUILD_LUAJIT
  traffic_server_LDADD += $(LUAJIT:%=$(top_builddir)/lib/luajit/src/%)
endif

# On Darwin LuaJIT requires magic link options, otherwise it will crash in luaL_openlibs() at startup. See
# http://luajit.org/install.html.
traffic_server_LDFLAGS += @TS_LUAJIT_LDFLAGS@

traffic_logcat_SOURCES = logcat.cc
traffic_logcat_LDFLAGS = @EXTRA_CXX_LDFLAGS@ @LIBTOOL_LINK_FLAGS@
traffic_logcat_LDADD = \
  logging/liblogging.a \
  shared/libdiagsconfig.a \
  shared/libUglyLogStubs.a \
  shared/libsignals.a \
  shared/libxml.a \
  $(top_builddir)/mgmt/libmgmt_p.la \
  $(top_builddir)/lib/records/librecords_p.a \
  $(top_builddir)/iocore/eventsystem/libinkevent.a \
  $(top_builddir)/lib/ts/libtsutil.la \
  @LIBRESOLV@ @LIBPCRE@ @OPENSSL_LIBS@ @LIBTCL@ @HWLOC_LIBS@ \
  @LIBEXPAT@ @LIBDEMANGLE@ @LIBPROFILER@ -lm

traffic_logstats_SOURCES = logstats.cc
traffic_logstats_LDFLAGS = @EXTRA_CXX_LDFLAGS@ @LIBTOOL_LINK_FLAGS@
traffic_logstats_LDADD = \
  logging/liblogging.a \
  shared/libdiagsconfig.a \
  shared/libUglyLogStubs.a \
  shared/libsignals.a \
  shared/libxml.a \
  $(top_builddir)/mgmt/libmgmt_p.la \
  $(top_builddir)/lib/records/librecords_p.a \
  $(top_builddir)/iocore/eventsystem/libinkevent.a \
  $(top_builddir)/lib/ts/libtsutil.la \
  @LIBRESOLV@ @LIBPCRE@ @OPENSSL_LIBS@ @LIBTCL@ @HWLOC_LIBS@ \
  @LIBEXPAT@ @LIBDEMANGLE@ @LIBPROFILER@ -lm

traffic_sac_SOURCES = \
  sac.cc \
  ICP.cc \
  ICPConfig.cc \
  ICPProcessor.cc \
  ICPStats.cc \
  IPAllow.cc \
  ParentSelection.cc \
  ControlBase.cc \
  ControlMatcher.cc \
  CacheControl.cc \
  StatSystem.cc \
  ReverseProxy.cc \
  EventName.cc \
  StatPages.cc \
  PluginVC.cc \
  AbstractBuffer.cc \
  Transform.cc \
  Prefetch.cc \
  ProtocolProbeSessionAccept.cc \
  ProtocolProbeSessionAccept.h \
  ProxyClientSession.cc \
  ProxyClientSession.h \
  Update.cc \
  Plugin.cc \
  InkAPI.cc \
  FetchSM.cc \
  InkIOCoreAPI.cc

traffic_sac_LDFLAGS = @EXTRA_CXX_LDFLAGS@ @LIBTOOL_LINK_FLAGS@
traffic_sac_LDADD = \
  http/libhttp.a \
  http2/libhttp2.a \
  spdy/libspdy.a \
  shared/libdiagsconfig.a \
  http/remap/libhttp_remap.a \
  congest/libCongestionControl.a \
  logging/liblogging.a \
  logging/liblogcollation.a \
  hdrs/libhdrs.a \
  shared/liberror.a \
  shared/libsignals.a \
  shared/libxml.a \
  $(top_builddir)/mgmt/libmgmt_p.la \
  $(top_builddir)/iocore/cluster/libinkcluster.a \
  $(top_builddir)/iocore/dns/libinkdns.a \
  $(top_builddir)/iocore/hostdb/libinkhostdb.a \
  $(top_builddir)/iocore/cluster/libinkcluster.a \
  $(top_builddir)/iocore/cache/libinkcache.a \
  $(top_builddir)/iocore/utils/libinkutils.a \
  $(top_builddir)/iocore/aio/libinkaio.a \
  $(top_builddir)/iocore/net/libinknet.a \
  $(top_builddir)/iocore/eventsystem/libinkevent.a \
  $(top_builddir)/lib/records/librecords_p.a \
  $(top_builddir)/lib/ts/libtsutil.la \
  @LIBRESOLV@ @LIBPCRE@ @OPENSSL_LIBS@ @LIBTCL@ @HWLOC_LIBS@ \
  @LIBEXPAT@ @LIBDEMANGLE@ @LIBZ@ @LIBLZMA@ @LIBPROFILER@ @SPDYLAY_LIBS@ -lm

if BUILD_TESTS
  traffic_sac_SOURCES += RegressionSM.cc
endif


test_xml_parser_SOURCES = test_xml_parser.cc
test_xml_parser_LDADD = \
  $(top_builddir)/mgmt/libmgmt_p.la \
  $(top_builddir)/lib/records/librecords_p.a \
  $(top_builddir)/iocore/eventsystem/libinkevent.a \
  $(top_builddir)/lib/ts/libtsutil.la \
  shared/libsignals.a \
  shared/libxml.a \
  @LIBTCL@

versiondir = $(pkgsysconfdir)

install-data-local:
	if [ `id -un` != "root" ]; then \
		$(INSTALL) -d $(DESTDIR)$(pkglocalstatedir) $(DESTDIR)$(pkglogdir) $(DESTDIR)$(pkgruntimedir) \
				$(DESTDIR)$(pkgsysconfdir) $(DESTDIR)$(pkgdatadir) $(DESTDIR)$(pkgcachedir); \
	else \
		 $(INSTALL) -d $(DESTDIR)$(pkglocalstatedir); \
		 $(INSTALL) -d -o $(pkgsysuser) -g $(pkgsysgroup) $(DESTDIR)$(pkglogdir) \
				$(DESTDIR)$(pkgruntimedir) $(DESTDIR)$(pkgsysconfdir) \
				$(DESTDIR)$(pkgdatadir) $(DESTDIR)$(pkgcachedir); \
	fi

install-data-hook:
	if [ `id -un` == "root" ]; then \
		chown -R $(pkgsysuser):$(pkgsysgroup) $(DESTDIR)$(pkgsysconfdir) $(DESTDIR)$(pkgdatadir);\
	fi
	-echo "<TS_VERSION> $(PACKAGE_VERSION)" > $(DESTDIR)$(pkgsysconfdir)/trafficserver-release
