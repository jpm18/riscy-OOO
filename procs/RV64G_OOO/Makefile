
# Copyright (c) 2017 Massachusetts Institute of Technology
# 
# Permission is hereby granted, free of charge, to any person
# obtaining a copy of this software and associated documentation
# files (the "Software"), to deal in the Software without
# restriction, including without limitation the rights to use, copy,
# modify, merge, publish, distribute, sublicense, and/or sell copies
# of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
# 
# The above copyright notice and this permission notice shall be
# included in all copies or substantial portions of the Software.
# 
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
# EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
# MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
# NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS
# BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN
# ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
# CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

PROC := RV64G_OOO

# core size
CORE_SIZE ?= SMALL
# cache size
CACHE_SIZE ?= LARGE
# always include perf counter
PERF_COUNT := true
# dram type in simulation: VC707 or AWSF1
SIM_DRAM_TYPE := AWSF1
# use Xilinx FPU IP cores
USE_XILINX_FPU ?= true

# default 1 core
CORE_NUM ?= 1
# TSO or WEAK
TSO_MM ?= false
# security
SECURITY ?= false
SECURE_LLC ?= false
SECURE_FLUSH ?= false
SECURE_NONE ?= false
SIM_LOG_LLC_PARTITION_NUM ?=
# default check cache deadlock and rename error
CHECK_DEADLOCK ?= true
RENAME_DEBUG ?= true

# clk frequency depends on core size
ifneq (,$(filter $(CORE_SIZE),TINY SMALL BOOM MEDIUM))
USER_CLK_PERIOD ?= 24
else ifneq (,$(filter $(CORE_SIZE),SMALL_WIDE LARGE))
USER_CLK_PERIOD ?= 32
else ifneq (,$(filter $(CORE_SIZE),LARGE_WIDE))
USER_CLK_PERIOD ?= 40
else
$(error unsupported CORE_SIZE)
endif

ifeq (,$(filter $(CACHE_SIZE),SMALL LARGE MC))
$(error unsupported CACHE_SIZE)
endif

# directories
BUILD_DIR := $(RISCY_HOME)/procs/build/$(PROC).core_$(CORE_NUM).core_$(CORE_SIZE).cache_$(CACHE_SIZE)
ifeq ($(TSO_MM),true)
BUILD_DIR := $(BUILD_DIR).tso
else
BUILD_DIR := $(BUILD_DIR).weak
endif
ifeq ($(SECURITY),true)
BUILD_DIR := $(BUILD_DIR).security
else ifeq ($(SECURE_LLC),true)
BUILD_DIR := $(BUILD_DIR).secure_llc
else ifeq ($(SECURE_FLUSH),true)
BUILD_DIR := $(BUILD_DIR).secure_flush
else ifeq ($(SECURE_NONE),true)
BUILD_DIR := $(BUILD_DIR).secure_none
endif
ifeq ($(CHECK_DEADLOCK),true)
BUILD_DIR := $(BUILD_DIR).check_deadlock
endif

include $(RISCY_HOME)/procs/scripts/Makefile.common

