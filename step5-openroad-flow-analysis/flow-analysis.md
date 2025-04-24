```makefile
# settings.mk is not under source control. Put variables into this
# file to avoid having to adding the to the make command line.
-include settings.mk

# ==============================================================================
# Uncomment or add the design to run
# ==============================================================================

# DESIGN_CONFIG=./designs/nangate45/aes/config.mk
# DESIGN_CONFIG=./designs/nangate45/ariane133/config.mk
# DESIGN_CONFIG=./designs/nangate45/ariane136/config.mk
# DESIGN_CONFIG=./designs/nangate45/black_parrot/config.mk
# DESIGN_CONFIG=./designs/nangate45/bp_be_top/config.mk
# DESIGN_CONFIG=./designs/nangate45/bp_fe_top/config.mk
# DESIGN_CONFIG=./designs/nangate45/bp_multi_top/config.mk
# DESIGN_CONFIG=./designs/nangate45/bp_quad/config.mk
# DESIGN_CONFIG=./designs/nangate45/dynamic_node/config.mk
# DESIGN_CONFIG=./designs/nangate45/gcd/config.mk
# DESIGN_CONFIG=./designs/nangate45/ibex/config.mk
# DESIGN_CONFIG=./designs/nangate45/jpeg/config.mk
# DESIGN_CONFIG=./designs/nangate45/mempool_group/config.mk
# DESIGN_CONFIG=./designs/nangate45/swerv/config.mk
# DESIGN_CONFIG=./designs/nangate45/swerv_wrapper/config.mk
# DESIGN_CONFIG=./designs/nangate45/tinyRocket/config.mk

# DESIGN_CONFIG=./designs/gf12/aes/config.mk
# DESIGN_CONFIG=./designs/gf12/ariane/config.mk
# DESIGN_CONFIG=./designs/gf12/ca53/config.mk
# DESIGN_CONFIG=./designs/gf12/coyote/config.mk
# DESIGN_CONFIG=./designs/gf12/gcd/config.mk
# DESIGN_CONFIG=./designs/gf12/ibex/config.mk
# DESIGN_CONFIG=./designs/gf12/jpeg/config.mk
# DESIGN_CONFIG=./designs/gf12/swerv_wrapper/config.mk
# DESIGN_CONFIG=./designs/gf12/tinyRocket/config.mk

# DESIGN_CONFIG=./designs/gf12/ariane133/config.mk
# DESIGN_CONFIG=./designs/gf12/bp_dual/config.mk
# DESIGN_CONFIG=./designs/gf12/bp_quad/config.mk
# DESIGN_CONFIG=./designs/gf12/bp_single/config.mk

# DESIGN_CONFIG=./designs/sky130hd/aes/config.mk
# DESIGN_CONFIG=./designs/sky130hd/chameleon/config.mk
# DESIGN_CONFIG=./designs/sky130hd/gcd/config.mk
# DESIGN_CONFIG=./designs/sky130hd/ibex/config.mk
# DESIGN_CONFIG=./designs/sky130hd/jpeg/config.mk
# DESIGN_CONFIG=./designs/sky130hd/microwatt/config.mk
# DESIGN_CONFIG=./designs/sky130hd/riscv32i/config.mk

# DESIGN_CONFIG=./designs/sky130hs/aes/config.mk
# DESIGN_CONFIG=./designs/sky130hs/gcd/config.mk
# DESIGN_CONFIG=./designs/sky130hs/ibex/config.mk
# DESIGN_CONFIG=./designs/sky130hs/jpeg/config.mk
# DESIGN_CONFIG=./designs/sky130hs/riscv32i/config.mk

# DESIGN_CONFIG=./designs/asap7/aes/config.mk
# DESIGN_CONFIG=./designs/asap7/ethmac/config.mk
# DESIGN_CONFIG=./designs/asap7/gcd/config.mk
# DESIGN_CONFIG=./designs/asap7/ibex/config.mk
# DESIGN_CONFIG=./designs/asap7/jpeg/config.mk
# DESIGN_CONFIG=./designs/asap7/megaboom/config.mk
# DESIGN_CONFIG=./designs/asap7/mock-array/config.mk
# DESIGN_CONFIG=./designs/asap7/riscv32i/config.mk
# DESIGN_CONFIG=./designs/asap7/swerv_wrapper/config.mk
# DESIGN_CONFIG=./designs/asap7/uart/config.mk

# DESIGN_CONFIG=./designs/intel16/aes/config.mk
# DESIGN_CONFIG=./designs/intel16/gcd/config.mk

# DESIGN_CONFIG=./designs/intel22/ibex/config.mk
# DESIGN_CONFIG=./designs/intel22/jpeg/config.mk

# DESIGN_CONFIG=./designs/gf180/aes/config.mk
# DESIGN_CONFIG=./designs/gf180/ibex/config.mk
# DESIGN_CONFIG=./designs/gf180/jpeg/config.mk
# DESIGN_CONFIG=./designs/gf180/riscv32i/config.mk
# DESIGN_CONFIG=./designs/gf180/uart-blocks/config.mk

# DESIGN_CONFIG=./designs/ihp-sg13g2/aes/config.mk
# DESIGN_CONFIG=./designs/ihp-sg13g2/ibex/config.mk
# DESIGN_CONFIG=./designs/ihp-sg13g2/gcd/config.mk
# DESIGN_CONFIG=./designs/ihp-sg13g2/spi/config.mk
# DESIGN_CONFIG=./designs/ihp-sg13g2/riscv32i/config.mk
# DESIGN_CONFIG=./designs/ihp-sg13g2/i2c-gpio-expander/config.mk

================================== My Note ==================================
=    Uses the '?=' operator, which assigns a value to the variable          =
=    only if it hasn't already been defined.                                =
=    This is called conditional assignment.                                 =
=    The right-hand side is evaluated immediately                           =
=    if the assignment happens.                                             =
=============================================================================
# Default design
DESIGN_CONFIG ?= ./designs/nangate45/gcd/config.mk
export DESIGN_CONFIG

include $(DESIGN_CONFIG)
#############################################################################
# ⬇️ Inline content from `config.mk` (for analysis purpose only)        ⬇️ #
#############################################################################
    export DESIGN_NAME = gcd
    export PLATFORM    = nangate45

================================== My Note ==================================
=    VERILOG_FILES is defined before DESIGN_HOME appears,                   =
=    but this works because Make uses *lazy evaluation* (`=`).              =
=    The value is not resolved until it's actually needed,                  =
=    by which time DESIGN_HOME will have been defined in variables.mk.      =
=============================================================================
    export VERILOG_FILES = $(DESIGN_HOME)/src/$(DESIGN_NAME)/gcd.v
    export SDC_FILE      = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NAME)/constraint.sdc
    export ABC_AREA      = 1
    
    # Adders degrade GCD
    export ADDER_MAP_FILE :=
    
    export CORE_UTILIZATION ?= 55
    export PLACE_DENSITY_LB_ADDON = 0.20
    export TNS_END_PERCENT        = 100
    export REMOVE_CELLS_FOR_EQY   = TAPCELL*
#############################################################################
# ⬆️ End of inline config.mk                                            ⬆️ #
#############################################################################

================================== My Note ==================================
=    $(dir ...) returns the directory portion of DESIGN_CONFIG.             =
=============================================================================
export DESIGN_DIR  = $(dir $(DESIGN_CONFIG))

# default value "base" is duplicated from variables.yaml because we need it
# earlier in the flow for BLOCKS. BLOCKS is a feature specific to the
# ORFS Makefile.
export FLOW_VARIANT?=base
# BLOCKS is a ORFS make flow specific feature.

================================== My Note ==================================
=    run this block only if BLOCKS is not empty.                            =
=============================================================================
ifneq ($(BLOCKS),)
  # Normally this comes from variables.yaml, but we need it here to set up these variables
  # which are part of the DESIGN_CONFIG. BLOCKS is a Makefile specific concept.

================================== My Note ==================================
=    Dynamically constructs and appends multiple design artifact paths      =
=    for each block in $(BLOCKS), using $(eval ...)                         =
=    to evaluate and assign Makefile code at runtime.                       =
=    This pattern builds composite variables                                =
=    like BLOCK_LEFS, BLOCK_LIBS, BLOCK_GDS, etc.                           =
=============================================================================
  $(foreach block,$(BLOCKS),$(eval BLOCK_LEFS += ./results/$(PLATFORM)/$(DESIGN_NICKNAME)_$(block)/$(FLOW_VARIANT)/${block}.lef))
  $(foreach block,$(BLOCKS),$(eval BLOCK_LIBS += ./results/$(PLATFORM)/$(DESIGN_NICKNAME)_$(block)/$(FLOW_VARIANT)/${block}.lib))
  $(foreach block,$(BLOCKS),$(eval BLOCK_GDS += ./results/$(PLATFORM)/$(DESIGN_NICKNAME)_$(block)/$(FLOW_VARIANT)/6_final.gds))
  $(foreach block,$(BLOCKS),$(eval BLOCK_CDL += ./results/$(PLATFORM)/$(DESIGN_NICKNAME)_$(block)/$(FLOW_VARIANT)/6_final.cdl))
  $(foreach block,$(BLOCKS),$(eval BLOCK_LOG_FOLDERS += ./logs/$(PLATFORM)/$(DESIGN_NICKNAME)_$(block)/$(FLOW_VARIANT)/))
  export ADDITIONAL_LEFS += $(BLOCK_LEFS)
  export ADDITIONAL_LIBS += $(BLOCK_LIBS)
  export ADDITIONAL_GDS += $(BLOCK_GDS)
  export GDS_FILES += $(BLOCK_GDS)
  ifneq ($(CDL_FILES),)
    export CDL_FILES += $(BLOCK_CDL)
  endif
endif

# ==============================================================================
#  ____  _____ _____ _   _ ____
# / ___|| ____|_   _| | | |  _ \
# \___ \|  _|   | | | | | | |_) |
#  ___) | |___  | | | |_| |  __/
# |____/|_____| |_|  \___/|_|
#
# ==============================================================================

# Disable make's implicit rules
MAKEFLAGS += --no-builtin-rules
.SUFFIXES:

#-------------------------------------------------------------------------------
# Default target when invoking without specific target.
.DEFAULT_GOAL := finish

#-------------------------------------------------------------------------------
# Proper way to initiate SHELL for make
SHELL          := /usr/bin/env bash
.SHELLFLAGS    := -o pipefail -c


#-------------------------------------------------------------------------------
# Setup variables to point to root / head of the OpenROAD directory
# - the following settings allowed user to point OpenROAD binaries to different
#   location
# - default is current install / clone directory

================================== My Note ==================================
=    Checks whether the variable FLOW_HOME is undefined.                    =
=    'origin' returns the origin of the variable                            =
=    (e.g. environment, file, command line, or undefined).                  =
=    $(MAKEFILE_LIST) contains the list of all Makefiles                    =
=    that have been included so far, in order.                              =
=    $(firstword ...) returns the first one                                 =
=    — usually the top-level Makefile.                                      =
=============================================================================
ifeq ($(origin FLOW_HOME), undefined)
FLOW_HOME := $(abspath $(dir $(firstword $(MAKEFILE_LIST))))
endif
export FLOW_HOME

include $(FLOW_HOME)/scripts/variables.mk
#############################################################################
# ⬇️ Inline content from `variables.mk` (for analysis purpose only)     ⬇️ #
#############################################################################
    # Sets up ORFS variables using make variable support, relying
    # on makefile features such as defaults, forward references,
    # lazy evaluation, conditional code, include statements,
    # etc.
    
    # Setup variables to point to root / head of the OpenROAD directory
    # - the following settings allowed user to point OpenROAD binaries to different
    #   location
    # - default is current install / clone directory
    ifeq ($(origin FLOW_HOME), undefined)
    FLOW_HOME := $(abspath $(dir $(firstword $(MAKEFILE_LIST)))/..)
    endif
    export FLOW_HOME
    
    export DESIGN_NICKNAME?=$(DESIGN_NAME)
    
    #-------------------------------------------------------------------------------
    # Setup variables to point to other location for the following sub directory
    # - designs - default is under current directory
    # - platforms - default is under current directory
    # - work home - default is current directory
    # - utils, scripts, test - default is under current directory
    export DESIGN_HOME   ?= $(FLOW_HOME)/designs
    export PLATFORM_HOME ?= $(FLOW_HOME)/platforms

================================== My Note ==================================
=    Sets WORK_HOME to the current directory                                =
=    (where the Makefile is located) if it is not already defined.          =
=============================================================================
    export WORK_HOME     ?= .
    
    export UTILS_DIR     ?= $(FLOW_HOME)/util
    export SCRIPTS_DIR   ?= $(FLOW_HOME)/scripts
    export TEST_DIR      ?= $(FLOW_HOME)/test
    
    PUBLIC=nangate45 sky130hd sky130hs asap7 ihp-sg13g2 gf180
    
    ifeq ($(origin PLATFORM), undefined)
      $(error PLATFORM variable net set.)
    endif
    ifeq ($(origin DESIGN_NAME), undefined)
      $(error DESIGN_NAME variable net set.)
    endif

================================== My Note ==================================
=    $(wildcard <path>) returns the path if it exists,                      =
=    otherwise returns an empty string.                                     =
=    $(findstring <substring>, <string>) returns the substring if found,    =
=    otherwise returns an empty string.                                     =
=============================================================================
    ifneq ($(PLATFORM_DIR),)
    else ifneq ($(wildcard $(PLATFORM_HOME)/$(PLATFORM)),)
      export PLATFORM_DIR = $(PLATFORM_HOME)/$(PLATFORM)
    else ifneq ($(findstring $(PLATFORM),$(PUBLIC)),)
      export PLATFORM_DIR = ./platforms/$(PLATFORM)
    else ifneq ($(wildcard ../../$(PLATFORM)),)
      export PLATFORM_DIR = ../../$(PLATFORM)
    else
      $(error [ERROR][FLOW] Platform '$(PLATFORM)' not found.)
    endif
    
    include $(PLATFORM_DIR)/config.mk
#############################################################################
# ⬇️ Inline content from `config.mk` (for analysis purpose only)        ⬇️ #
#############################################################################
        # Process node
        export PROCESS = 130
        
        #-----------------------------------------------------
        # Tech/Libs
        # ----------------------------------------------------
        export TECH_LEF = $(PLATFORM_DIR)/lef/sky130_fd_sc_hd.tlef
        export SC_LEF = $(PLATFORM_DIR)/lef/sky130_fd_sc_hd_merged.lef
        
        export LIB_FILES = $(PLATFORM_DIR)/lib/sky130_fd_sc_hd__tt_025C_1v80.lib \
                             $(ADDITIONAL_LIBS)
        export GDS_FILES = $(wildcard $(PLATFORM_DIR)/gds/*.gds) \
                             $(ADDITIONAL_GDS)
        
        # Dont use cells to ease congestion
        # Specify at least one filler cell if none
        
        # The *probe* are for inserting probe points and have metal shapes
        # on all layers.
        # *lpflow* cells are for multi-power domains

================================== My Note ==================================
=    DONT_USE_CELLS is used to blacklist specific cells                     =
=    during synthesis or PnR.                                               =
=    This helps avoid congestion (large/complex cells),                     =
=    excludes special-purpose cells like *probe (DFT test points),          =
=    or lpflow (multi-VDD),                                                 =
=    and maintains design constraints and manufacturability.                =
=============================================================================
        export DONT_USE_CELLS += \
            sky130_fd_sc_hd__probe_p_8 sky130_fd_sc_hd__probec_p_8 \
            sky130_fd_sc_hd__lpflow_bleeder_1 \
            sky130_fd_sc_hd__lpflow_clkbufkapwr_1 \
            sky130_fd_sc_hd__lpflow_clkbufkapwr_16 \
            sky130_fd_sc_hd__lpflow_clkbufkapwr_2 \
            sky130_fd_sc_hd__lpflow_clkbufkapwr_4 \
            sky130_fd_sc_hd__lpflow_clkbufkapwr_8 \
            sky130_fd_sc_hd__lpflow_clkinvkapwr_1 \
            sky130_fd_sc_hd__lpflow_clkinvkapwr_16 \
            sky130_fd_sc_hd__lpflow_clkinvkapwr_2 \
            sky130_fd_sc_hd__lpflow_clkinvkapwr_4 \
            sky130_fd_sc_hd__lpflow_clkinvkapwr_8 \
            sky130_fd_sc_hd__lpflow_decapkapwr_12 \
            sky130_fd_sc_hd__lpflow_decapkapwr_3 \
            sky130_fd_sc_hd__lpflow_decapkapwr_4 \
            sky130_fd_sc_hd__lpflow_decapkapwr_6 \
            sky130_fd_sc_hd__lpflow_decapkapwr_8 \
            sky130_fd_sc_hd__lpflow_inputiso0n_1 \
            sky130_fd_sc_hd__lpflow_inputiso0p_1 \
            sky130_fd_sc_hd__lpflow_inputiso1n_1 \
            sky130_fd_sc_hd__lpflow_inputiso1p_1 \
            sky130_fd_sc_hd__lpflow_inputisolatch_1 \
            sky130_fd_sc_hd__lpflow_isobufsrc_1 \
            sky130_fd_sc_hd__lpflow_isobufsrc_16 \
            sky130_fd_sc_hd__lpflow_isobufsrc_2 \
            sky130_fd_sc_hd__lpflow_isobufsrc_4 \
            sky130_fd_sc_hd__lpflow_isobufsrc_8 \
            sky130_fd_sc_hd__lpflow_isobufsrckapwr_16 \
            sky130_fd_sc_hd__lpflow_lsbuf_lh_hl_isowell_tap_1 \
            sky130_fd_sc_hd__lpflow_lsbuf_lh_hl_isowell_tap_2 \
            sky130_fd_sc_hd__lpflow_lsbuf_lh_hl_isowell_tap_4 \
            sky130_fd_sc_hd__lpflow_lsbuf_lh_isowell_4 \
            sky130_fd_sc_hd__lpflow_lsbuf_lh_isowell_tap_1 \
            sky130_fd_sc_hd__lpflow_lsbuf_lh_isowell_tap_2 \
            sky130_fd_sc_hd__lpflow_lsbuf_lh_isowell_tap_4
        #
        # Define fill cells
        export FILL_CELLS ?= sky130_fd_sc_hd__fill_1 sky130_fd_sc_hd__fill_2 sky130_fd_sc_hd__fill_4 sky130_fd_sc_hd__fill_8
        
        # -----------------------------------------------------
        #  Yosys
        #  ----------------------------------------------------
        # Set the TIEHI/TIELO cells
        # These are used in yosys synthesis to avoid logical 1/0's in the netlist
        export TIEHI_CELL_AND_PORT = sky130_fd_sc_hd__conb_1 HI
        export TIELO_CELL_AND_PORT = sky130_fd_sc_hd__conb_1 LO
        
        # Used in synthesis
        export MIN_BUF_CELL_AND_PORTS = sky130_fd_sc_hd__buf_4 A X
        
        # Yosys mapping files
        export LATCH_MAP_FILE = $(PLATFORM_DIR)/cells_latch_hd.v
        export CLKGATE_MAP_FILE = $(PLATFORM_DIR)/cells_clkgate_hd.v
        export ADDER_MAP_FILE ?= $(PLATFORM_DIR)/cells_adders_hd.v
        
        # Define ABC driver and load
        export ABC_DRIVER_CELL = sky130_fd_sc_hd__buf_1
        export ABC_LOAD_IN_FF = 5
        
        # -----------------------------------------------------
        #  Sizing
        # -----------------------------------------------------
        
        export MATCH_CELL_FOOTPRINT = 1
        
        #--------------------------------------------------------
        # Floorplan
        # -------------------------------------------------------
        
        # Placement site for core cells
        # This can be found in the technology lef
        export PLACE_SITE = unithd
        
        # IO Placer pin layers
        export IO_PLACER_H ?= met3
        export IO_PLACER_V ?= met2
        
        # Define default PDN config
        export PDN_TCL ?= $(PLATFORM_DIR)/pdn.tcl
        
        # Endcap and Welltie cells
        export TAP_CELL_NAME = sky130_fd_sc_hd__tapvpwrvgnd_1
        export TAPCELL_TCL ?= $(PLATFORM_DIR)/tapcell.tcl
        
        export MACRO_PLACE_HALO ?= 40 40
        
        #---------------------------------------------------------
        # Place
        # --------------------------------------------------------
        export PLACE_DENSITY ?= 0.60
        
        # ---------------------------------------------------------
        #  Route
        # ---------------------------------------------------------
        # FastRoute options
        export MIN_ROUTING_LAYER ?= met1
        export MIN_CLK_ROUTING_LAYER ?= met3
        export MAX_ROUTING_LAYER ?= met5
        #
        # Define fastRoute tcl
        export FASTROUTE_TCL ?= $(PLATFORM_DIR)/fastroute.tcl
        
        # KLayout technology file
        export KLAYOUT_TECH_FILE = $(PLATFORM_DIR)/$(PLATFORM).lyt
        #
        # Rules for metal fill
        export FILL_CONFIG = $(PLATFORM_DIR)/fill.json
        #
        # Template definition for power grid analysis
        export TEMPLATE_PGA_CFG ?= $(PLATFORM_DIR)/template_pga.cfg
        
        # OpenRCX extRules
        export RCX_RULES = $(PLATFORM_DIR)/rcx_patterns.rules
        
        # ---------------------------------------------------------
        #  IR Drop
        # ---------------------------------------------------------
        
        # IR drop estimation supply net name to be analyzed and supply voltage variable
        # For multiple nets: PWR_NETS_VOLTAGES  = "VDD1 1.8 VDD2 1.2"
        export PWR_NETS_VOLTAGES  ?= VDD 1.8
        export GND_NETS_VOLTAGES  ?= VSS 0.0
        export IR_DROP_LAYER ?= met1
        
        # DRC Check
        export KLAYOUT_DRC_FILE = $(PLATFORM_DIR)/drc/$(PLATFORM).lydrc
        
        #LVS Check
        export CDL_FILE = $(PLATFORM_DIR)/cdl/$(PLATFORM).cdl
        export KLAYOUT_LVS_FILE = $(PLATFORM_DIR)/lvs/$(PLATFORM).lylvs
#############################################################################
# ⬆️ End of inline config.mk                                            ⬆️ #
#############################################################################

    # __SPACE__ is a workaround for whitespace hell in "foreach"; there
    # is no way to escape space in defaults.py and get "foreach" to work.
    $(foreach line,$(shell $(SCRIPTS_DIR)/defaults.py),$(eval export $(subst __SPACE__, ,$(line))))
#############################################################################
# ⬇️ Inline content from `defaults.py` (for analysis purpose only)      ⬇️ #
#############################################################################
        #!/usr/bin/env python3
        
        import os
        import yaml
        
        dir_path = os.path.dirname(os.path.realpath(__file__))
        
        yaml_path = os.path.join(dir_path, "variables.yaml")
        with open(yaml_path, "r") as file:
            data = yaml.safe_load(file)
#############################################################################
# ⬇️ Inline content from `variables.yaml` (for analysis purpose only)   ⬇️ #
#############################################################################
================================== My Note ==================================
=    "TNS_END_PERCENT": {                                                   =
=        "description": "...",                                              =
=        "default": 100,                                                    =
=        "stages": ["cts", "floorplan", "grt"]                              =
=    }                                                                      =
=============================================================================
            ---
            GENERATE_ARTIFACTS_ON_FAILURE:
              description: >
                For instance Bazel needs artifacts (.odb and .rpt files) on a failure to
                allow the user to save hours on re-running the failed step locally, but when
                working with a Makefile flow, it is more natural to fail the step and leave
                the user to manually inspect the logs and artifacts directly via the file
                system.
                Set to 1 to change the behavior to generate artifacts upon failure to e.g.
                do a global route. The exit code will still be non-zero on all other
                failures that aren't covered by the "useful to inspect the artifacts on
                failure" use-case.
                Example: just like detailed routing, a global route that fails with
                congestion, is not a build failure(as in exit code non-zero), it is a
                successful(as in zero exit code) global route that produce reports
                detailing the problem.
                Detailed route will not proceed, if there is global routing congestion
                This allows build systems, such as bazel, to create artifacts for global and
                detailed route, even if the operation had problems, without having know
                about the semantics between global and detailed route.
                Considering that global and detailed route can run for a long time and use a
                lot of memory, this allows inspecting results on a laptop for a build that
                ran on a server.
              default: 0
            TNS_END_PERCENT:
              description: >
                Default TNS_END_PERCENT value for post CTS timing repair. Try fixing all
                violating endpoints by default (reduce to 5% for runtime).
                Specifies how many percent of violating paths to fix [0-100]. Worst path
                will always be fixed.
              default: 100
              stages:
                - cts
                - floorplan
                - grt
            ROUTING_LAYER_ADJUSTMENT:
              default: 0.5
              description: >
                Adjusts routing layer capacities to manage congestion and
                improve detailed routing. High values ease detailed routing
                but risk excessive detours and long global routing times,
                while low values reduce global routing failure but can
                complicate detailed routing.
                The global routing running time normally reduces
                dramatically (entirely design specific, but going from hours to
                minutes has been observed) when the value is
                low (such as 0.10).
                Sometimes, global routing will succeed with lower values and
                fail with higher values. Exploring results with different
                values can help shed light on the problem. Start with
                a too low value, such as 0.10, and bisect
                to value that works by doing multiple global routing runs.
                As a last resort, `make global_route_issue` and using
                the tools/OpenROAD/etc/deltaDebug.py can be useful to debug
                global routing errors. If there is something specific that is
                impossible to route, such as a clock line over a macro, global
                routing will terminate with DRC errors routes that could
                have been routed were it not for the specific impossible routes.
                deltaDebug.py should weed out the possible routes and leave
                a minimal failing case that pinpoints the problem.
              stages:
                - place
                - grt
                - route
                - final
            RECOVER_POWER:
              description: >
                Specifies how many percent of paths with positive slacks can be slowed for
                power savings [0-100].
              default: 0
            SKIP_INCREMENTAL_REPAIR:
              default: 0
              description: >
                Skip incremental repair in global route.
              stages:
                - grt
            DETAILED_METRICS:
              description: >
                If set, then calls report_metrics prior to repair operations in the CTS
                and global route stages
              default: 0
              stages:
                - cts
                - grt
            EQUIVALENCE_CHECK:
              description: >
                Enable running equivalence checks to verify logical correctness of
                repair_timing.
              default: 0
              stages:
                - cts
            CORE_UTILIZATION:
              description: |
                The core utilization percentage (0-100).
              stages:
                - floorplan
              tunable: 1
            CORE_AREA:
              description: >
                The core area specified as a list of lower-left and upper-right corners in
                microns
                (X1 Y1 X2 Y2).
              stages:
                - floorplan
              tunable: 1
            REPORT_CLOCK_SKEW:
              description: >
                Report clock skew as part of reporting metrics, starting at CTS, before which
                there is no clock skew.
                This metric can be quite time-consuming, so it can be useful to disable.
              stages:
                - cts
                - grt
                - route
                - final
              default: 1
            SKIP_REPORT_METRICS:
              description: >
                If set to 1, then metrics, report_metrics does nothing. Useful to speed up
                builds.
              stages:
                - floorplan
                - place
                - cts
                - grt
                - route
                - final
            PROCESS:
              description: |
                Technology node or process in use.
            CORNER:
              description: >
                PVT corner library selection. Only available for ASAP7 and GF180 PDKs.
            TECH_LEF:
              description: >
                A technology LEF file of the PDK that includes all relevant information
                regarding metal layers, vias, and spacing requirements.
            SC_LEF:
              description: |
                Path to technology standard cell LEF file.
            GDS_FILES:
              description: |
                Path to platform GDS files.
            LIB_FILES:
              description: >
                A Liberty file of the standard cell library with PVT characterization,
                input and output characteristics, timing and power definitions for each
                cell.
            DONT_USE_CELLS:
              description: |
                Dont use cells eases pin access in detailed routing.
            SYNTH_GUT:
              description: >
                Load design and remove all internal logic before doing synthesis. This is
                useful when creating a mock .lef abstract that has a smaller area than the
                amount of logic would allow. bazel-orfs uses this to mock SRAMs, for
                instance.
              stages:
                - synth
            SYNTH_HIERARCHICAL:
              description: |
                Enable to Synthesis hierarchically, otherwise considered flat synthesis.
              stages:
                - synth
              default: 0
            SYNTH_MEMORY_MAX_BITS:
              description: >
                Maximum number of bits for memory synthesis.
              default: 4096
              stages:
                - synth
            SYNTH_BLACKBOXES:
              description: >
                List of cells treated as a black box by Yosys. With Bazel, this can be used
                to run synthesis in parallel for the large modules of the design.
              stages:
                - synth
            SYNTH_NETLIST_FILES:
              description: >
                Skips synthesis and uses the supplied netlist files. If the netlist files
                contains duplicate modules, which can happen when using hierarchical
                synthesis on indvidual netlist files and combining here,
                subsequent modules are silently ignored and only the first module is used.
              stages:
                - synth
            LATCH_MAP_FILE:
              description: |
                List of latches treated as a black box by Yosys.
              stages:
                - synth
            CLKGATE_MAP_FILE:
              description: |
                List of cells for gating clock treated as a black box by Yosys.
              stages:
                - synth
            ADDER_MAP_FILE:
              description: |
                List of adders treated as a black box by Yosys.
              stages:
                - synth
            TIEHI_CELL_AND_PORT:
              description: >
                Tie high cells used in Yosys synthesis to replace a logical 1 in the
                Netlist.
              stages:
                - synth
                - place
            TIELO_CELL_AND_PORT:
              description: |
                Tie low cells used in Yosys synthesis to replace a logical 0 in the Netlist.
              stages:
                - synth
                - place
            MIN_BUF_CELL_AND_PORTS:
              description: |
                Used to insert a buffer cell to pass through wires. Used in synthesis.
              stages:
                - synth
            ABC_CLOCK_PERIOD_IN_PS:
              description: >
                Clock period to be used by STA during synthesis. Default value read from
                `constraint.sdc`.
              stages:
                - synth
            ABC_DRIVER_CELL:
              description: |
                Default driver cell used during ABC synthesis.
              stages:
                - synth
            ABC_LOAD_IN_FF:
              description: |
                During synthesis set_load value used.
              stages:
                - synth
            SYNTH_MINIMUM_KEEP_SIZE:
              description: >
                For hierarchical synthesis, we keep modules of larger area than given by
                this variable and flatten smaller modules.
                The area unit used is the size of a basic nand2 gate from the
                platform's standard cell library. The default value is platform specific.
              stages:
                - synth
              default: 0
            SYNTH_WRAPPED_OPERATORS:
              description: >
                Synthesize multiple architectural options for each arithmetic operator in the
                design. These options are available for switching among in later stages of
                the flow.
              stages:
                - synth
            FLOORPLAN_DEF:
              description: |
                Use the DEF file to initialize floorplan.
              stages:
                - floorplan
                - place
            REMOVE_ABC_BUFFERS:
              description: >
                Remove abc buffers from the netlist. If timing repair in floorplanning is
                taking too long, use a SETUP/HOLD_SLACK_MARGIN to terminate timing repair early
                instead of using REMOVE_ABC_BUFFERS or set SKIP_LAST_GASP=1.
              stages:
                - floorplan
              deprecated: 1
            PLACE_SITE:
              description: |
                Placement site for core cells defined in the technology LEF file.
              stages:
                - floorplan
            TAPCELL_TCL:
              description: |
                Path to Endcap and Welltie cells file.
              stages:
                - floorplan
            MACRO_PLACEMENT:
              description: >
                Specifies the path of a file on how to place certain macros manually using
                read_macro_placement.
              stages:
                - floorplan
            MACRO_PLACEMENT_TCL:
              description: |
                Specifies the path of a TCL file on how to place certain macros manually.
              stages:
                - floorplan
            MACRO_PLACE_HALO:
              description: >
                Horizontal/vertical halo around macros (microns). Used by automatic macro
                placement.
              stages:
                - floorplan
            MACRO_BLOCKAGE_HALO:
              description: >
                Distance beyond the edges of a macro that will also be covered by the
                blockage generated for that macro.
                Note that the default macro blockage halo comes from the largest of the
                specified MACRO_PLACE_HALO x or y values. This variable overrides that
                calculation.
              stages:
                - floorplan
            PDN_TCL:
              description: >
                File path which has a set of power grid policies used by pdn to be applied
                to the design, such as layers to use, stripe width and spacing to generate
                the actual metal straps.
              stages:
                - floorplan
            MAKE_TRACKS:
              description: |
                Tcl file that defines add routing tracks to a floorplan.
              stages:
                - floorplan
            IO_CONSTRAINTS:
              description: |
                File path to the IO constraints .tcl file.
              stages:
                - floorplan
                - place
            IO_PLACER_H:
              description: >
                The metal layer on which to place the I/O pins horizontally (top and bottom
                of the die).
              stages:
                - place
            IO_PLACER_V:
              description: >
                The metal layer on which to place the I/O pins vertically (sides of the
                die).
              stages:
                - place
            GUI_TIMING:
              description: >
                Load timing information when opening GUI. For large designs, this can be
                quite time consuming. Useful to disable when investigating non-timing
                aspects like floorplan, placement, routing, etc.
              default: 1
            FILL_CELLS:
              description: >
                Fill cells are used to fill empty sites. If not set or empty, fill cell
                insertion is skipped.
              stages:
                - route
            TAP_CELL_NAME:
              description: |
                Name of the cell to use in tap cell insertion.
            CELL_PAD_IN_SITES_GLOBAL_PLACEMENT:
              description: >
                Cell padding on both sides in site widths to ease routability during global
                placement.
              stages:
                - place
                - floorplan
              default: 0
              tunable: 1
            CELL_PAD_IN_SITES_DETAIL_PLACEMENT:
              description: >
                Cell padding on both sides in site widths to ease routability in detail
                placement.
              stages:
                - place
                - cts
                - grt
              default: 0
              tunable: 1
            PLACE_PINS_ARGS:
              description: |
                Arguments to place_pins
              stages:
                - place
              default: ""
            PLACE_DENSITY:
              description: >
                The desired placement density of cells. It reflects how spread the cells
                would be on the core area. 1.0 = closely dense. 0.0 = widely spread.
              stages:
                - floorplan
                - place
            PLACE_DENSITY_LB_ADDON:
              description: >
                Check the lower boundary of the PLACE_DENSITY and add
                PLACE_DENSITY_LB_ADDON if it exists.
              stages:
                - floorplan
                - place
              tunable: 1
            REPAIR_PDN_VIA_LAYER:
              description: |
                Remove power grid vias which generate DRC violations after detailed routing.
            GLOBAL_PLACEMENT_ARGS:
              description: >
                Use additional tuning parameters during global placement other than default
                args defined in global_place.tcl.
              default: ""
            ENABLE_DPO:
              description: |
                Enable detail placement with improve_placement feature.
              default: 1
            DPO_MAX_DISPLACEMENT:
              description: |
                Specifies how far an instance can be moved when optimizing.
              default: 5 1
            GPL_TIMING_DRIVEN:
              description: |
                Specifies whether the placer should use timing driven placement.
              stages:
                - place
              default: 1
            GPL_ROUTABILITY_DRIVEN:
              description: |
                Specifies whether the placer should use routability driven placement.
              stages:
                - place
              default: 1
            CAP_MARGIN:
              description: >
                Specifies a capacitance margin when fixing max capacitance violations. This
                option allows you to overfix.
            SLEW_MARGIN:
              description: >
                Specifies a slew margin when fixing max slew violations. This option allows
                you to overfix.
            CTS_ARGS:
              description: |
                Override `clock_tree_synthesis` arguments.
              stages:
                - cts
            HOLD_SLACK_MARGIN:
              description: >
                Specifies a time margin for the slack when fixing hold violations.
                This option allows you to overfix or underfix (negative value, terminate
                retiming before 0 or positive slack).
                floorplan.tcl uses min of HOLD_SLACK_MARGIN and 0 (default hold slack margin).
                This avoids overrepair in floorplan for hold by default, but allows skipping
                hold repair using a negative HOLD_SLACK_MARGIN.
                Exiting timing repair early is useful in exploration where
                the .sdc has a fixed clock period at the design's target clock period and where
                HOLD/SETUP_SLACK_MARGIN is used to avoid overrepair (extremely long running
                times) when exploring different parameter settings.
                When an ideal clock is used, that is before CTS,
                a clock insertion delay of 0 is used in timing paths. This creates
                a mismatch between macros that have a .lib file from after CTS, when
                the clock is propagated. To mitigate this, OpenSTA will use subtract
                the clock insertion delay of macros when calculating timing with ideal
                clock. Provided that min_clock_tree_path
                and max_clock_tree_path are in the .lib file, which is the case for
                macros built with OpenROAD. This is less accurate than if OpenROAD had
                created a placeholder clock tree for timing estimation purposes
                prior to CTS.
                There will inevitably be inaccuracies in the timing calculation prior
                to CTS. Use a slack margin that is low enough, even negative, to
                avoid overrepair. Inaccuracies in the timing prior to CTS can also
                lead to underrepair, but there no obvious and simple way to avoid
                underrapir in these cases.
                Overrepair can lead to excessive runtimes in repair or too much buffering
                being added, which can present itself as congestion of hold cells or
                buffer cells.
                Another use of SETUP/HOLD_SLACK_MARGIN is design parameter exploration
                when trying to find the minimum clock period for a design.
                The SDC_FILE for a design can be quite complicated and instead of
                modifying the clock period in the SDC_FILE, which can be non-trivial,
                the clock period can be fixed at the target frequency and the
                SETUP/HOLD_SLACK_MARGIN can be swept to find a plausible
                current minimum clock period.
              stages:
                - cts
                - floorplan
                - grt
              default: 0
            SETUP_SLACK_MARGIN:
              description: |
                Specifies a time margin for the slack when fixing setup violations.
                This option allows you to overfix or underfix(negative value, terminate
                retiming before 0 or positive slack).
                See HOLD_SLACK_MARGIN for more details.
              stages:
                - cts
                - floorplan
                - grt
              default: 0
            SKIP_GATE_CLONING:
              description: >
                Do not use gate cloning transform to fix timing violations (default: use
                gate cloning).
              stages:
                - cts
                - floorplan
                - grt
            SKIP_LAST_GASP:
              description: >
                Do not use last gasp optimization to fix timing violations (default: use
                gate last gasp).
              stages:
                - cts
                - floorplan
                - grt
            SKIP_PIN_SWAP:
              description: >
                Do not use pin swapping as a transform to fix timing violations (default:
                use pin swapping).
              stages:
                - cts
                - floorplan
                - grt
            REMOVE_CELLS_FOR_EQY:
              description: >
                String patterns directly passed to write_verilog -remove_cells <> for
                equivalence checks.
              stages:
                - cts
            SKIP_CTS_REPAIR_TIMING:
              description: >
                Skipping CTS repair, which can take a long time, can be useful in
                architectural exploration or when getting CI up and running.
              stages:
                - cts
            MIN_ROUTING_LAYER:
              description: |
                The lowest metal layer name to be used in routing.
              stages:
                - place
                - grt
                - route
                - final
            MAX_ROUTING_LAYER:
              description: |
                The highest metal layer name to be used in routing.
              stages:
                - place
                - grt
                - route
                - final
            DETAILED_ROUTE_ARGS:
              description: |
                Add additional arguments for debugging purposes during detail route.
              stages:
                - route
            MACRO_EXTENSION:
              description: |
                Sets the number of GCells added to the blockages boundaries from macros.
            DETAILED_ROUTE_END_ITERATION:
              description: >
                Maximum number of iterations.
              default: 64
              stages:
                - route
            RCX_RULES:
              description: |
                RC Extraction rules file path.
            SET_RC_TCL:
              description: |
                Metal & Via RC definition file path.
            FILL_CONFIG:
              description: |
                JSON rule file for metal fill during chip finishing.
            KLAYOUT_TECH_FILE:
              description: |
                A mapping from LEF/DEF to GDS using the KLayout tool.
            IR_DROP_LAYER:
              description: |
                Default metal layer to report IR drop.
            PLATFORM:
              required: true
              description: |
                Specifies process design kit or technology node to be used.
            DESIGN_NAME:
              required: true
              description: |
                The name of the top-level module of the design.
            VERILOG_FILES:
              required: true
              description: >
                The path to the design Verilog files or JSON files providing a description
                of modules (check `yosys -h write_json` for more details).
              stages:
                - synth
            SDC_FILE:
              required: true
              description: |
                The path to design constraint (SDC) file.
              stages:
                - synth
            SDC_GUT:
              description: >
                Load design and remove all internal logic before doing synthesis. This is
                useful when creating a mock .lef abstract that has a smaller area than the
                amount of logic would allow. bazel-orfs uses this to mock SRAMs, for
                instance.
              stages:
                - synth
            ADDITIONAL_FILES:
              description: |
                Additional files to be added to `make issue` archive.
            ADDITIONAL_LEFS:
              description: >
                Hardened macro LEF view files listed here. The LEF information of the
                macros is immutable and used throughout all stages. Stored in the .odb file.
            ADDITIONAL_LIBS:
              description: >
                Hardened macro library files listed here. The library information is
                immutable and used throughout all stages. Not stored in the .odb file.
            ADDITIONAL_GDS:
              description: |
                Hardened macro GDS files listed here.
              stages:
                - final
            VERILOG_INCLUDE_DIRS:
              description: |
                Specifies the include directories for the Verilog input files.
              stages:
                - synth
            DESIGN_NICKNAME:
              description: >
                DESIGN_NICKNAME just changes the directory name that ORFS outputs to be
                DESIGN_NICKNAME instead of DESIGN_NAME in case DESIGN_NAME is unwieldy or
                conflicts with a different design.
            ABC_AREA:
              description: |
                Strategies for Yosys ABC synthesis: Area/Speed. Default ABC_SPEED.
              stages:
                - synth
              default: 0
            PWR_NETS_VOLTAGES:
              description: |
                Used for IR Drop calculation.
              stages:
                - final
            GND_NETS_VOLTAGES:
              description: |
                Used for IR Drop calculation.
              stages:
                - final
            BLOCKS:
              description: >
                Blocks used as hard macros in a hierarchical flow. Do note that you have to
                specify block-specific inputs file in the directory mentioned by Makefile.
            CDL_FILES:
              description: |
                Insert additional Circuit Description Language (`.cdl`) netlist files.
            DFF_LIB_FILES:
              description: |
                Technology mapping liberty files for flip-flops.
            DONT_USE_LIBS:
              description: |
                Set liberty files as `dont_use`.
            SYNTH_KEEP_MODULES:
              description: |
                Mark modules to keep from getting removed in flattening.
              stages:
                - synth
            SYNTH_ARGS:
              description: |
                Optional synthesis variables for yosys.
              default: -flatten
            VERILOG_TOP_PARAMS:
              description: |
                Apply toplevel params (if exist).
              stages:
                - synth
              default: ""
            CORE_ASPECT_RATIO:
              description: >
                The core aspect ratio (height / width). This value is ignored if
                `CORE_UTILIZATION` is undefined.
              stages:
                - floorplan
              tunable: 1
            CORE_MARGIN:
              description: >
                The margin between the core area and die area, specified in microns.
                Allowed values are either one value for all margins or a set of four
                values, one for each margin. The order of the four values are:
                `{bottom top left right}`. This variable is ignored if `CORE_UTILIZATION`
                is undefined.
              stages:
                - floorplan
              tunable: 1
            DIE_AREA:
              description: >
                The die area specified as a list of lower-left and upper-right corners in
                microns
                (X1 Y1 X2 Y2).
              stages:
                - floorplan
              tunable: 1
            RESYNTH_AREA_RECOVER:
              description: |
                Enable re-synthesis for area reclaim.
              stages:
                - floorplan
              default: 0
            RESYNTH_TIMING_RECOVER:
              description: |
                Enable re-synthesis for timing optimization.
              stages:
                - floorplan
              default: 0
            MACRO_ROWS_HALO_X:
              description: >
                Horizontal distance between the edge of the macro and the beginning of the
                rows created by tapcell. Only available for ASAP7 PDK and GF180/uart-blocks
                design.
              stages:
                - floorplan
            MACRO_ROWS_HALO_Y:
              description: >
                Vertical distance between the edge of the macro and the beginning of the
                rows created by tapcell. Only available for ASAP7 PDK and GF180/uart-blocks
                design.
              stages:
                - floorplan
            MACRO_WRAPPERS:
              description: |
                The wrapper file that replaces existing macros with their wrapped version.
              stages:
                - floorplan
            CTS_BUF_DISTANCE:
              description: |
                Distance (in microns) between buffers.
              stages:
                - cts
            CTS_CLUSTER_DIAMETER:
              description: >
                Maximum diameter (in microns) of sink cluster.
              default: 20
              stages:
                - cts
              tunable: 1
            CTS_CLUSTER_SIZE:
              description: >
                Maximum number of sinks per cluster.
              default: 50
              stages:
                - cts
              tunable: 1
            CTS_SNAPSHOT:
              description: |
                Creates ODB/SDC files prior to clock net and setup/hold repair.
              stages:
                - cts
            POST_CTS_TCL:
              description: |
                Specifies a Tcl script with commands to run after CTS is completed.
              stages:
                - cts
            FASTROUTE_TCL:
              description: |
                Specifies a Tcl script with commands to run before FastRoute.
            USE_FILL:
              description: >
                Whether to perform metal density filling.
              default: 0
            SEAL_GDS:
              description: |
                Seal macro to place around the design.
            ABSTRACT_SOURCE:
              description: |
                Which .odb file to use to create abstract
              stages:
                - generate_abstract
            GLOBAL_ROUTE_ARGS:
              description: >
                Replaces default arguments for global route.
              stages:
                - grt
              default: -congestion_iterations 30 -congestion_report_iter_step 5 -verbose
            MATCH_CELL_FOOTPRINT:
              description: >
                Enforce sizing operations to only swap cells that have the same layout
                boundary.
              stages:
                - floorplan
                - place
                - cts
                - route
              default: 0
            RTLMP_MAX_LEVEL:
              description: >
                Maximum depth of the physical hierarchy tree.
              default: 2
              stages:
                - floorplan
            RTLMP_MAX_INST:
              description: >
                Maximum number of standard cells in a cluster. If unset, rtl_macro_placer
                will calculate a value based on the design attributes.
              stages:
                - floorplan
            RTLMP_MIN_INST:
              description: >
                Minimum number of standard cells in a cluster. If unset, rtl_macro_placer
                will calculate a value based on the design attributes.
              stages:
                - floorplan
            RTLMP_MAX_MACRO:
              description: >
                Maximum number of macros in a cluster. If unset, rtl_macro_placer will
                calculate a value based on the design attributes.
              stages:
                - floorplan
            RTLMP_MIN_MACRO:
              description: >
                Minimum number of macros in a cluster. If unset, rtl_macro_placer will
                calculate a value based on the design attributes.
              stages:
                - floorplan
            RTLMP_MIN_AR:
              description: >
                Specifies the minimum aspect ratio (height/width).
              default: 0.33
              stages:
                - floorplan
            RTLMP_SIGNATURE_NET_THRESHOLD:
              description: >
                Minimum number of connections between two clusters to be identified as
                connected.
              default: 50
              stages:
                - floorplan
            RTLMP_AREA_WT:
              description: >
                Weight for the area of the current floorplan.
              default: 0.1
              stages:
                - floorplan
            RTLMP_WIRELENGTH_WT:
              description: >
                Weight for half-perimiter wirelength.
              default: 100.0
              stages:
                - floorplan
            RTLMP_OUTLINE_WT:
              description: >
                Weight for violating the fixed outline constraint, meaning that all
                clusters should be placed within the shape of their parent cluster.
              default: 100.00
              stages:
                - floorplan
            RTLMP_BOUNDARY_WT:
              description: >
                Weight for the boundary or how far the hard macro clusters are from
                boundaries.
              default: 50.0
              stages:
                - floorplan
            RTLMP_NOTCH_WT:
              description: >
                Weight for the notch, or the existence of dead space that cannot be used
                for placement and routing.
              default: 10.0
              stages:
                - floorplan
            RTLMP_DEAD_SPACE:
              description: >
                Specifies the target dead space percentage, which influences the
                utilization of a cluster.
              default: 0.05
              stages:
                - floorplan
            RTLMP_RPT_DIR:
              description: >
                Path to the directory where reports are saved.
              stages:
                - floorplan
            RTLMP_FENCE_LX:
              description: >
                Defines the lower left X coordinate for the global fence bounding box in
                microns.
              default: 0.0
              stages:
                - floorplan
            RTLMP_FENCE_LY:
              description: >
                Defines the lower left Y coordinate for the global fence bounding box in
                microns.
              default: 0.0
              stages:
                - floorplan
            RTLMP_FENCE_UX:
              description: >
                Defines the upper right X coordinate for the global fence bounding box in
                microns.
              default: 100000000.0
              stages:
                - floorplan
            RTLMP_FENCE_UY:
              description: >
                Defines the upper right Y coordinate for the global fence bounding box in
                microns.
              default: 100000000.0
              stages:
                - floorplan
            RTLMP_ARGS:
              description: >
                Overrides all other RTL macro placer arguments.
              stages:
                - floorplan
            GDS_ALLOW_EMPTY:
              description: >
                Regular expression of module names of macros that have no .gds file
              stages:
                - final
            RUN_SCRIPT:
              description: >
                Path to script to run from `make run`, python or tcl script detected by
                .py or .tcl extension.
            RUN_LOG_NAME_STEM:
              description: >
                Stem of the log file name, the log file will be named
                `$(LOG_DIR)/$(RUN_LOG_NAME_STEM).log`.
              default: run
            YOSYS_FLAGS:
              description: >
                Flags to pass to yosys.
              stages:
                - synth
              default: -v 3
            FLOW_VARIANT:
              description: >
                Flow variant to use, used in the flow variant directory name.
              default: base
#############################################################################
# ⬆️ End of inline variables.yaml                                       ⬆️ #
#############################################################################

================================== My Note ==================================
=    Skip if the "default" key is missing in the value dictionary.          =
=    Print an export statement, replacing spaces in the default value.      =
=============================================================================
        for key, value in data.items():
            if value.get("default", None) is None:
                continue
            print(f'export {key}?={str(value["default"]).replace(" ", "__SPACE__")}')
#############################################################################
# ⬆️ End of inline defaults.py                                          ⬆️ #
#############################################################################

    export LOG_DIR     = $(WORK_HOME)/logs/$(PLATFORM)/$(DESIGN_NICKNAME)/$(FLOW_VARIANT)
    export OBJECTS_DIR = $(WORK_HOME)/objects/$(PLATFORM)/$(DESIGN_NICKNAME)/$(FLOW_VARIANT)
    export REPORTS_DIR = $(WORK_HOME)/reports/$(PLATFORM)/$(DESIGN_NICKNAME)/$(FLOW_VARIANT)
    export RESULTS_DIR = $(WORK_HOME)/results/$(PLATFORM)/$(DESIGN_NICKNAME)/$(FLOW_VARIANT)
    
    #-------------------------------------------------------------------------------
    ifeq (,$(strip $(NUM_CORES)))
      # Linux (utility program)
      NUM_CORES := $(shell nproc 2>/dev/null)
    
      ifeq (,$(strip $(NUM_CORES)))
        # Linux (generic)
        NUM_CORES := $(shell grep -c ^processor /proc/cpuinfo 2>/dev/null)
      endif
      ifeq (,$(strip $(NUM_CORES)))
        # BSD (at least FreeBSD and Mac OSX)
        NUM_CORES := $(shell sysctl -n hw.ncpu 2>/dev/null)
      endif
      ifeq (,$(strip $(NUM_CORES)))
        # Fallback
        NUM_CORES := 1
      endif
    endif
    export NUM_CORES
    
    #-------------------------------------------------------------------------------
    # setup all commands used within this flow
    export TIME_BIN   ?= env time
    TIME_CMD = $(TIME_BIN) -f 'Elapsed time: %E[h:]min:sec. CPU time: user %U sys %S (%P). Peak memory: %MKB.'
    TIME_TEST = $(shell $(TIME_CMD) echo foo 2>/dev/null)
    ifeq (,$(strip $(TIME_TEST)))
      TIME_CMD = $(TIME_BIN)
    endif
    export TIME_CMD
    
    # The following determine the executable location for each tool used by this flow.
    # Priority is given to
    #       1 user explicit set with variable in Makefile or command line, for instance setting OPENROAD_EXE
    #       2 ORFS compiled tools: openroad, yosys
    ifneq (${IN_NIX_SHELL},)
      export OPENROAD_EXE := $(shell command -v openroad)
    else
      export OPENROAD_EXE ?= $(abspath $(FLOW_HOME)/../tools/install/OpenROAD/bin/openroad)
    endif
    ifneq (${IN_NIX_SHELL},)
      export OPENSTA_EXE := $(shell command -v sta)
    else
      export OPENSTA_EXE ?= $(abspath $(FLOW_HOME)/../tools/install/OpenROAD/bin/sta)
    endif
    
    export OPENROAD_ARGS = -no_init -threads $(NUM_CORES) $(OR_ARGS)
    export OPENROAD_CMD = $(OPENROAD_EXE) -exit $(OPENROAD_ARGS)
    export OPENROAD_NO_EXIT_CMD = $(OPENROAD_EXE) $(OPENROAD_ARGS)
    export OPENROAD_GUI_CMD = $(OPENROAD_EXE) -gui $(OR_ARGS)
    
    ifneq (${IN_NIX_SHELL},)
      YOSYS_EXE := $(shell command -v yosys)
    else
      YOSYS_EXE ?= $(abspath $(FLOW_HOME)/../tools/install/yosys/bin/yosys)
    endif
    export YOSYS_EXE
    
    # Use locally installed and built klayout if it exists, otherwise use klayout in path
    KLAYOUT_DIR = $(abspath $(FLOW_HOME)/../tools/install/klayout/)
    KLAYOUT_BIN_FROM_DIR = $(KLAYOUT_DIR)/klayout
    
    ifeq ($(wildcard $(KLAYOUT_BIN_FROM_DIR)), $(KLAYOUT_BIN_FROM_DIR))
    KLAYOUT_CMD ?= sh -c 'LD_LIBRARY_PATH=$(dir $(KLAYOUT_BIN_FROM_DIR)) $$0 "$$@"' $(KLAYOUT_BIN_FROM_DIR)
    else
    ifeq ($(KLAYOUT_CMD),)
    KLAYOUT_CMD := $(shell command -v klayout)
    endif
    endif
    KLAYOUT_FOUND            = $(if $(KLAYOUT_CMD),,$(error KLayout not found in PATH))
    
    ifneq ($(shell command -v stdbuf),)
      STDBUF_CMD ?= stdbuf -o L
    endif
    
    #-------------------------------------------------------------------------------
    WRAPPED_LEFS = $(foreach lef,$(notdir $(WRAP_LEFS)),$(OBJECTS_DIR)/lef/$(lef:.lef=_mod.lef))
    WRAPPED_LIBS = $(foreach lib,$(notdir $(WRAP_LIBS)),$(OBJECTS_DIR)/$(lib:.lib=_mod.lib))
    export ADDITIONAL_LEFS += $(WRAPPED_LEFS) $(WRAP_LEFS)
    export LIB_FILES += $(WRAP_LIBS) $(WRAPPED_LIBS)

================================== My Note ==================================
=    Extract filenames from LIB_FILES (remove directories).                 =
=    Prepend path prefix OBJECTS_DIR/lib/ to each filename.                 =
=    Replace file extension from .lib.gz to .lib.                           =
=    Final list represents libraries to exclude from usage.                 =
=============================================================================
    export DONT_USE_LIBS   = $(patsubst %.lib.gz, %.lib, $(addprefix $(OBJECTS_DIR)/lib/, $(notdir $(LIB_FILES))))
    export DONT_USE_SC_LIB ?= $(firstword $(DONT_USE_LIBS))
    
    # Stream system used for final result (GDS is default): GDS, GSDII, GDS2, OASIS, or OAS
    STREAM_SYSTEM ?= GDS
    ifneq ($(findstring GDS,$(shell echo $(STREAM_SYSTEM) | tr '[:lower:]' '[:upper:]')),)
            export STREAM_SYSTEM_EXT := gds
            GDSOAS_FILES = $(GDS_FILES)
            ADDITIONAL_GDSOAS = $(ADDITIONAL_GDS)
            SEAL_GDSOAS = $(SEAL_GDS)
    else
            export STREAM_SYSTEM_EXT := oas
            GDSOAS_FILES = $(OAS_FILES)
            ADDITIONAL_GDSOAS = $(ADDITIONAL_OAS)
            SEAL_GDSOAS = $(SEAL_OAS)
    endif
    export WRAPPED_GDSOAS = $(foreach lef,$(notdir $(WRAP_LEFS)),$(OBJECTS_DIR)/$(lef:.lef=_mod.$(STREAM_SYSTEM_EXT)))
    
    # If we are running headless use offscreen rendering for save_image
    ifeq ($(DISPLAY),)
    export QT_QPA_PLATFORM ?= offscreen
    endif
    
    # Create Macro wrappers (if necessary)
    export WRAP_CFG = $(PLATFORM_DIR)/wrapper.cfg
    
    export TCLLIBPATH := util/cell-veneer $(TCLLIBPATH)
    
    export SYNTH_SCRIPT ?= $(SCRIPTS_DIR)/synth.tcl
    export SDC_FILE_CLOCK_PERIOD = $(RESULTS_DIR)/clock_period.txt
    
    export YOSYS_DEPENDENCIES=$(DONT_USE_LIBS) $(WRAPPED_LIBS) $(DFF_LIB_FILE) $(VERILOG_FILES) $(SYNTH_NETLIST_FILES) $(LATCH_MAP_FILE) $(ADDER_MAP_FILE) $(SDC_FILE_CLOCK_PERIOD)
    
    # Ubuntu 22.04 ships with older than 0.28.11, so support older versions
    # for a while still.
    export KLAYOUT_ENV_VAR_IN_PATH_VERSION = 0.28.11
    export KLAYOUT_VERSION := $(if $(KLAYOUT_CMD),$(shell $(KLAYOUT_CMD) -v 2>/dev/null | grep 'KLayout' | cut -d ' ' -f2),)
    
    export KLAYOUT_ENV_VAR_IN_PATH = $(shell \
            if [ -z "$(KLAYOUT_VERSION)" ]; then \
                    echo "not_found"; \
            elif [ "$$(echo -e "$(KLAYOUT_VERSION)\n$(KLAYOUT_ENV_VAR_IN_PATH_VERSION)" | sort -V | head -n1)" = "$(KLAYOUT_VERSION)" ] && [ "$(KLAYOUT_VERSION)" != "$(KLAYOUT_ENV_VAR_IN_PATH_VERSION)" ]; then \
                    echo "invalid"; \
            else \
                    echo "valid"; \
            fi)
    
    export GDS_FINAL_FILE = $(RESULTS_DIR)/6_final.$(STREAM_SYSTEM_EXT)
    export RESULTS_ODB = $(notdir $(sort $(wildcard $(RESULTS_DIR)/*.odb)))
    export RESULTS_DEF = $(notdir $(sort $(wildcard $(RESULTS_DIR)/*.def)))
    export RESULTS_GDS = $(notdir $(sort $(wildcard $(RESULTS_DIR)/*.gds)))
    export RESULTS_OAS = $(notdir $(sort $(wildcard $(RESULTS_DIR)/*.oas)))
    export GDS_MERGED_FILE = $(RESULTS_DIR)/6_1_merged.$(STREAM_SYSTEM_EXT)
    
    define get_variables
    $(foreach V, $(.VARIABLES),$(if $(filter-out $(1), $(origin $V)), $(if $(filter-out .% %QT_QPA_PLATFORM% %TIME_CMD% KLAYOUT% GENERATE_ABSTRACT_RULE% do-step% do-copy% OPEN_GUI% OPEN_GUI_SHORTCUT% SUB_MAKE% UNSET_VARS% export%, $(V)), $V$ )))
    endef
    
    export UNSET_VARIABLES_NAMES := $(call get_variables,command% line environment% default automatic)
    export ISSUE_VARIABLES_NAMES := $(sort $(filter-out \n get_variables, $(call get_variables,environment% default automatic)))
    # This is Makefile's way to define a macro that expands to a single newline.
    define newline
    
    
    endef
    export ISSUE_VARIABLES := $(foreach V, $(ISSUE_VARIABLES_NAMES), $(if $($V),$V=$($V),$V='')$(newline))
    export COMMAND_LINE_ARGS := $(foreach V,$(.VARIABLES),$(if $(filter command% line, $(origin $V)),$(V)))
    
    # Set yosys-abc clock period to first "clk_period" value or "-period" value found in sdc file
    ifeq ($(origin ABC_CLOCK_PERIOD_IN_PS), undefined)
       ifneq ($(wildcard $(SDC_FILE)),)
          export ABC_CLOCK_PERIOD_IN_PS := $(shell sed -nE "s/^set\s+clk_period\s+(\S+).*|.*-period\s+(\S+).*/\1\2/p" $(SDC_FILE) | head -1 | awk '{print $$1}')
       endif
    endif
    
    .PHONY: vars
    vars:
            mkdir -p $(OBJECTS_DIR)
            $(UTILS_DIR)/generate-vars.sh $(OBJECTS_DIR)/vars
    
    .PHONY: print-%
    # Print any variable, for instance: make print-DIE_AREA
    print-%  : ; @echo "$* = $($*)"
#############################################################################
# ⬆️ End of inline variables.mk                                         ⬆️ #
#############################################################################

define GENERATE_ABSTRACT_RULE
ifeq ($(wildcard $(3)),)
# There is no unique config.mk for this module, use the shared
# block.mk that, by convention, is in the same folder as config.mk
# of the parent macro.
#
# At an early stage, before refining each of the macros, a shared
# block.mk file can be useful to run through the flow to explore
# more global concerns instead of getting mired in the details of
# each macro.
block := $(patsubst ./designs/$(PLATFORM)/$(DESIGN_NICKNAME)/%,%,$(dir $(3)))
$(1) $(2) &:
        $$(UNSET_AND_MAKE) DESIGN_NAME=${block} DESIGN_NICKNAME=$$(DESIGN_NICKNAME)_${block} DESIGN_CONFIG=$$(shell dirname $$(DESIGN_CONFIG))/block.mk generate_abstract
else
# There is a unique config.mk for this Verilog module
$(1) $(2) &:
        $$(UNSET_AND_MAKE) DESIGN_CONFIG=$(3) generate_abstract
endif
endef

# Targets to harden Blocks in case of hierarchical flow is triggered
.PHONY: build_macros
build_macros: $(BLOCK_LEFS) $(BLOCK_LIBS)

$(foreach block,$(BLOCKS),$(eval $(call GENERATE_ABSTRACT_RULE,./results/$(PLATFORM)/$(DESIGN_NICKNAME)_$(block)/$(FLOW_VARIANT)/${block}.lef,./results/$(PLATFORM)/$(DESIGN_NICKNAME)_$(block)/$(FLOW_VARIANT)/${block}.lib,$(shell dirname $(DESIGN_CONFIG))/${block}/config.mk)))
$(foreach block,$(BLOCKS),$(eval ./results/$(PLATFORM)/$(DESIGN_NICKNAME)_$(block)/$(FLOW_VARIANT)/6_final.gds: ./results/$(PLATFORM)/$(DESIGN_NICKNAME)_$(block)/$(FLOW_VARIANT)/${block}.lef))

# Utility to print tool version information
#-------------------------------------------------------------------------------
.PHONY: versions.txt
versions.txt:
        mkdir -p $(OBJECTS_DIR)
        @if [ -z "$(YOSYS_EXE)" ]; then \
                echo >> $(OBJECTS_DIR)/$@ "yosys not installed"; \
        else \
                $(YOSYS_EXE) -V > $(OBJECTS_DIR)/$@; \
        fi
        @echo openroad `$(OPENROAD_EXE) -version` >> $(OBJECTS_DIR)/$@
        @if [ -z "$(KLAYOUT_CMD)" ]; then \
                echo >> $(OBJECTS_DIR)/$@ "klayout not installed"; \
        else \
                $(KLAYOUT_CMD) -zz -v >> $(OBJECTS_DIR)/$@; \
        fi

# Pre-process libraries
# ==============================================================================

# Create temporary Liberty files which have the proper dont_use properties set
# For use with Yosys and ABC
.SECONDEXPANSION:
$(DONT_USE_LIBS): $$(filter %$$(@F) %$$(@F).gz,$(LIB_FILES))
        @mkdir -p $(OBJECTS_DIR)/lib
        $(UTILS_DIR)/preprocessLib.py -i $^ -o $@

$(OBJECTS_DIR)/lib/merged.lib: $(DONT_USE_LIBS)
        $(UTILS_DIR)/mergeLib.pl $(PLATFORM)_merged $(DONT_USE_LIBS) > $@

# Pre-process KLayout tech
# ==============================================================================
$(OBJECTS_DIR)/klayout_tech.lef: $(TECH_LEF)
        $(UNSET_AND_MAKE) do-klayout_tech

.PHONY: do-klayout_tech
do-klayout_tech:
        @mkdir -p $(OBJECTS_DIR)
        cp $(TECH_LEF) $(OBJECTS_DIR)/klayout_tech.lef

$(OBJECTS_DIR)/klayout.lyt: $(KLAYOUT_TECH_FILE) $(OBJECTS_DIR)/klayout_tech.lef
        $(UNSET_AND_MAKE) do-klayout

.PHONY: do-klayout
do-klayout:
ifeq ($(KLAYOUT_ENV_VAR_IN_PATH),valid)
        SC_LEF_RELATIVE_PATH="$$\(env('FLOW_HOME')\)/$(shell realpath --relative-to=$(FLOW_HOME) $(SC_LEF))"; \
        OTHER_LEFS_RELATIVE_PATHS=$$(echo "$(foreach file, $(OBJECTS_DIR)/klayout_tech.lef $(ADDITIONAL_LEFS),<lef-files>$$(realpath --relative-to=$(RESULTS_DIR) $(file))</lef-files>)"); \
        sed 's,<lef-files>.*</lef-files>,<lef-files>'"$$SC_LEF_RELATIVE_PATH"'</lef-files>'"$$OTHER_LEFS_RELATIVE_PATHS"',g' $(KLAYOUT_TECH_FILE) > $(OBJECTS_DIR)/klayout.lyt
else
        sed 's,<lef-files>.*</lef-files>,$(foreach file, $(OBJECTS_DIR)/klayout_tech.lef $(SC_LEF) $(ADDITIONAL_LEFS),<lef-files>$(shell realpath --relative-to=$(RESULTS_DIR) $(file))</lef-files>),g' $(KLAYOUT_TECH_FILE) > $(OBJECTS_DIR)/klayout.lyt
endif
        sed -i 's,<map-file>.*</map-file>,$(foreach file, $(FLOW_HOME)/platforms/$(PLATFORM)/*map,<map-file>$(shell realpath $(file))</map-file>),g' $(OBJECTS_DIR)/klayout.lyt

$(OBJECTS_DIR)/klayout_wrap.lyt: $(KLAYOUT_TECH_FILE) $(OBJECTS_DIR)/klayout_tech.lef
        $(UNSET_AND_MAKE) do-klayout_wrap

.PHONY: do-klayout_wrap
do-klayout_wrap:
        sed 's,<lef-files>.*</lef-files>,$(foreach file, $(OBJECTS_DIR)/klayout_tech.lef $(WRAP_LEFS),<lef-files>$(shell realpath --relative-to=$(OBJECTS_DIR)/def $(file))</lef-files>),g' $(KLAYOUT_TECH_FILE) > $(OBJECTS_DIR)/klayout_wrap.lyt

$(WRAPPED_LEFS):
        mkdir -p $(OBJECTS_DIR)/lef $(OBJECTS_DIR)/def
        util/cell-veneer/wrap.tcl -cfg $(WRAP_CFG) -macro $(filter %$(notdir $(@:_mod.lef=.lef)),$(WRAP_LEFS))
        mv $(notdir $@) $@
        mv $(notdir $(@:lef=def)) $(dir $@)../def/$(notdir $(@:lef=def))

$(WRAPPED_LIBS):
        mkdir -p $(OBJECTS_DIR)/lib
        sed 's/library(\(.*\))/library(\1_mod)/g' $(filter %$(notdir $(@:_mod.lib=.lib)),$(WRAP_LIBS)) | sed 's/cell(\(.*\))/cell(\1_mod)/g' > $@

# ==============================================================================
#  ______   ___   _ _____ _   _ _____ ____ ___ ____
# / ___\ \ / / \ | |_   _| | | | ____/ ___|_ _/ ___|
# \___ \\ V /|  \| | | | | |_| |  _| \___ \| |\___ \
#  ___) || | | |\  | | | |  _  | |___ ___) | | ___) |
# |____/ |_| |_| \_| |_| |_| |_|_____|____/___|____/
#
.PHONY: synth
synth: $(RESULTS_DIR)/1_synth.v

.PHONY: synth-report
synth-report: synth
        $(UNSET_AND_MAKE) do-synth-report

.PHONY: do-synth-report
do-synth-report:
        ($(TIME_CMD) $(OPENROAD_CMD) $(SCRIPTS_DIR)/synth_metrics.tcl) 2>&1 | tee $(abspath $(LOG_DIR)/1_1_yosys_metrics.log)

.PHONY: memory
memory:
        if [ -f $(RESULTS_DIR)/mem_hierarchical.json ]; then \
                python3 $(SCRIPTS_DIR)/mem_dump.py $(RESULTS_DIR)/mem_hierarchical.json; \
        fi
        python3 $(SCRIPTS_DIR)/mem_dump.py $(RESULTS_DIR)/mem.json

# ==============================================================================


# Run Synthesis using yosys
#-------------------------------------------------------------------------------

$(SDC_FILE_CLOCK_PERIOD): $(SDC_FILE)
        mkdir -p $(dir $@)
        echo $(ABC_CLOCK_PERIOD_IN_PS) > $@

.PHONY: yosys-dependencies
yosys-dependencies: $(YOSYS_DEPENDENCIES)

.PHONY: do-yosys
do-yosys: $(DONT_USE_SC_LIB)
        $(SCRIPTS_DIR)/synth.sh $(SYNTH_SCRIPT) $(LOG_DIR)/1_1_yosys.log

.PHONY: do-yosys-canonicalize
do-yosys-canonicalize: yosys-dependencies $(DONT_USE_SC_LIB)
        $(SCRIPTS_DIR)/synth.sh $(SCRIPTS_DIR)/synth_canonicalize.tcl $(LOG_DIR)/1_1_yosys_canonicalize.log

$(RESULTS_DIR)/1_synth.rtlil: $(YOSYS_DEPENDENCIES)
        $(UNSET_AND_MAKE) do-yosys-canonicalize

$(RESULTS_DIR)/1_1_yosys.v: $(RESULTS_DIR)/1_synth.rtlil
        $(UNSET_AND_MAKE) do-yosys

.PHONY: do-synth
do-synth:
        mkdir -p $(RESULTS_DIR) $(LOG_DIR) $(REPORTS_DIR)
        cp $(RESULTS_DIR)/1_1_yosys.v $(RESULTS_DIR)/1_synth.v

$(RESULTS_DIR)/1_synth.v: $(RESULTS_DIR)/1_1_yosys.v
        $(UNSET_AND_MAKE) do-synth

.PHONY: clean_synth
clean_synth:
        rm -f $(RESULTS_DIR)/1_* $(RESULTS_DIR)/mem*.json
        rm -f $(REPORTS_DIR)/synth_*
        rm -f $(LOG_DIR)/1_*
        rm -f $(SYNTH_STATS)
        rm -f $(SDC_FILE_CLOCK_PERIOD)
        rm -rf _tmp_yosys-abc-*


# ==============================================================================
#  _____ _     ___   ___  ____  ____  _        _    _   _
# |  ___| |   / _ \ / _ \|  _ \|  _ \| |      / \  | \ | |
# | |_  | |  | | | | | | | |_) | |_) | |     / _ \ |  \| |
# |  _| | |__| |_| | |_| |  _ <|  __/| |___ / ___ \| |\  |
# |_|   |_____\___/ \___/|_| \_\_|   |_____/_/   \_\_| \_|
#
.PHONY: floorplan
floorplan: $(RESULTS_DIR)/2_floorplan.odb \
           $(RESULTS_DIR)/2_floorplan.sdc

# ==============================================================================

UNSET_VARS = for var in $(UNSET_VARIABLES_NAMES); do unset $$var; done

# FILE_MAKEFILE is needed when ORFS is invoked with
# `make --file=$FLOW_DIR/Makefile` or `make --directory $FLOW_DIR`.
#
# However, on some versions of make, MAKEFILE_LIST can be empty, so
# don't expand it in that case.
FILE_MAKEFILE ?= $(if $(firstword $(MAKEFILE_LIST)),--file=$(firstword $(MAKEFILE_LIST)),)
SUB_MAKE = $(MAKE) $(foreach V,$(COMMAND_LINE_ARGS), $(if $($V),$V=$(shell echo "$($V)" | $(FLOW_HOME)/scripts/escape.sh),$V='')) --no-print-directory $(FILE_MAKEFILE) DESIGN_CONFIG=$(DESIGN_CONFIG)
UNSET_AND_MAKE = @bash -c '$(UNSET_VARS); $(SUB_MAKE) $$@' --

$(OBJECTS_DIR)/copyright.txt:
        @$(OPENROAD_CMD) $(SCRIPTS_DIR)/noop.tcl
        mkdir -p $(OBJECTS_DIR)
        @touch $(OBJECTS_DIR)/copyright.txt

define OPEN_GUI_SHORTCUT
.PHONY: gui_$(1) open_$(1)
gui_$(1): gui_$(2)
open_$(1): open_$(2)
endef

define OPEN_GUI
.PHONY: open_$(1) gui_$(1)
open_$(1):
        $(2)=$(RESULTS_DIR)/$(1) $(OPENROAD_NO_EXIT_CMD) $(SCRIPTS_DIR)/open.tcl
gui_$(1):
        $(2)=$(RESULTS_DIR)/$(1) $(OPENROAD_GUI_CMD) $(SCRIPTS_DIR)/open.tcl
endef

# Separate dependency checking and doing a step. This can
# be useful to retest a stage without having to delete the
# target, or when building a wafer thin layer on top of
# ORFS using CMake, Ninja, Bazel, etc. where makefile
# dependency checking only gets in the way.
#
# Note that there is no "do-synth" step as it is a special
# first step that for usecases such as Bazel where it should
# always be built when invoked. Latter stages in the build process
# are conditionally built by the Bazel implementation.
#
# A "do-synth" step would be welcomed, but it isn't strictly necessary
# for the Bazel use-case.
#
# do-floorplan, do-place, do-cts, do-route, do-finish are the
# supported interface to execute those stages without checking
# for dependencies.
#
# The do- substeps of each of these stages are subject to change.
#
# $(1) stem, e.g. 2_1_floorplan
# $(2) dependencies
# $(3) tcl script step
# $(4) extension of result, default .odb
# $(5) folder of target, default $(RESULTS_DIR)
define do-step
$(if $(5),$(5),$(RESULTS_DIR))/$(1)$(if $(4),$(4),.odb): $(2)
        $$(UNSET_AND_MAKE) do-$(1)

ifeq ($(if $(4),$(4),.odb),.odb)
.PHONY: $(1)
$(1): $(RESULTS_DIR)/$(1).odb

$(eval $(call OPEN_GUI_SHORTCUT,$(1),$(1).odb))
endif

.PHONY: do-$(1)
do-$(1): $(OBJECTS_DIR)/copyright.txt
        $(SCRIPTS_DIR)/flow.sh $(1) $(3)
endef

# generate make rules to copy a file, if a dependency change and
# a do- sibling rule that copies the file unconditionally.
#
# The file is copied within the $(RESULTS_DIR)
#
# $(1) stem of target, e.g. 2_1_floorplan
# $(2) basename of file to be copied
# $(3) further dependencies
# $(4) target extension, default .odb
define do-copy
$(RESULTS_DIR)/$(1)$(if $(4),$(4),.odb): $(RESULTS_DIR)/$(2) $(3)
        $$(UNSET_AND_MAKE) do-$(1)$(if $(4),$(4),)

.PHONY: do-$(1)$(if $(4),$(4),)
do-$(1)$(if $(4),$(4),):
        cp $(RESULTS_DIR)/$(2) $(RESULTS_DIR)/$(1)$(if $(4),$(4),.odb)
endef


# STEP 1: Translate verilog to odb
#-------------------------------------------------------------------------------
$(eval $(call do-step,2_1_floorplan,$(RESULTS_DIR)/1_synth.v $(RESULTS_DIR)/1_synth.sdc $(TECH_LEF) $(SC_LEF) $(ADDITIONAL_LEFS) $(FOOTPRINT) $(SIG_MAP_FILE) $(FOOTPRINT_TCL) $(DONT_USE_SC_LIB),floorplan))

$(eval $(call do-copy,2_floorplan,2_1_floorplan.sdc,,.sdc))

# STEP 2: Macro Placement
#-------------------------------------------------------------------------------
$(eval $(call do-step,2_2_floorplan_macro,$(RESULTS_DIR)/2_1_floorplan.odb $(RESULTS_DIR)/1_synth.v $(RESULTS_DIR)/1_synth.sdc $(MACRO_PLACEMENT) $(MACRO_PLACEMENT_TCL),macro_place))

# STEP 3: Tapcell and Welltie insertion
#-------------------------------------------------------------------------------
$(eval $(call do-step,2_3_floorplan_tapcell,$(RESULTS_DIR)/2_2_floorplan_macro.odb $(TAPCELL_TCL),tapcell))

# STEP 4: PDN generation
#-------------------------------------------------------------------------------
$(eval $(call do-step,2_4_floorplan_pdn,$(RESULTS_DIR)/2_3_floorplan_tapcell.odb $(PDN_TCL),pdn))

$(eval $(call do-copy,2_floorplan,2_4_floorplan_pdn.odb,))

$(RESULTS_DIR)/2_floorplan.sdc: $(RESULTS_DIR)/2_1_floorplan.odb

.PHONY: do-floorplan
do-floorplan:
        $(UNSET_AND_MAKE) do-2_1_floorplan do-2_2_floorplan_macro do-2_3_floorplan_tapcell do-2_4_floorplan_pdn do-2_floorplan do-2_floorplan.sdc

.PHONY: clean_floorplan
clean_floorplan:
        rm -f $(RESULTS_DIR)/2_*floorplan*.odb $(RESULTS_DIR)/2_floorplan.sdc $(RESULTS_DIR)/2_*.v $(RESULTS_DIR)/2_*.def
        rm -f $(REPORTS_DIR)/2_*
        rm -f $(LOG_DIR)/2_*

# ==============================================================================
#  ____  _        _    ____ _____
# |  _ \| |      / \  / ___| ____|
# | |_) | |     / _ \| |   |  _|
# |  __/| |___ / ___ \ |___| |___
# |_|   |_____/_/   \_\____|_____|
#
.PHONY: place
place: $(RESULTS_DIR)/3_place.odb \
       $(RESULTS_DIR)/3_place.sdc
# ==============================================================================
# STEP 1: Global placement without placed IOs, timing-driven, and routability-driven.
#-------------------------------------------------------------------------------
$(eval $(call do-step,3_1_place_gp_skip_io,$(RESULTS_DIR)/2_floorplan.odb $(RESULTS_DIR)/2_floorplan.sdc $(LIB_FILES),global_place_skip_io))

$(eval $(call do-step,3_2_place_iop,$(RESULTS_DIR)/3_1_place_gp_skip_io.odb $(IO_CONSTRAINTS),io_placement))

# STEP 3: Global placement with placed IOs, timing-driven, and routability-driven.
#-------------------------------------------------------------------------------
$(eval $(call do-step,3_3_place_gp,$(RESULTS_DIR)/3_2_place_iop.odb $(RESULTS_DIR)/2_floorplan.sdc $(LIB_FILES),global_place))

# STEP 4: Resizing & Buffering
#-------------------------------------------------------------------------------
$(eval $(call do-step,3_4_place_resized,$(RESULTS_DIR)/3_3_place_gp.odb $(RESULTS_DIR)/2_floorplan.sdc,resize))

.PHONY: clean_resize
clean_resize:
        rm -f $(RESULTS_DIR)/3_4_place_resized.odb

# STEP 5: Detail placement
#-------------------------------------------------------------------------------
$(eval $(call do-step,3_5_place_dp,$(RESULTS_DIR)/3_4_place_resized.odb,detail_place))

$(eval $(call do-copy,3_place,3_5_place_dp.odb,))

$(eval $(call do-copy,3_place,2_floorplan.sdc,,.sdc))

.PHONY: do-place
do-place:
        $(UNSET_AND_MAKE) do-3_1_place_gp_skip_io do-3_2_place_iop do-3_3_place_gp do-3_4_place_resized do-3_5_place_dp do-3_place do-3_place.sdc

# Clean Targets
#-------------------------------------------------------------------------------
.PHONY: clean_place
clean_place:
        rm -f $(RESULTS_DIR)/3_*place*.odb
        rm -f $(RESULTS_DIR)/3_place.sdc
        rm -f $(RESULTS_DIR)/3_*.def $(RESULTS_DIR)/3_*.v
        rm -f $(REPORTS_DIR)/3_*
        rm -f $(LOG_DIR)/3_*


# ==============================================================================
#   ____ _____ ____
#  / ___|_   _/ ___|
# | |     | | \___ \
# | |___  | |  ___) |
#  \____| |_| |____/
#
.PHONY: cts
cts: $(RESULTS_DIR)/4_cts.odb \
     $(RESULTS_DIR)/4_cts.sdc
# ==============================================================================

# Run TritonCTS
# ------------------------------------------------------------------------------
$(eval $(call do-step,4_1_cts,$(RESULTS_DIR)/3_place.odb $(RESULTS_DIR)/3_place.sdc,cts))

$(RESULTS_DIR)/4_cts.sdc: $(RESULTS_DIR)/4_cts.odb

$(eval $(call do-copy,4_cts,4_1_cts.odb))

.PHONY: do-cts
do-cts:
        $(UNSET_AND_MAKE) do-4_1_cts do-4_cts

.PHONY: clean_cts
clean_cts:
        rm -rf $(RESULTS_DIR)/4_*cts*.odb $(RESULTS_DIR)/4_cts.sdc $(RESULTS_DIR)/4_*.v $(RESULTS_DIR)/4_*.def
        rm -f  $(REPORTS_DIR)/4_*
        rm -rf $(LOG_DIR)/4_*


# ==============================================================================
#  ____   ___  _   _ _____ ___ _   _  ____
# |  _ \ / _ \| | | |_   _|_ _| \ | |/ ___|
# | |_) | | | | | | | | |  | ||  \| | |  _
# |  _ <| |_| | |_| | | |  | || |\  | |_| |
# |_| \_\\___/ \___/  |_| |___|_| \_|\____|
#
.PHONY: route
route: $(RESULTS_DIR)/5_route.odb \
       $(RESULTS_DIR)/5_route.sdc

.PHONY: grt
grt: $(RESULTS_DIR)/5_1_grt.odb

# ==============================================================================


# STEP 1: Run global route
#-------------------------------------------------------------------------------
$(eval $(call do-step,5_1_grt,$(RESULTS_DIR)/4_cts.odb $(FASTROUTE_TCL) $(PRE_GLOBAL_ROUTE),global_route))

# STEP 2: Run detailed route
#-------------------------------------------------------------------------------
$(eval $(call do-step,5_2_route,$(RESULTS_DIR)/5_1_grt.odb,detail_route))

$(eval $(call do-step,5_3_fillcell,$(RESULTS_DIR)/5_2_route.odb,fillcell))

$(eval $(call do-copy,5_route,5_3_fillcell.odb))

$(eval $(call do-copy,5_route,5_1_grt.sdc,,.sdc))

.PHONY: do-route
do-route:
        $(UNSET_AND_MAKE) do-5_1_grt do-5_2_route do-5_3_fillcell do-5_route do-5_route.sdc

.PHONY: do-grt
do-grt:
        $(UNSET_AND_MAKE) do-5_1_grt

.PHONY: clean_route
clean_route:
        rm -rf output*/ results*.out.dmp layer_*.mps
        rm -rf *.gdid *.log *.met *.sav *.res.dmp
        rm -rf $(RESULTS_DIR)/route.guide $(RESULTS_DIR)/output_guide.mod $(RESULTS_DIR)/updated_clks.sdc
        rm -rf $(RESULTS_DIR)/5_*.odb $(RESULTS_DIR)/5_route.sdc $(RESULTS_DIR)/5_*.def $(RESULTS_DIR)/5_*.v
        rm -f  $(REPORTS_DIR)/5_*
        rm -f  $(LOG_DIR)/5_*

.PHONY: klayout_tr_rpt
klayout_tr_rpt: $(RESULTS_DIR)/5_route.def $(OBJECTS_DIR)/klayout.lyt
        $(call KLAYOUT_FOUND)
        $(KLAYOUT_CMD) -rd in_drc="$(REPORTS_DIR)/5_route_drc.rpt" \
                -rd in_def="$<" \
                -rd tech_file=$(OBJECTS_DIR)/klayout.lyt \
                -rm $(UTILS_DIR)/viewDrc.py

.PHONY: klayout_guides
klayout_guides: $(RESULTS_DIR)/5_route.def $(OBJECTS_DIR)/klayout.lyt
        $(call KLAYOUT_FOUND)
        $(KLAYOUT_CMD) -rd in_guide="$(RESULTS_DIR)/route.guide" \
                -rd in_def="$<" \
                -rd net_name=$(GUIDE_NET) \
                -rd tech_file=$(OBJECTS_DIR)/klayout.lyt \
                -rm $(UTILS_DIR)/viewGuide.py

# ==============================================================================
#  _____ ___ _   _ ___ ____  _   _ ___ _   _  ____
# |  ___|_ _| \ | |_ _/ ___|| | | |_ _| \ | |/ ___|
# | |_   | ||  \| || |\___ \| |_| || ||  \| | |  _
# |  _|  | || |\  || | ___) |  _  || || |\  | |_| |
# |_|   |___|_| \_|___|____/|_| |_|___|_| \_|\____|
#
.PHONY: finish
finish: $(LOG_DIR)/6_report.log \
        $(RESULTS_DIR)/6_final.v \
        $(RESULTS_DIR)/6_final.sdc \
        $(GDS_FINAL_FILE)
        $(UNSET_AND_MAKE) elapsed

.PHONY: elapsed
elapsed:
        -@$(UTILS_DIR)/genElapsedTime.py -d $(BLOCK_LOG_FOLDERS) $(LOG_DIR)

# Useful when working with macros, see elapsed time for all macros in platform
.PHONY: elapsed-all
elapsed-all:
        @$(UTILS_DIR)/genElapsedTime.py -d $(shell find $(WORK_HOME)/logs/$(PLATFORM)/*/*/ -type d)

$(eval $(call do-step,6_1_fill,$(RESULTS_DIR)/5_route.odb $(RESULTS_DIR)/5_route.sdc $(FILL_CONFIG),density_fill))

$(eval $(call do-copy,6_1_fill,5_route.sdc,,.sdc))

$(eval $(call do-copy,6_final,5_route.sdc,,.sdc))

$(eval $(call do-step,6_report,$(RESULTS_DIR)/6_1_fill.odb $(RESULTS_DIR)/6_1_fill.sdc,final_report,.log,$(LOG_DIR)))

$(RESULTS_DIR)/6_final.def: $(LOG_DIR)/6_report.log

# The final results are called 6_final.*, so it is convenient when scripting
# to have the names of the artifacts match the name of the target
.PHONY: do-final
do-final: do-finish

.PHONY: final
final: finish

.PHONY: do-finish
do-finish:
        $(UNSET_AND_MAKE) do-6_1_fill do-6_1_fill.sdc do-6_final.sdc do-6_report do-gds elapsed

.PHONY: generate_abstract
generate_abstract: $(RESULTS_DIR)/6_final.gds $(RESULTS_DIR)/6_final.def  $(RESULTS_DIR)/6_final.v $(RESULTS_DIR)/6_final.sdc
        $(UNSET_AND_MAKE) do-generate_abstract

# Set ABSTRACT_SOURCE if you want to create an abstract from another stage than 6_final.
.PHONY: do-generate_abstract
do-generate_abstract:
        mkdir -p $(LOG_DIR) $(REPORTS_DIR)
        ($(TIME_CMD) $(OPENROAD_CMD) $(SCRIPTS_DIR)/generate_abstract.tcl -metrics $(LOG_DIR)/generate_abstract.json) 2>&1 | tee $(abspath $(LOG_DIR)/generate_abstract.log)

.PHONY: clean_abstract
clean_abstract:
        rm -f $(RESULTS_DIR)/$(DESIGN_NAME).lib $(RESULTS_DIR)/$(DESIGN_NAME).lef

# Merge wrapped macros using Klayout
#-------------------------------------------------------------------------------
$(WRAPPED_GDSOAS): $(OBJECTS_DIR)/klayout_wrap.lyt $(WRAPPED_LEFS)
        $(call KLAYOUT_FOUND)
        ($(TIME_CMD) $(KLAYOUT_CMD) -zz -rd design_name=$(basename $(notdir $@)) \
                -rd in_def=$(OBJECTS_DIR)/def/$(notdir $(@:$(STREAM_SYSTEM_EXT)=def)) \
                -rd in_files="$(ADDITIONAL_GDSOAS)" \
                -rd config_file=$(FILL_CONFIG) \
                -rd seal_file="" \
                -rd out_file=$@ \
                -rd tech_file=$(OBJECTS_DIR)/klayout_wrap.lyt \
                -rd layer_map=$(GDS_LAYER_MAP) \
                -r $(UTILS_DIR)/def2stream.py) 2>&1 | tee $(abspath $(LOG_DIR)/6_merge_$(basename $(notdir $@)).log)

# Merge GDS using Klayout
#-------------------------------------------------------------------------------
$(GDS_MERGED_FILE): $(RESULTS_DIR)/6_final.def $(OBJECTS_DIR)/klayout.lyt $(GDSOAS_FILES) $(WRAPPED_GDSOAS) $(SEAL_GDSOAS)
        $(UNSET_AND_MAKE) do-gds-merged

.PHONY: do-gds-merged
do-gds-merged:
        $(call KLAYOUT_FOUND)
        ($(TIME_CMD) $(STDBUF_CMD) $(KLAYOUT_CMD) -zz -rd design_name=$(DESIGN_NAME) \
                -rd in_def=$(RESULTS_DIR)/6_final.def \
                -rd in_files="$(GDSOAS_FILES) $(WRAPPED_GDSOAS)" \
                -rd seal_file="$(SEAL_GDSOAS)" \
                -rd out_file=$(GDS_MERGED_FILE) \
                -rd tech_file=$(OBJECTS_DIR)/klayout.lyt \
                -rd layer_map=$(GDS_LAYER_MAP) \
                -r $(UTILS_DIR)/def2stream.py) 2>&1 | tee $(abspath $(LOG_DIR)/6_1_merge.log)

$(RESULTS_DIR)/6_final.v: $(LOG_DIR)/6_report.log

.PHONY: do-gds
do-gds:
        $(UNSET_AND_MAKE) do-klayout_tech do-klayout do-klayout_wrap do-gds-merged
        cp $(GDS_MERGED_FILE) $(GDS_FINAL_FILE)

$(GDS_FINAL_FILE): $(GDS_MERGED_FILE)
        cp $< $@

.PHONY: drc
drc: $(REPORTS_DIR)/6_drc.lyrdb

$(REPORTS_DIR)/6_drc.lyrdb: $(GDS_FINAL_FILE) $(KLAYOUT_DRC_FILE)
ifneq ($(KLAYOUT_DRC_FILE),)
        $(call KLAYOUT_FOUND)
        ($(TIME_CMD) $(KLAYOUT_CMD) -zz -rd in_gds="$<" \
                -rd report_file=$(abspath $@) \
                -r $(KLAYOUT_DRC_FILE)) 2>&1 | tee $(abspath $(LOG_DIR)/6_drc.log)
        # Hacky way of getting DRV count (don't error on no matches)
        grep -c "<value>" $@ > $(REPORTS_DIR)/6_drc_count.rpt || [[ $$? == 1 ]]
else
        echo "DRC not supported on this platform" > $@
endif

$(RESULTS_DIR)/6_final.cdl: $(RESULTS_DIR)/6_final.v
        ($(TIME_CMD) $(OPENROAD_CMD) $(SCRIPTS_DIR)/cdl.tcl) 2>&1 | tee $(abspath $(LOG_DIR)/6_cdl.log)

$(OBJECTS_DIR)/6_final_concat.cdl: $(RESULTS_DIR)/6_final.cdl $(CDL_FILE)
        cat $^ > $@

.PHONY: lvs
lvs: $(RESULTS_DIR)/6_lvs.lvsdb

$(RESULTS_DIR)/6_lvs.lvsdb: $(GDS_FINAL_FILE) $(KLAYOUT_LVS_FILE) $(OBJECTS_DIR)/6_final_concat.cdl
ifneq ($(KLAYOUT_LVS_FILE),)
        $(call KLAYOUT_FOUND)
        ($(TIME_CMD) $(KLAYOUT_CMD) -b -rd in_gds="$<" \
                -rd cdl_file=$(abspath $(OBJECTS_DIR)/6_final_concat.cdl) \
                -rd report_file=$(abspath $@) \
                -r $(KLAYOUT_LVS_FILE)) 2>&1 | tee $(abspath $(LOG_DIR)/6_lvs.log)
else
        echo "LVS not supported on this platform" > $@
endif

.PHONY: clean_finish
clean_finish:
        rm -rf $(RESULTS_DIR)/6_*.gds $(RESULTS_DIR)/6_*.oas $(RESULTS_DIR)/6_*.odb $(RESULTS_DIR)/6_*.v $(RESULTS_DIR)/6_*.def $(RESULTS_DIR)/6_*.sdc $(RESULTS_DIR)/6_*.spef
        rm -rf $(REPORTS_DIR)/6_*.rpt
        rm -f  $(LOG_DIR)/6_*


# ==============================================================================
#  __  __ ___ ____   ____
# |  \/  |_ _/ ___| / ___|
# | |\/| || |\___ \| |
# | |  | || | ___) | |___
# |_|  |_|___|____/ \____|
#
# ==============================================================================

.PHONY: all
all: synth floorplan place cts route finish

.PHONY: clean
clean:
        @echo
        @echo "Make clean disabled."
        @echo "Use make clean_all or clean individual steps:"
        @echo "  clean_synth clean_floorplan clean_place clean_cts clean_route clean_finish"
        @echo

.PHONY: clean_all
clean_all: clean_synth clean_floorplan clean_place clean_cts clean_route clean_finish clean_metadata clean_abstract
        rm -rf $(OBJECTS_DIR)

.PHONY: nuke
nuke: clean_test clean_issues
        rm -rf ./results ./logs ./reports ./objects
        rm -rf layer_*.mps macrocell.list *best.plt *_pdn.def
        rm -rf *.rpt *.rpt.old *.def.v pin_dumper.log
        rm -f $(OBJECTS_DIR)/versions.txt $(OBJECTS_DIR)/copyright.txt dummy.guide

# DEF/GDS/OAS viewer shortcuts
#-------------------------------------------------------------------------------
.PHONY: $(foreach file,$(RESULTS_DEF) $(RESULTS_GDS) $(RESULTS_OAS),klayout_$(file))
$(foreach file,$(RESULTS_DEF) $(RESULTS_GDS) $(RESULTS_OAS),klayout_$(file)): klayout_%: $(OBJECTS_DIR)/klayout.lyt
        $(KLAYOUT_CMD) -nn $(OBJECTS_DIR)/klayout.lyt $(RESULTS_DIR)/$*

.PHONY: gui_synth
gui_synth:
        $(OPENROAD_GUI_CMD) $(SCRIPTS_DIR)/sta-synth.tcl
.PHONY: open_synth
open_synth:
        $(OPENROAD_NO_EXIT_CMD) $(SCRIPTS_DIR)/sta-synth.tcl

$(eval $(call OPEN_GUI_SHORTCUT,floorplan,2_floorplan.odb))
$(eval $(call OPEN_GUI_SHORTCUT,place,3_place.odb))
$(eval $(call OPEN_GUI_SHORTCUT,cts,4_cts.odb))
$(eval $(call OPEN_GUI_SHORTCUT,route,5_route.odb))
$(eval $(call OPEN_GUI_SHORTCUT,grt,5_1_grt.odb))
$(eval $(call OPEN_GUI_SHORTCUT,final,6_final.odb))

$(foreach file,$(RESULTS_DEF),$(eval $(call OPEN_GUI,$(file),DEF_FILE)))
$(foreach file,$(RESULTS_ODB),$(eval $(call OPEN_GUI,$(file),ODB_FILE)))

# Write a def for the corresponding odb
$(foreach file,$(RESULTS_ODB),$(file).def): %.def:
        ODB_FILE=$(RESULTS_DIR)/$* DEF_FILE=$(RESULTS_DIR)/$@ $(OPENROAD_CMD) $(SCRIPTS_DIR)/write_def.tcl
#
# Write a verilog for the corresponding odb
$(foreach file,$(RESULTS_ODB),$(file).v): %.v:
        ODB_FILE=$(RESULTS_DIR)/$* VERILOG_FILE=$(RESULTS_DIR)/$@ $(OPENROAD_CMD) $(SCRIPTS_DIR)/write_verilog.tcl

# Drop into yosys with all environment variables, useful to for instance
# debug synthesis, or run other commands aftewards, such as "show" to
# generate a .dot file of the design to visualize designs.
.PHONY: yosys
yosys:
        $(YOSYS_EXE)

# Drop into a bash shell with all environment variables, useful for debugging
.PHONY: bash
bash:
        bash --init-file <(echo "PS1='\[\e[32m\]Makefile Environment \[\e[0m\] \w $ '")

.PHONY: all_defs
all_defs : $(foreach file,$(RESULTS_ODB),$(file).def)
.PHONY: all_verilog
all_verilog : $(foreach file,$(RESULTS_ODB),$(file).v)

.PHONY: handoff
handoff : all_defs all_verilog

.PHONY: test-unset-and-make-%
test-unset-and-make-%: ; $(UNSET_AND_MAKE) $*

.phony: klayout
klayout:
        $(KLAYOUT_CMD)

.phony: run
run:
        @mkdir -p $(RESULTS_DIR) $(LOG_DIR) $(REPORTS_DIR) $(OBJECTS_DIR)
        ($(OPENROAD_CMD) -no_splash $(if $(filter %.py,$(RUN_SCRIPT)),-python) $(RUN_SCRIPT) 2>&1 | tee $(abspath $(LOG_DIR)/$(RUN_LOG_NAME_STEM).log))

export RUN_YOSYS_ARGS ?= -c $(SCRIPTS_DIR)/yosys_keep.tcl
.phony: run-yosys
run-yosys:
        $(YOSYS_EXE) $(RUN_YOSYS_ARGS)

# Utilities
#-------------------------------------------------------------------------------
include $(UTILS_DIR)/utils.mk
export PRIVATE_DIR ?= ../../private_tool_scripts
-include $(PRIVATE_DIR)/private.mk
```
