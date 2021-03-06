#! /usr/bin/make -f
SHELL=/bin/bash
BUILD_DIR = obj
default: login-server char-server map-server ladmin eathena-monitor
.DELETE_ON_ERROR:
include make.defs

.PHONY: all clean common
# With no prerequisites, no target should ever be implicitly deleted.
# With any prerequisites, those targets won't be (no patterns).
.SECONDARY:
# This does the same, but only for its prerequisites.
# Unlike .SECONDARY, these may be patterns as well as normal prerequisites.
# .PRECIOUS: %/.

%/.:
	+mkdir -p $@

# The default recipe is suboptimal
%.cpp: %.lpp
	$(LEX) -o $@ $<
%.cpp %.h: %.ypp
	$(BISON) -d -o $*.cpp $<


# All this duplication is required because make handles pattern rules specially
${BUILD_DIR}/char/%.o: src/char/%.cpp | ${BUILD_DIR}/char/.
	$(COMPILE.cpp) -o $@ $<
${BUILD_DIR}/common/%.o: src/common/%.cpp | ${BUILD_DIR}/common/.
	$(COMPILE.cpp) -o $@ $<
${BUILD_DIR}/ladmin/%.o: src/ladmin/%.cpp | ${BUILD_DIR}/ladmin/.
	$(COMPILE.cpp) -o $@ $<
${BUILD_DIR}/login/%.o: src/login/%.cpp | ${BUILD_DIR}/login/.
	$(COMPILE.cpp) -o $@ $<
${BUILD_DIR}/map/%.o: src/map/%.cpp | ${BUILD_DIR}/map/.
	$(COMPILE.cpp) -o $@ $<
${BUILD_DIR}/tool/%.o: src/tool/%.cpp | ${BUILD_DIR}/tool/.
	$(COMPILE.cpp) -o $@ $<
${BUILD_DIR}/webserver/%.o: src/webserver/%.cpp | ${BUILD_DIR}/webserver/.
	$(COMPILE.cpp) -o $@ $<
${BUILD_DIR}/webserver/pages/%.o: src/webserver/pages/%.cpp | ${BUILD_DIR}/webserver/pages/.
	$(COMPILE.cpp) -o $@ $<

PROGS = login-server char-server map-server ladmin eathena-monitor webserver
# Things to actually make
all: ${PROGS}
clean:
	rm -rf ${PROGS} ${BUILD_DIR}/
common: ${BUILD_DIR}/common/core.o ${BUILD_DIR}/common/db.o ${BUILD_DIR}/common/grfio.o ${BUILD_DIR}/common/lock.o ${BUILD_DIR}/common/md5calc.o ${BUILD_DIR}/common/mt_rand.o ${BUILD_DIR}/common/nullpo.o ${BUILD_DIR}/common/socket.o ${BUILD_DIR}/common/timer.o ${BUILD_DIR}/common/utils.o

# Top level programs
login-server: ${BUILD_DIR}/login/login
	cp -f $< $@
char-server: ${BUILD_DIR}/char/char
	cp -f $< $@
map-server: ${BUILD_DIR}/map/map
	cp -f $< $@
ladmin: ${BUILD_DIR}/ladmin/ladmin
	cp -f $< $@
eathena-monitor: ${BUILD_DIR}/tool/eathena-monitor
	cp -f $< $@
webserver: ${BUILD_DIR}/webserver/main
	cp -f $< $@

