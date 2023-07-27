# GW-R86S-U1 with Mellanox ConnectX-4 MCX4421A-ACQN

## Introduction
> If you're new to GW-R86S's world and looking for a device, I highly recommend starting with [Patrick Kennedy](https://www.servethehome.com/the-gowin-r86s-revolution-low-power-2-5gbe-and-10gbe-intel-nvidia/)'s review.

I've established this repository to document the upgrade process of my GW-R86S-U1, where I'll be installing a Mellanox ConnectX-4 MCX4421A-ACQN interface.

First and foremost, let me provide you with the specifications of my GW-R86S-U1:

* CPU: Intel Celeron N5105
* Memory: 8GB
* ECC: 128GB
* Original Interfaces: 3*2.5g ethernet ports + ConnectX-3 EN 10 Gigabit Ethernet CX341A

As I proceed with the upgrade, I'll be sharing detailed steps and any insights I gain through this repository.

## About the Mellanox ConnectX-4 MCX4421A-ACQN

> For more information about the OCP, I found this really interesting [document](https://www.opencompute.org/documents/ocp-mezz-2-0-rev1-1-20200103-nocb-pdf) from www.opencompute.org with a lot information.

It's important to be aware that the GW-R86S-U* models come equipped with an OCP connector, which facilitates communication via PCIe 3.0 x4 with the CX341A card. These models have been specifically designed to be a seamless fit with the CX341A card. If you're looking to replace the CX341A card, the ideal option would be the CX4421A in the version MCX4421A-ACQN.

I purchased the MCX4421A-ACQN card from eBay at approximately ~$90 USD.

![Ebay MCX4421A-ACQN card used.](https://github.com/camilo-nunez/r86s-25g/blob/9d09ede85fda08aa975fab1a98c3d80bfffdead1/imgs/552eed7eb070f074.png)

Prior to changing and installing the interface card, it is crucial to ensure that the card's firmware is up to date. Therefore, let's proceed with the firmware upgrade!

### Upgrade firmware

> You can find the official documentation for this [here](https://network.nvidia.com/support/firmware/nic/).

1. Get the NVIDIA Firmware Tools (MFT) from here: https://network.nvidia.com/products/adapter-software/firmware-tools/
2. As root, start the mst tools with: `sudo mst start`
3. To verify the Part Number (OPN), the PSID, and the PCI device name, execute the command: `sudo mlxfwmanager`.
4. Once you have obtained the OPN and PSID, proceed to download the official firmware for your device from the following link: https://network.nvidia.com/support/firmware/connectx4lxen/.
5. After obtaining the PCI device name, proceed to burn the downloaded binary firmware using the following command: `sudo mlxburn –i <fw-ConnectX-4-downloaded>.bin –d /dev/mst/<PCI-device-name>`
> More info about the `mlxburn` command [here](https://docs.nvidia.com/networking/pages/viewpage.action?pageId=12013137).