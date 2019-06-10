This is the patched version of DCMI and MEI for Quanta Windmill mobo (OpenCompute node)

Thanks nz0.14910 from servethehome.com for this https://forums.servethehome.com/index.php?threads/potential-deal-2-x-dual-2011-nodes-199-quanta-openrack.6856/page-34

TODO: make rpm and deb specs with DKMS-support


Howto:

Download the repository, and do make, and make install.



Download the source files from Packages in https://launchpad.net/~opencompute-developers/+archive/ubuntu/ocp-certification-tools-ppa/

- dcmi-dkms-2.1.6.28.MEI
- mei-dkms-7.1.21.4.S

for mei-dkms add #include <linux/irq.h> to mei_dev.h

for dcmi-dkms replace f_dentry with f_path.dentry in dcmi_main.c 

you need to reboot in order to load the newly compiled mei module.

load the module dcmi.


