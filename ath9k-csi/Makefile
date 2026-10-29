# Override des CONFIG nécessaires pour out-of-tree
export CONFIG_ATH9K=m
export CONFIG_ATH9K_PCI=y
export CONFIG_ATH9K_DEBUGFS=y
export CONFIG_ATH9K_BTCOEX_SUPPORT=y
export CONFIG_ATH9K_DFS_CERTIFIED=y
export CONFIG_ATH9K_HTC=n
export CONFIG_ATH9K_WOW=n
export CONFIG_ATH9K_HWRNG=n
export CONFIG_ATH9K_TX99=n
export CONFIG_ATH9K_STATION_STATISTICS=n
export CONFIG_ATH9K_DFS_DEBUGFS=n

KDIR  := /lib/modules/$(shell uname -r)/build
PWD   := $(shell pwd)

all:
	$(MAKE) -C $(KDIR) M=$(PWD) \
		EXTRA_CFLAGS="-I$(PWD) -DCONFIG_ATH9K_DEBUGFS -DCONFIG_ATH9K_PCI -DCONFIG_ATH9K_BTCOEX_SUPPORT -DCONFIG_ATH9K_DFS_CERTIFIED" \
		modules

clean:
	$(MAKE) -C $(KDIR) M=$(PWD) clean