# Executable dependencies - generated by hand
${BUILD_DIR}/char/char: ${BUILD_DIR}/char/char.o ${BUILD_DIR}/char/inter.o ${BUILD_DIR}/char/int_party.o ${BUILD_DIR}/char/int_guild.o ${BUILD_DIR}/char/int_storage.o ${BUILD_DIR}/common/core.o ${BUILD_DIR}/common/socket.o ${BUILD_DIR}/common/timer.o ${BUILD_DIR}/common/db.o ${BUILD_DIR}/common/lock.o ${BUILD_DIR}/common/mt_rand.o ${BUILD_DIR}/common/utils.o
${BUILD_DIR}/ladmin/ladmin: ${BUILD_DIR}/ladmin/ladmin.o ${BUILD_DIR}/common/md5calc.o ${BUILD_DIR}/common/core.o ${BUILD_DIR}/common/socket.o ${BUILD_DIR}/common/timer.o ${BUILD_DIR}/common/db.o ${BUILD_DIR}/common/mt_rand.o ${BUILD_DIR}/common/utils.o
${BUILD_DIR}/login/login: ${BUILD_DIR}/login/login.o ${BUILD_DIR}/common/core.o ${BUILD_DIR}/common/socket.o ${BUILD_DIR}/common/timer.o ${BUILD_DIR}/common/db.o ${BUILD_DIR}/common/lock.o ${BUILD_DIR}/common/mt_rand.o ${BUILD_DIR}/common/md5calc.o ${BUILD_DIR}/common/utils.o
${BUILD_DIR}/map/map: ${BUILD_DIR}/map/map.o ${BUILD_DIR}/map/tmw.o ${BUILD_DIR}/map/magic-interpreter-lexer.o ${BUILD_DIR}/map/magic-interpreter-parser.o ${BUILD_DIR}/map/magic-interpreter-base.o ${BUILD_DIR}/map/magic-expr.o ${BUILD_DIR}/map/magic-stmt.o ${BUILD_DIR}/map/magic.o ${BUILD_DIR}/map/map.o ${BUILD_DIR}/map/chrif.o ${BUILD_DIR}/map/clif.o ${BUILD_DIR}/map/pc.o ${BUILD_DIR}/map/npc.o ${BUILD_DIR}/map/chat.o ${BUILD_DIR}/map/path.o ${BUILD_DIR}/map/itemdb.o ${BUILD_DIR}/map/mob.o ${BUILD_DIR}/map/script.o ${BUILD_DIR}/map/storage.o ${BUILD_DIR}/map/skill.o ${BUILD_DIR}/map/skill-pools.o ${BUILD_DIR}/map/atcommand.o ${BUILD_DIR}/map/battle.o ${BUILD_DIR}/map/intif.o ${BUILD_DIR}/map/trade.o ${BUILD_DIR}/map/party.o ${BUILD_DIR}/map/guild.o ${BUILD_DIR}/common/core.o ${BUILD_DIR}/common/socket.o ${BUILD_DIR}/common/timer.o ${BUILD_DIR}/common/grfio.o ${BUILD_DIR}/common/db.o ${BUILD_DIR}/common/lock.o ${BUILD_DIR}/common/nullpo.o ${BUILD_DIR}/common/mt_rand.o ${BUILD_DIR}/common/md5calc.o ${BUILD_DIR}/common/utils.o
${BUILD_DIR}/tool/eathena-monitor: ${BUILD_DIR}/tool/eathena-monitor.o
${BUILD_DIR}/tool/adduser: ${BUILD_DIR}/tool/adduser.o ${BUILD_DIR}/common/socket.o
${BUILD_DIR}/tool/itemfrob: ${BUILD_DIR}/tool/itemfrob.o ${BUILD_DIR}/common/timer.o ${BUILD_DIR}/common/socket.o ${BUILD_DIR}/common/db.o ${BUILD_DIR}/common/lock.o ${BUILD_DIR}/char/inter.o ${BUILD_DIR}/char/int_guild.o ${BUILD_DIR}/char/int_party.o ${BUILD_DIR}/char/int_storage.o
${BUILD_DIR}/tool/mapfrob: ${BUILD_DIR}/tool/mapfrob.o ${BUILD_DIR}/common/timer.o ${BUILD_DIR}/common/socket.o ${BUILD_DIR}/common/db.o ${BUILD_DIR}/common/lock.o ${BUILD_DIR}/char/inter.o ${BUILD_DIR}/char/int_guild.o ${BUILD_DIR}/char/int_party.o ${BUILD_DIR}/char/int_storage.o
${BUILD_DIR}/tool/marriage-info: ${BUILD_DIR}/tool/marriage-info.o ${BUILD_DIR}/common/timer.o ${BUILD_DIR}/common/socket.o ${BUILD_DIR}/common/db.o ${BUILD_DIR}/common/lock.o ${BUILD_DIR}/char/inter.o ${BUILD_DIR}/char/int_guild.o ${BUILD_DIR}/char/int_party.o ${BUILD_DIR}/char/int_storage.o
${BUILD_DIR}/webserver/main: ${BUILD_DIR}/webserver/main.o ${BUILD_DIR}/webserver/parse.o ${BUILD_DIR}/webserver/generate.o ${BUILD_DIR}/webserver/htmlstyle.o ${BUILD_DIR}/webserver/logs.o ${BUILD_DIR}/webserver/pages/about.o ${BUILD_DIR}/webserver/pages/sample.o ${BUILD_DIR}/webserver/pages/notdone.o

# deps.make is *NOT* automatically rebuilt normally
# but the generated source files do need to be done first
deps.make: src/map/magic-interpreter-parser.cpp src/map/magic-interpreter-lexer.cpp
	for F in `find src/ -name '*.cpp'`; do \
	    ${CXX} ${CPPFLAGS} -MM "$$F" -MT "$$(sed 's/src/$${BUILD_DIR}/;s/\.cpp/.o/' <<< "$$F")"; \
	done > deps.make

include deps.make

prefix=/usr/local
install:
	install -d ${prefix}/bin/
	install -t ${prefix}/bin/ $(wildcard ${PROGS})
