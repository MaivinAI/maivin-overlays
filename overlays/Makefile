# your kernel sources
STAGING_KERNEL_DIR ?= $(INSTALL_MOD_PATH)/lib/modules/$(KERNELRELEASE)/source/

# kernel output (if building out-of-tree)
KBUILD_OUTPUT ?= $(STAGING_KERNEL_DIR)

DTC_FLAGS := '-@'

KERNEL_INCLUDE = " \
    ${STAGING_KERNEL_DIR}/arch/arm64/boot/dts/*/ \
"

DTS_INCLUDES := $(patsubst %,-I%,$(dir $(wildcard $(KERNEL_INCLUDE))))

HOSTCC := gcc $(DTS_INCLUDES)

PWD := $(shell pwd)

dtb-y += maivin1.dtbo
dtb-y += maivin1-ar0521.dtbo
dtb-y += maivin1-os08a20.dtbo
dtb-y += maivin1-gps.dtbo
dtb-y += maivin1-m2usb.dtbo
dtb-y += maivin1-m2pcie.dtbo
dtb-y += maivin2.dtbo
dtb-y += maivin2-os08a20.dtbo
dtb-y += maivin2-m2usb.dtbo
dtb-y += maivin2-m2pcie.dtbo

targets += $(dtb-y)
always  := $(dtb-y)

# adopted to dtbo from scripts/Makefile.lib
$(obj)/%.dtbo: $(src)/%.dts $(DTC) FORCE
	$(call if_changed_dep,dtc,dtb)

all:
	make -C $(KBUILD_OUTPUT) M=$(PWD)

clean:
	make -C $(KBUILD_OUTPUT) M=$(PWD) clean
