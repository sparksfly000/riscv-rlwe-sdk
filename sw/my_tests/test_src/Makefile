# Makefile

.PHONY: all clean riscv
all: riscv

bmarks = my_test

dst_dir          ?= $(CURDIR)
src_dir          := $(root_dir)/test_src/
tests_common_dir := ../tests_common/

include $(tests_common_dir)tests_common.mk

$(info src_dir=$(src_dir))

VPATH += $(src_dir) $(tests_common_dir)

FLAGS_ = $(PORT_CFLAGS)
FLAGS_ += $(XLFLAGS)
FLAGS_ += $(XCFLAGS)

FLAGS_STR = "$(FLAGS_)"

CFLAGS = -static -Wa,-march=$(MARCH) -march=$(MARCH) -mabi=$(MABI) -std=gnu99 $(PORT_CFLAGS) $(XLFLAGS) -fno-common -fno-builtin-printf -DFLAGS_STR=\"$(FLAGS_STR)\"
LFLAGS = -march=$(MARCH) -mabi=$(MABI) -nostartfiles -nostdlib $(XLFLAGS) -lc -lgcc

CFLAGS += -DITERATIONS=$(ITERATIONS)

bmarks_defs += -DSELF_TIMED=1

build_dir ?= $(dst_dir)/

incs  += -I. -I$(src_dir) -I$(tests_common_dir)
objs  :=

my_test_c_src = aes.c
my_test_asm_src =

my_test_c_objs   = $(patsubst %.c, $(build_dir)%.o, $(my_test_c_src) $(common_c_src))
my_test_asm_objs = $(patsubst %.S, $(build_dir)%.o, $(my_test_asm_src) $(common_asm_src))

my_test_elf = $(build_dir)my_test$(build_siffix).elf
my_test_bin = $(build_dir)my_test$(build_siffix).bin
my_test_map = $(build_dir)my_test$(build_siffix).map

$(my_test_elf): $(ld_script) $(my_test_asm_objs) $(my_test_c_objs)
	$(LD) $(incs) -o $@ -Wl,-Map=$(my_test_map) -T $^ $(LFLAGS)
	$(OBJCOPY) -Obinary -S $@ $(my_test_bin)
	$(RM) $(build_dir)*.o
	$(RM) $(my_test_elf)
	$(RM) $(my_test_map)

bmarks_riscv_elf = $(my_test_elf)
bmarks_riscv_dump =$(build_dir)my_test.$(build_siffix).dump

$(bmarks_riscv_dump): $(bmarks_riscv_elf)

%.dump: %.elf
	$(OBJDUMP) -w -x -d -s -z -S $< > $@

$(build_dir)%.o: $(src_dir)%.c | $(build_dir)
	$(CC) $(CFLAGS) $(bmarks_defs) -c $(incs) $< -o $@

$(build_dir)%.o: $(tests_common_dir)%.c | $(build_dir)
	$(CC) $(CFLAGS) $(bmarks_defs) -c $(incs) $< -o $@

$(build_dir)%.o: $(tests_common_dir)%.S | $(build_dir)
	$(CC) $(CFLAGS) $(bmarks_defs) -D__ASSEMBLY__=1 -c $(incs) $< -o $@

riscv: $(bmarks_riscv_elf) $(bmarks_riscv_dump)

$(build_dir):
	mkdir -p $(build_dir)

clean:
	rm -rf $(my_test_elf) $(my_test_bin) $(my_test_map)
