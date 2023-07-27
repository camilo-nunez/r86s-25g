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

In you host do:

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


## Phase I
```
root@r86s-01:~# lspci
00:00.0 Host bridge: Intel Corporation Device 4e24
00:02.0 VGA compatible controller: Intel Corporation JasperLake [UHD Graphics] (rev 01)
00:14.0 USB controller: Intel Corporation Device 4ded (rev 01)
00:14.2 RAM memory: Intel Corporation Device 4def (rev 01)
00:16.0 Communication controller: Intel Corporation Management Engine Interface (rev 01)
00:1a.0 SD Host controller: Intel Corporation Device 4dc4 (rev 01)
00:1c.0 PCI bridge: Intel Corporation Device 4db8 (rev 01)
00:1c.1 PCI bridge: Intel Corporation Device 4db9 (rev 01)
00:1c.2 PCI bridge: Intel Corporation Device 4dba (rev 01)
00:1c.4 PCI bridge: Intel Corporation Device 4dbc (rev 01)
00:1f.0 ISA bridge: Intel Corporation Device 4d87 (rev 01)
00:1f.3 Audio device: Intel Corporation Jasper Lake HD Audio (rev 01)
00:1f.4 SMBus: Intel Corporation Jasper Lake SMBus (rev 01)
00:1f.5 Serial bus controller: Intel Corporation Jasper Lake SPI Controller (rev 01)
01:00.0 Ethernet controller: Intel Corporation Ethernet Controller I226-V (rev 04)
02:00.0 Ethernet controller: Intel Corporation Ethernet Controller I226-V (rev 04)
03:00.0 Ethernet controller: Intel Corporation Ethernet Controller I226-V (rev 04)
04:00.0 Ethernet controller: Mellanox Technologies MT27710 Family [ConnectX-4 Lx]
04:00.1 Ethernet controller: Mellanox Technologies MT27710 Family [ConnectX-4 Lx]
```

