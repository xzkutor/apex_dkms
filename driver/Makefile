ifeq ($(KERNELRELEASE), )
KERNELDIR := /lib/modules/$(shell uname -r)/build
PWD :=$(shell pwd)
default:
	$(MAKE) -C $(KERNELDIR)  M=$(PWD)
clean:
	rm -rf *.mk .tmp_versions Module.symvers *.mod.c *.o .*.o.d *.ko .*.cmd Module.markers modules.order *.a *.mod
load:
	insmod gasket.ko
	insmod apex.ko
unload:
	rmmod apex
	rmmod gasket
install: default
	mkdir -p /lib/modules/$(shell uname -r)/kernel/drivers/staging/gasket
	cp -f ./{apex,gasket}.ko /lib/modules/$(shell uname -r)/kernel/drivers/staging/gasket
	echo "apex\ngasket\n" >> /etc/modules
	depmod -a
uninstall:
	rm -rf /lib/modules/$(shell uname -r)/kernel/drivers/usb/serial/ch343.ko
	depmod -a
else
	obj-m := gasket.o apex.o
	gasket-y := gasket_core.o gasket_ioctl.o gasket_interrupt.o gasket_page_table.o gasket_sysfs.o
	apex-y := apex_driver.o
endif
