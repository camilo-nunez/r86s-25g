# GW-R86S-U1 with Mellanox ConnectX-4 MCX4421A-ACQN

# Introduction
> If you're new to GW-R86S's world and looking for a device, I highly recommend starting with [Patrick Kennedy](https://www.servethehome.com/the-gowin-r86s-revolution-low-power-2-5gbe-and-10gbe-intel-nvidia/)'s review.

I've established this repository to document the upgrade process of my GW-R86S-U1, where I'll be installing a Mellanox ConnectX-4 MCX4421A-ACQN interface.

First and foremost, let me provide you with the specifications of my GW-R86S-U1:

* CPU: Intel Celeron N5105
* Memory: 8GB
* ECC: 128GB
* Original Interfaces: 3*2.5g ethernet ports + ConnectX-3 EN 10 Gigabit Ethernet CX341A

As I proceed with the upgrade, I'll be sharing detailed steps and any insights I gain through this repository.

# About the Mellanox ConnectX-4 MCX4421A-ACQN

> For more information about the OCP, I found this really interesting [document](https://www.opencompute.org/documents/ocp-mezz-2-0-rev1-1-20200103-nocb-pdf) from www.opencompute.org with a lot information.

It's important to be aware that the GW-R86S-U* models come equipped with an OCP connector, which facilitates communication via PCIe 3.0 x4 with the CX341A card. These models have been specifically designed to be a seamless fit with the CX341A card. If you're looking to replace the CX341A card, the ideal option would be the CX4421A in the version MCX4421A-ACQN.

I purchased the MCX4421A-ACQN card from eBay at approximately ~$90 USD.

![Ebay MCX4421A-ACQN card used.](https://github.com/camilo-nunez/r86s-25g/blob/9d09ede85fda08aa975fab1a98c3d80bfffdead1/imgs/552eed7eb070f074.png)

Prior to changing and installing the interface card, it is crucial to ensure that the card's firmware is up to date. Therefore, let's proceed with the firmware upgrade!

![MCX4421A-ACQN card.](https://github.com/camilo-nunez/r86s-25g/blob/1b3a5a17c6c8ad0920ae7d28878fcb13baf4ef1a/imgs/7f4baf08b8713a04.gif)

## Upgrade firmware

> You can find the official documentation for this [here](https://network.nvidia.com/support/firmware/nic/).

In your host do:

1. Get the NVIDIA Firmware Tools (MFT) from here: https://network.nvidia.com/products/adapter-software/firmware-tools/

2. As root, start the mst tools with: `sudo mst start`

![cmd1](https://github.com/camilo-nunez/r86s-25g/blob/27848541d1a19d63c6cd65e9c8a103080711f426/imgs/35a7c2ba0b40c5bb/35a7c2ba0b40c5bb-1.png)

3. To verify the Part Number (OPN), the PSID, and the PCI device name, execute the command: `sudo mlxfwmanager`.

![cmd2](https://github.com/camilo-nunez/r86s-25g/blob/27848541d1a19d63c6cd65e9c8a103080711f426/imgs/35a7c2ba0b40c5bb/35a7c2ba0b40c5bb-2.png)

4. Once you have obtained the OPN and PSID, proceed to download the official firmware for your device from the following link: https://network.nvidia.com/support/firmware/connectx4lxen/.

![cmd3](https://github.com/camilo-nunez/r86s-25g/blob/1b3a5a17c6c8ad0920ae7d28878fcb13baf4ef1a/imgs/35a7c2ba0b40c5bb/35a7c2ba0b40c5bb-3.png)

5. After obtaining the PCI device name, proceed to burn the downloaded binary firmware using the following command: `sudo mlxburn –i <fw-ConnectX-4-downloaded>.bin –d /dev/mst/<PCI-device-name>`

![cmd4](https://github.com/camilo-nunez/r86s-25g/blob/1b3a5a17c6c8ad0920ae7d28878fcb13baf4ef1a/imgs/35a7c2ba0b40c5bb/35a7c2ba0b40c5bb-4.png)
> More info about the `mlxburn` command [here](https://docs.nvidia.com/networking/pages/viewpage.action?pageId=12013137).

# Change the CX341A interface card

1. Remove the four lateral screws.

![rem1](https://github.com/camilo-nunez/r86s-25g/blob/a66d5ce754d549cdc7b39aa216dc8aa76d94d59e/imgs/eff6bb60850e0922/eff6bb60850e0922-1.png)

![rem2](https://github.com/camilo-nunez/r86s-25g/blob/a66d5ce754d549cdc7b39aa216dc8aa76d94d59e/imgs/eff6bb60850e0922/eff6bb60850e0922-2.png)

2. Take your time, there's no need to hurry. Start by slowly opening the case. With a [Opening Tool](https://www.ifixit.com/products/ifixit-opening-tool) remove the PCI flex. And the power cable. DO NOT disconnect the battery cable.

![rem3](https://github.com/camilo-nunez/r86s-25g/blob/a66d5ce754d549cdc7b39aa216dc8aa76d94d59e/imgs/eff6bb60850e0922/eff6bb60850e0922-3.png)

3. Unscrew the four screws securing the card in place. Carefully take out the card from its slot after removing the screws.

![rem4](https://github.com/camilo-nunez/r86s-25g/blob/a66d5ce754d549cdc7b39aa216dc8aa76d94d59e/imgs/eff6bb60850e0922/eff6bb60850e0922-4.png)

4. Finally you will get this:

![rem5](https://github.com/camilo-nunez/r86s-25g/blob/a66d5ce754d549cdc7b39aa216dc8aa76d94d59e/imgs/eff6bb60850e0922/eff6bb60850e0922-5.png)

Upon comparing the cards, it becomes evident that they share identical size and form.

![rem6](https://github.com/camilo-nunez/r86s-25g/blob/a66d5ce754d549cdc7b39aa216dc8aa76d94d59e/imgs/eff6bb60850e0922/eff6bb60850e0922-6.png)

![rem7](https://github.com/camilo-nunez/r86s-25g/blob/a66d5ce754d549cdc7b39aa216dc8aa76d94d59e/imgs/eff6bb60850e0922/eff6bb60850e0922-7.png)

5. Lastly, add a thermal pad or thermal paste, then proceed to mount the card securely by fastening the four screws. Once the card is securely in place, carefully reconnect both the PCIe flex and the power cable.

![rem8](https://github.com/camilo-nunez/r86s-25g/blob/a66d5ce754d549cdc7b39aa216dc8aa76d94d59e/imgs/eff6bb60850e0922/eff6bb60850e0922-8.png)

![rem9](https://github.com/camilo-nunez/r86s-25g/blob/a66d5ce754d549cdc7b39aa216dc8aa76d94d59e/imgs/eff6bb60850e0922/eff6bb60850e0922-9.png)

# Testing
> Disclaimer: This is an unfinished section.

## Equipment

* 1x MCX455A-ECAT in my host
* 1x [1.5m (5ft) LC UPC to LC UPC Duplex OM4 Multimode](https://www.fs.com/products/88534.html)
* 1x [Mellanox MAM1Q00A-QSA28](https://www.fs.com/products/178073.html)
* 2x [Generic Compatible 25GBASE-SR SFP28 850nm 100m DOM Duplex LC MMF](https://www.fs.com/products/75296.html)

![equ1](https://github.com/camilo-nunez/r86s-25g/blob/4ba1ae08f3bc913693351f933520ca9f847c0fd6/imgs/440071a96d495743/440071a96d495743-1.png)

![equ2](https://github.com/camilo-nunez/r86s-25g/blob/4ba1ae08f3bc913693351f933520ca9f847c0fd6/imgs/440071a96d495743/440071a96d495743-3.png)

![equ3](https://github.com/camilo-nunez/r86s-25g/blob/4ba1ae08f3bc913693351f933520ca9f847c0fd6/imgs/440071a96d495743/440071a96d495743-4.png)


## Display the new card

Let confirm whether or not we can view the card, and provide the slot ID where the device is located.
> Here the slot device have the form `bus:device.function`. More info about the `lspci` command in the [man page](https://man7.org/linux/man-pages/man8/lspci.8.html).

```
root@r86s-01:~# lspci | grep -e 'Mellanox*'
04:00.0 Ethernet controller: Mellanox Technologies MT27710 Family [ConnectX-4 Lx]
04:00.1 Ethernet controller: Mellanox Technologies MT27710 Family [ConnectX-4 Lx]
```

The card is located in the bus ID `04`, with the device number `00`. Additionally, the two functions of the two interfaces have IDs `0` and `1`, respectively.

## About the PCIe lanes usage

It is important to note that the [Intel Celeron N5105](https://www.intel.com/content/www/us/en/products/sku/212328/intel-celeron-processor-n5105-4m-cache-up-to-2-90-ghz/specifications.html) processor is equipped with a maximum of 8 PCIe lanes. Let's investigate the distribution of the lanes around the devices. To do this, we will examine the system's topology using the `lstopo` command:

```
root@r86s-01:~# lstopo
Machine (7721MB total)
  Package L#0
    NUMANode L#0 (P#0 7721MB)
    L3 L#0 (4096KB) + L2 L#0 (1536KB)
      L1d L#0 (32KB) + L1i L#0 (32KB) + Core L#0 + PU L#0 (P#0)
      L1d L#1 (32KB) + L1i L#1 (32KB) + Core L#1 + PU L#1 (P#1)
      L1d L#2 (32KB) + L1i L#2 (32KB) + Core L#2 + PU L#2 (P#2)
      L1d L#3 (32KB) + L1i L#3 (32KB) + Core L#3 + PU L#3 (P#3)
  HostBridge
    PCI 00:02.0 (VGA)
    PCIBridge
      PCI 01:00.0 (Ethernet)
        Net "enp1s0"
    PCIBridge
      PCI 02:00.0 (Ethernet)
        Net "enp2s0"
    PCIBridge
      PCI 03:00.0 (Ethernet)
        Net "enp3s0"
    PCIBridge
      PCI 04:00.0 (Ethernet)
        Net "enp4s0f0np0"
        OpenFabrics "mlx5_0"
      PCI 04:00.1 (Ethernet)
        Net "enp4s0f1np1"
        OpenFabrics "mlx5_1"
    Block "mmcblk0"
    Block "mmcblk0boot0"
    Block "mmcblk0boot1"
  Misc(MemoryModule)
  Misc(MemoryModule)

```

Here, we can confirm that the distribution of the PCIe lanes is concentrated around buses `00`, `01`, `02`, `03`, and `04`. Among these lanes, the most crucial one is bus 04 as it houses our MCX4421A card. However, it's essential to consider the other lanes as well. Let's take a closer look at the PCIe configuration:

```
root@r86s-01:~# lspci -s 01:00.0 -vvv | grep Width
        LnkCap: Port #0, Speed 5GT/s, Width x1, ASPM L1, Exit Latency L1 <4us
        LnkSta: Speed 5GT/s, Width x1
root@r86s-01:~# lspci -s 02:00.0 -vvv | grep Width
        LnkCap: Port #0, Speed 5GT/s, Width x1, ASPM L1, Exit Latency L1 <4us
        LnkSta: Speed 5GT/s, Width x1
root@r86s-01:~# lspci -s 03:00.0 -vvv | grep Width
        LnkCap: Port #0, Speed 5GT/s, Width x1, ASPM L1, Exit Latency L1 <4us
        LnkSta: Speed 5GT/s, Width x1
```

Upon further investigation, we have confirmed that our [Intel Ethernet Controller I226-V](https://www.intel.com/content/www/us/en/products/sku/210599/intel-ethernet-controller-i226v/specifications.html) card operates using x1 lanes for each interface. This information aligns perfectly with the details provided in the Intel datasheet. Specifically, for each individual port, the Speed & Slot Width is specified as 5G, x1.

Now, let see what happen with the MCX4421A card:
```
root@r86s-01:~# lspci -s 04:00.0 -vvv | grep Width
        LnkCap: Port #0, Speed 8GT/s, Width x8, ASPM L1, Exit Latency L1 <4us
        LnkSta: Speed 8GT/s, Width x4 (downgraded)
root@r86s-01:~# lspci -s 04:00.1 -vvv | grep Width
        LnkCap: Port #0, Speed 8GT/s, Width x8, ASPM L1, Exit Latency L1 <4us
        LnkSta: Speed 8GT/s, Width x4 (downgraded)
```
The key and critical confirmation here is that the **MCX4421A is currently utilizing a width of x4 lanes**. This translates to a significant throughput of 3.938 GB/s, which is equivalent to 31.504 Gbps at the physical layer. However, it is crucial to note that we cannot fully utilize the complete data transfer rate offered by the 8x lanes default configuration of the card.

> If you want to know more about the performance of the PCIe lanes and the NICs, I highly recommend you the paper [Understanding PCIe performance for end host networking](https://doi.org/10.1145/3230543.3230560).

## Phase II

https://github.com/camilo-nunez/r86s-25g/assets/5784228/54bea83f-fca4-41eb-a876-00cfc127fe37
