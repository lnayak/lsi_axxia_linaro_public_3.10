# Build an image for emulation.

OBJCOPY = $(CROSS_COMPILE)objcopy
DTC = $(obj)/../../../../scripts/dtc/dtc
DTS = $(obj)/../dts/axm55xx-emu.dts

clean-files := vmlinux.bin* linux.img axm55xx-emu.dtb

$(obj)/linux.img: $(obj)/axm55xx-emu.dtb $(obj)/../../../../vmlinux
	$(OBJCOPY) -O binary -R .note -R .comment -S $(obj)/../../../../vmlinux $(obj)/vmlinux.bin
	gzip -f -9 $(obj)/vmlinux.bin
	mkimage -f $(obj)/axm55xx-emu.its $@

$(obj)/axm55xx-emu.dtb: $(DTS)
	$(DTC) -O dtb -R 32 -p 0x400 -o $@ $<
