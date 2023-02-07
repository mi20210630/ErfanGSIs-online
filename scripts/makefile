# SPDX-License-Identifier: GPL-2.0-only
EROFS_VERSION = "1.0"
ccflags-y += -DEROFS_VERSION=\"$(EROFS_VERSION)\"
CONFIG_EROFS_FS=y
CONFIG_EROFS_FS_DEBUG=y
CONFIG_EROFS_FS_XATTR=y
CONFIG_EROFS_FS_POSIX_ACL=y
CONFIG_EROFS_FS_SECURITY=y
CONFIG_EROFS_FS_ZIP=y
CONFIG_EROFS_FS_CLUSTER_PAGE_LIMIT=1
obj-m += erofs.o
erofs-objs := super.o inode.o data.o namei.o dir.o utils.o
erofs-$(CONFIG_EROFS_FS_XATTR) += xattr.o
erofs-$(CONFIG_EROFS_FS_ZIP) += decompressor.o zmap.o zdata.o

ifneq ($(KERNELRELEASE),)
# call from kernel build system
obj-m   := erofs.o
else
KERNELDIR ?= /lib/modules/$(shell uname -r)/build
PWD       := ~/linux-erofs/fs/erofs
default:
        $(MAKE) -C $(KERNELDIR) M=$(PWD) modules
        echo ${KERNELRELEASE}
endif
clean:
        rm -rf *.o *~ core .depend .*.cmd *.ko *.mod.c .tmp_versions Module.symvers modules.order
depend .depend dep:
        $(CC) $(EXTRA_CFLAGS) -M *.c > .depend
ifeq (.depend,$(wildcard .depend))
include .depend
endif
