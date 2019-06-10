This is the patched version of DCMI and MEI for Quanta Windmill mobo (OpenCompute node)

Currently here only binary kernel modules form DCMI and MEI interfaces, modules not striped, so if you need, stripe them.

Thanks nz0.14910 from servethehome.com for this https://forums.servethehome.com/index.php?threads/potential-deal-2-x-dual-2011-nodes-199-quanta-openrack.6856/page-34

## Howto:

Download the repository, and install the modules.

## Manual build:
1. Download the source files from packages in https://launchpad.net/~opencompute-developers/+archive/ubuntu/ocp-certification-tools-ppa/
    - dcmi-dkms-2.1.6.28.MEI
    - mei-dkms-7.1.21.4.S

2. For mei-dkms add ```#include <linux/irq.h>``` to **mei_dev.h** file:
    ```bash
    sed -i '/#include "hw.h"/a #include <linux\/irq.h>' mei_dev.h
    ```
3. For dcmi-dkms replace ```f_dentry``` with ```f_path.dentry``` in **dcmi_main.c**:
    ```bash
    sed -i 's/f_dentry/f_path.dentry/g' dcmi_main.c
    ```
4. Build and install each module:
    ```bash
    make
    make install
   ```
5. Additionally, you can stripe modules ( remove debug-symbols), and this will reduce module size ( from 1.6M to 141K):
    ```bash
    find -type f -name \*.ko -print -exec strip --strip-debug \{\} \;
    ```

### TODO:
Make rpm and deb specs with DKMS-support
