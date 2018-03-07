#------------------------------------------------------------------------------
# Makefile for SCR1 FPGA tests
#------------------------------------------------------------------------------

# Parameters
export ARCH ?= imfc

# Paths
export root_dir := $(CURDIR)
export inc_dir := $(root_dir)/tests_common
export bld_dir := $(root_dir)/build

test_results := $(bld_dir)/test_results.txt
test_info := $(bld_dir)/test_info

# Environment
export CROSS_PREFIX ?= riscv32-unknown-elf-

# Targets
.PHONY: fpga_sw

fpga_sw:fpga_de2_115

fpga_arty:
	$(eval export SYS_CLK := 25000000)
	$(info arty_sys_clk=$(SYS_CLK))
	mkdir -p build
	$(MAKE) -C ./test_src ITERATIONS=500 dst_dir=$(root_dir)/build OPT=3lto clean all
	$(MAKE) -C ./test_src ITERATIONS=500 dst_dir=$(root_dir)/build OPT=2 clean all

fpga_de2_115:
	$(eval export SYS_CLK := 20000000)
	$(info de10lite_sys_clk=$(SYS_CLK))
	mkdir -p build
	$(MAKE) -C ./test_src ITERATIONS=500 dst_dir=$(root_dir)/build OPT=3lto clean all
	$(MAKE) -C ./test_src ITERATIONS=500 dst_dir=$(root_dir)/build OPT=2 clean all

fpga_de10lite:
	$(eval export SYS_CLK := 20000000)
	$(info de10lite_sys_clk=$(SYS_CLK))
	mkdir -p build
	$(MAKE) -C ./test_src ITERATIONS=500 dst_dir=$(root_dir)/build OPT=3lto clean all
	$(MAKE) -C ./test_src ITERATIONS=500 dst_dir=$(root_dir)/build OPT=2 clean all

fpga_a5:
	$(eval export SYS_CLK := 30000000)
	$(info a5_sys_clk=$(SYS_CLK))
	mkdir -p build
	$(MAKE) -C ./test_src ITERATIONS=500 dst_dir=$(root_dir)/build OPT=3lto clean all
	$(MAKE) -C ./test_src ITERATIONS=500 dst_dir=$(root_dir)/build OPT=2 clean all

clean:
	$(MAKE) -C ./test_src dst_dir=$(root_dir)/build OPT=3lto clean
	$(MAKE) -C ./test_src dst_dir=$(root_dir)/build OPT=2 clean
	$(MAKE) -C ./test_src dst_dir=$(root_dir)/build OPT=3lto clean
	$(MAKE) -C ./test_src dst_dir=$(root_dir)/build OPT=2 clean
