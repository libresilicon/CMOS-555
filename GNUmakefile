#   ************    LibreSilicon's CMOS-555     ***********************
#
#   Organisation:   Chipforge
#                   Germany / European Union
#
#   Profile:        Chipforge focus on fine System-on-Chip Cores in
#                   Verilog HDL Code which are easy understandable and
#                   adjustable. For further information see
#                           www.chipforge.org
#                   there are projects from small cores up to PCBs, too.
#
#   File:           CMOS-555/GNUmakefile
#
#   Purpose:        Root Makefile
#
#   ************    GNU Make 3.80 Source Code       ****************
#
#   ////////////////////////////////////////////////////////////////
#
#   Copyright (c) 2019 by chipforge <CMOS-555@nospam.chipforge.org>
#   All rights reserved.
#
#       This Standard Cell Library is licensed under the Libre Silicon
#       public license; you can redistribute it and/or modify it under
#       the terms of the Libre Silicon public license as published by
#       the Libre Silicon alliance, either version 1 of the License, or
#       (at your option) any later version.
#
#       This design is distributed in the hope that it will be useful,
#       but WITHOUT ANY WARRANTY; without even the implied warranty of
#       MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#       See the Libre Silicon Public License for more details.
#
#   ////////////////////////////////////////////////////////////////////

#   ----------------------------------------------------------------
#               DEFINITIONS
#   ----------------------------------------------------------------

#   project name

PROJECT =       CMOS-555

#   directory pathes

DOCUMENTSDIR =  Documents
SIMULATIONDIR = Simulation
SOURCESDIR =    Sources
TBENCHDIR =     TBench

#   tool variables

ECHO ?=         @echo # -e
MV ?=           mv
RM ?=           rm -f
TAR ?=          tar -zh
DATE :=         $(shell date +%Y%m%d)

#   project tools

DISTRIBUTION =  GNUmakefile README.md \
                $(DOCUMENTSDIR) \
                $(SOURCESDIR) \
                $(SIMULATIONDIR) \
                $(TBENCHDIR)
#NETLIST ?=      lepton-netlist -g spice-sdb -o
NETLIST ?=      gnetlist -g spice-sdb -o
SPICE ?=        ngspice -b -c

#   others

.SUFFIXES:      # delete all default suffix rules

TESTS =         $(patsubst %.sch,%,$(notdir $(wildcard $(TBENCHDIR)/geda/*.sch)))

#   ----------------------------------------------------------------
#               DEFAULT TARGETS
#   ----------------------------------------------------------------

#   display help screen if no target is specified

.PHONY: help
help:
	$(ECHO) "-------------------------------------------------------------------"
	$(ECHO) "    available targets:"
	$(ECHO) "-------------------------------------------------------------------"
	$(ECHO) ""
	$(ECHO) "    help       - print this help screen"
	$(ECHO) "    dist       - build a tarball with all important files"
	$(ECHO) "    clean      - clean up all intermediate files"
	$(ECHO) ""
	$(ECHO) "    doc        - compile documentation"
	$(ECHO) ""
	$(ECHO) "    <simulation> - run this specified test case (see list below)"
	$(ECHO) "    sim        - run all simulations (see list below)"

	$(ECHO) ""
	$(ECHO) "-------------------------------------------------------------------"
	$(ECHO) "    available simulations:"
	$(ECHO) "-------------------------------------------------------------------"
	$(ECHO) ""
	$(ECHO) "$(TESTS)"
	$(ECHO) ""

#   make archive by building a tarball with all important files

.PHONY: dist
dist: clean
	$(ECHO) "---- build a tarball with all important files ----"
	$(TAR) -cvf $(PROJECT)_$(DATE).tgz $(DISTRIBUTION)

#   well, 'clean' directories before distributing

.PHONY: clean
clean:
	$(ECHO) "---- clean up all intermediate files ----"
	$(MAKE) -C $(DOCUMENTSDIR)/LaTeX -f GNUmakefile $@
	$(RM) $(SOURCESDIR)/spice/*.cir
	$(RM) $(TBENCHDIR)/spice/*.sp
	$(RM) $(SIMULATIONDIR)/spice/*.txt

#   run LaTeX for data sheets etc.

.PHONY: doc
doc:
	$(ECHO) "---- documentation, data sheet etc. ----"
	$(MAKE) -C $(DOCUMENTSDIR)/LaTeX -f GNUmakefile $@

#   run all simulations at once

#   ----------------------------------------------------------------
#               SIMULATION TARGETS
#   ----------------------------------------------------------------

#   common simulation target

.PHONY: sim
sim:    $(TESTS)

#   Use-Case Astable Mode

Use-Case_astable-mode:  $(SIMULATIONDIR)/Use-Case_astable-mode.txt

$(SIMULATIONDIR)/Use-Case_astable-mode.txt:   $(SOURCESDIR)/spice/555_Book-Version.cir $(TBENCHDIR)/spice/Use-Case_astable-mode.sp
	$(SPICE) $? > $@

$(TBENCHDIR)/spice/Use-Case_astable-mode.sp:    $(TBENCHDIR)/geda/Use-Case_astable-mode.sch # $(SIMULATIONDIR)/spice/Use-Case_astable-mode.cmd
	$(NETLIST) $@ $<

#   555 Circuits

$(SOURCESDIR)/spice/555_Book-Version.cir:   $(SOURCESDIR)/geda/555_Book-Version.sch
	$(NETLIST) $@ $?

$(SOURCESDIR)/spice/555_Righto-Version.cir:   $(SOURCESDIR)/geda/555_Righto-Version.sch
	$(NETLIST) $@ $?

$(SOURCESDIR)/spice/555_Wikimedia-Version.cir:   $(SOURCESDIR)/geda/555_Wikimedia-Version.sch
	$(NETLIST) $@ $?

#$(SOURCESDIR)/spice/555_Data-Sheet-Version.cir:   $(SOURCESDIR)/geda/555_Data-Sheet-Version.sch
#	$(NETLIST) $@ $?