```
root@r86s-01:~# lspci -s 04:00.0 -vv
04:00.0 Ethernet controller: Mellanox Technologies MT27710 Family [ConnectX-4 Lx]
    Subsystem: Mellanox Technologies MCX4421A-ACQN ConnectX-4 Lx EN OCP,2x25G
    Control: I/O- Mem+ BusMaster+ SpecCycle- MemWINV- VGASnoop- ParErr- Stepping- SERR- FastB2B- DisINTx+
    Status: Cap+ 66MHz- UDF- FastB2B- ParErr- DEVSEL=fast >TAbort- <TAbort- <MAbort- >SERR- <PERR- INTx-
    Latency: 0, Cache Line Size: 64 bytes
    Interrupt: pin A routed to IRQ 29
    IOMMU group: 13
    Region 0: Memory at 4010000000 (64-bit, prefetchable) [size=32M]
    Expansion ROM at 7fd00000 [disabled] [size=1M]
    Capabilities: [60] Express (v2) Endpoint, MSI 00
        DevCap: MaxPayload 512 bytes, PhantFunc 0, Latency L0s unlimited, L1 unlimited
            ExtTag+ AttnBtn- AttnInd- PwrInd- RBE+ FLReset+ SlotPowerLimit 25W
        DevCtl: CorrErr+ NonFatalErr+ FatalErr+ UnsupReq+
            RlxdOrd+ ExtTag+ PhantFunc- AuxPwr- NoSnoop+ FLReset-
            MaxPayload 256 bytes, MaxReadReq 512 bytes
        DevSta: CorrErr+ NonFatalErr- FatalErr- UnsupReq+ AuxPwr- TransPend-
        LnkCap: Port #0, Speed 8GT/s, Width x8, ASPM L1, Exit Latency L1 <4us
            ClockPM- Surprise- LLActRep- BwNot- ASPMOptComp+
        LnkCtl: ASPM L1 Enabled; RCB 64 bytes, Disabled- CommClk+
            ExtSynch- ClockPM- AutWidDis- BWInt- AutBWInt-
        LnkSta: Speed 8GT/s, Width x4 (downgraded)
            TrErr- Train- SlotClk+ DLActive- BWMgmt- ABWMgmt-
        DevCap2: Completion Timeout: Range ABC, TimeoutDis+ NROPrPrP- LTR-
             10BitTagComp- 10BitTagReq- OBFF Not Supported, ExtFmt- EETLPPrefix-
             EmergencyPowerReduction Not Supported, EmergencyPowerReductionInit-
             FRS- TPHComp- ExtTPHComp-
             AtomicOpsCap: 32bit- 64bit- 128bitCAS-
        DevCtl2: Completion Timeout: 50us to 50ms, TimeoutDis- LTR- 10BitTagReq- OBFF Disabled,
             AtomicOpsCtl: ReqEn-
        LnkCap2: Supported Link Speeds: 2.5-8GT/s, Crosslink- Retimer- 2Retimers- DRS-
        LnkCtl2: Target Link Speed: 8GT/s, EnterCompliance- SpeedDis-
             Transmit Margin: Normal Operating Range, EnterModifiedCompliance- ComplianceSOS-
             Compliance Preset/De-emphasis: -6dB de-emphasis, 0dB preshoot
        LnkSta2: Current De-emphasis Level: -6dB, EqualizationComplete+ EqualizationPhase1+
             EqualizationPhase2+ EqualizationPhase3+ LinkEqualizationRequest-
             Retimer- 2Retimers- CrosslinkRes: unsupported
    Capabilities: [48] Vital Product Data
        Product Name: CX4421A- ConnectX-4 LX SFP28
        Read-only fields:
            [PN] Part number: MCX4421A-ACQN        
            [EC] Engineering changes: AC
            [SN] Serial number: MT2025K30970            
            [V0] Vendor specific: PCIeGen3 x8     
            [RV] Reserved: checksum good, 0 byte(s) reserved
        End
    Capabilities: [9c] MSI-X: Enable+ Count=64 Masked-
        Vector table: BAR=0 offset=00002000
        PBA: BAR=0 offset=00003000
    Capabilities: [c0] Vendor Specific Information: Len=18 <?>
    Capabilities: [40] Power Management version 3
        Flags: PMEClk- DSI- D1- D2- AuxCurrent=375mA PME(D0-,D1-,D2-,D3hot-,D3cold+)
        Status: D0 NoSoftRst+ PME-Enable- DSel=0 DScale=0 PME-
    Capabilities: [100 v1] Advanced Error Reporting
        UESta:  DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
        UEMsk:  DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
        UESvrt: DLP+ SDES- TLP- FCP+ CmpltTO- CmpltAbrt- UnxCmplt- RxOF+ MalfTLP+ ECRC- UnsupReq- ACSViol-
        CESta:  RxErr- BadTLP- BadDLLP- Rollover- Timeout- AdvNonFatalErr-
        CEMsk:  RxErr- BadTLP- BadDLLP- Rollover- Timeout- AdvNonFatalErr+
        AERCap: First Error Pointer: 04, ECRCGenCap+ ECRCGenEn- ECRCChkCap+ ECRCChkEn-
            MultHdrRecCap- MultHdrRecEn- TLPPfxPres- HdrLogCap-
        HeaderLog: 00000000 00000000 00000000 00000000
    Capabilities: [150 v1] Alternative Routing-ID Interpretation (ARI)
        ARICap: MFVC- ACS-, Next Function: 1
        ARICtl: MFVC- ACS-, Function Group: 0
    Capabilities: [180 v1] Single Root I/O Virtualization (SR-IOV)
        IOVCap: Migration- 10BitTagReq- Interrupt Message Number: 000
        IOVCtl: Enable- Migration- Interrupt- MSE- ARIHierarchy+ 10BitTagReq-
        IOVSta: Migration-
        Initial VFs: 8, Total VFs: 8, Number of VFs: 0, Function Dependency Link: 00
        VF offset: 2, stride: 1, Device ID: 1016
        Supported Page Size: 000007ff, System Page Size: 00000001
        Region 0: Memory at 0000004014000000 (64-bit, prefetchable)
        VF Migration: offset: 00000000, BIR: 0
    Capabilities: [1c0 v1] Secondary PCI Express
        LnkCtl3: LnkEquIntrruptEn- PerformEqu-
        LaneErrStat: 0
    Capabilities: [230 v1] Access Control Services
        ACSCap: SrcValid- TransBlk- ReqRedir- CmpltRedir- UpstreamFwd- EgressCtrl- DirectTrans-
        ACSCtl: SrcValid- TransBlk- ReqRedir- CmpltRedir- UpstreamFwd- EgressCtrl- DirectTrans-
    Kernel driver in use: mlx5_core
    Kernel modules: mlx5_core
```


