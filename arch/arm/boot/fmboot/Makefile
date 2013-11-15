# Build an image for Fast Models

AS		= $(CROSS_COMPILE)gcc -c
LD		= $(CROSS_COMPILE)ld

DTC = $(obj)/../../../../scripts/dtc/dtc
DTS = $(obj)/../dts/axm55xx-sim.dts
ZIMAGE = $(obj)/../zImage

clean-files := fmboot.o zImage.fm axm55xx-sim.dtb

arch/arm/boot/linux.img: $(obj)/fmboot.o $(srctree)/$(obj)/fmboot.lds $(obj)/zImage.fm
	cd $(obj) && $(LD) -o ../linux.img --script=$(srctree)/$(obj)/fmboot.lds
	tar jcf $(obj)/../linux.img.tar.bz2 $(obj)/../linux.img

$(obj)/zImage.fm: $(ZIMAGE) $(obj)/axm55xx-sim.dtb
	python $(srctree)/$(obj)/pack.py $(ZIMAGE) $(obj)/axm55xx-sim.dtb > $@

$(obj)/axm55xx-sim.dtb: $(DTS)
	$(DTC) -O dtb -o $@ $<

$(obj)/fmboot.o: $(obj)/fmboot.S
	$(AS) -o $@ $<