```
root@r86s-01:~# lspci -s 04:00.1 -vv
04:00.1 Ethernet controller: Mellanox Technologies MT27710 Family [ConnectX-4 Lx]
    Subsystem: Mellanox Technologies MCX4421A-ACQN ConnectX-4 Lx EN OCP,2x25G
    Control: I/O- Mem+ BusMaster+ SpecCycle- MemWINV- VGASnoop- ParErr- Stepping- SERR- FastB2B- DisINTx+
    Status: Cap+ 66MHz- UDF- FastB2B- ParErr- DEVSEL=fast >TAbort- <TAbort- <MAbort- >SERR- <PERR- INTx-
    Latency: 0, Cache Line Size: 64 bytes
    Interrupt: pin B routed to IRQ 19
    IOMMU group: 14
    Region 0: Memory at 4012000000 (64-bit, prefetchable) [size=32M]
    Expansion ROM at 7fc00000 [disabled] [size=1M]
    Capabilities: [60] Express (v2) Endpoint, MSI 00
        DevCap: MaxPayload 512 bytes, PhantFunc 0, Latency L0s unlimited, L1 unlimited
            ExtTag+ AttnBtn- AttnInd- PwrInd- RBE+ FLReset+ SlotPowerLimit 25W
        DevCtl: CorrErr+ NonFatalErr+ FatalErr+ UnsupReq+
            RlxdOrd+ ExtTag+ PhantFunc- AuxPwr- NoSnoop+ FLReset-
            MaxPayload 256 bytes, MaxReadReq 512 bytes
        DevSta: CorrErr+ NonFatalErr- FatalErr- UnsupReq+ AuxPwr- TransPend-
        LnkCap: Port #0, Speed 8GT/s, Width x8, ASPM L1, Exit Latency L1 <4us
            ClockPM- Surprise- LLActRep- BwNot- ASPMOptComp+
        LnkCtl: ASPM L1 Enabled; RCB 64 bytes, Disabled- CommClk+
            ExtSynch- ClockPM- AutWidDis- BWInt- AutBWInt-
        LnkSta: Speed 8GT/s, Width x4 (downgraded)
            TrErr- Train- SlotClk+ DLActive- BWMgmt- ABWMgmt-
        DevCap2: Completion Timeout: Range ABC, TimeoutDis+ NROPrPrP- LTR-
             10BitTagComp- 10BitTagReq- OBFF Not Supported, ExtFmt- EETLPPrefix-
             EmergencyPowerReduction Not Supported, EmergencyPowerReductionInit-
             FRS- TPHComp- ExtTPHComp-
             AtomicOpsCap: 32bit- 64bit- 128bitCAS-
        DevCtl2: Completion Timeout: 50us to 50ms, TimeoutDis- LTR- 10BitTagReq- OBFF Disabled,
             AtomicOpsCtl: ReqEn-
        LnkSta2: Current De-emphasis Level: -6dB, EqualizationComplete- EqualizationPhase1-
             EqualizationPhase2- EqualizationPhase3- LinkEqualizationRequest-
             Retimer- 2Retimers- CrosslinkRes: unsupported
    Capabilities: [48] Vital Product Data
        Product Name: CX4421A- ConnectX-4 LX SFP28
        Read-only fields:
            [PN] Part number: MCX4421A-ACQN        
            [EC] Engineering changes: AC
            [SN] Serial number: MT2025K30970            
            [V0] Vendor specific: PCIeGen3 x8     
            [RV] Reserved: checksum good, 0 byte(s) reserved
        End
    Capabilities: [9c] MSI-X: Enable+ Count=64 Masked-
        Vector table: BAR=0 offset=00002000
        PBA: BAR=0 offset=00003000
    Capabilities: [c0] Vendor Specific Information: Len=18 <?>
    Capabilities: [40] Power Management version 3
        Flags: PMEClk- DSI- D1- D2- AuxCurrent=375mA PME(D0-,D1-,D2-,D3hot-,D3cold+)
        Status: D0 NoSoftRst+ PME-Enable- DSel=0 DScale=0 PME-
    Capabilities: [100 v1] Advanced Error Reporting
        UESta:  DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
        UEMsk:  DLP- SDES- TLP- FCP- CmpltTO- CmpltAbrt- UnxCmplt- RxOF- MalfTLP- ECRC- UnsupReq- ACSViol-
        UESvrt: DLP+ SDES- TLP- FCP+ CmpltTO- CmpltAbrt- UnxCmplt- RxOF+ MalfTLP+ ECRC- UnsupReq- ACSViol-
        CESta:  RxErr- BadTLP- BadDLLP- Rollover- Timeout- AdvNonFatalErr-
        CEMsk:  RxErr- BadTLP- BadDLLP- Rollover- Timeout- AdvNonFatalErr+
        AERCap: First Error Pointer: 04, ECRCGenCap+ ECRCGenEn- ECRCChkCap+ ECRCChkEn-
            MultHdrRecCap- MultHdrRecEn- TLPPfxPres- HdrLogCap-
        HeaderLog: 00000000 00000000 00000000 00000000
    Capabilities: [150 v1] Alternative Routing-ID Interpretation (ARI)
        ARICap: MFVC- ACS-, Next Function: 0
        ARICtl: MFVC- ACS-, Function Group: 0
    Capabilities: [180 v1] Single Root I/O Virtualization (SR-IOV)
        IOVCap: Migration- 10BitTagReq- Interrupt Message Number: 000
        IOVCtl: Enable- Migration- Interrupt- MSE- ARIHierarchy- 10BitTagReq-
        IOVSta: Migration-
        Initial VFs: 8, Total VFs: 8, Number of VFs: 0, Function Dependency Link: 01
        VF offset: 9, stride: 1, Device ID: 1016
        Supported Page Size: 000007ff, System Page Size: 00000001
        Region 0: Memory at 0000004014800000 (64-bit, prefetchable)
        VF Migration: offset: 00000000, BIR: 0
    Capabilities: [230 v1] Access Control Services
        ACSCap: SrcValid- TransBlk- ReqRedir- CmpltRedir- UpstreamFwd- EgressCtrl- DirectTrans-
        ACSCtl: SrcValid- TransBlk- ReqRedir- CmpltRedir- UpstreamFwd- EgressCtrl- DirectTrans-
    Kernel driver in use: mlx5_core
    Kernel modules: mlx5_core

```

## Phase II

https://github.com/camilo-nunez/r86s-25g/assets/5784228/54bea83f-fca4-41eb-a876-00cfc127fe37
