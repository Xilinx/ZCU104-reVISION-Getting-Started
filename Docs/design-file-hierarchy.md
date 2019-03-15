<p align="right">
            Read this page in other languages:<a href="../../Japanese-master/design-file-hierarchy.md">日本語</a>    <table style="width:100%"><table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://www.xilinx.com/content/dam/xilinx/imgs/press/media-kits/corporate/xilinx-logo.png" width="30%"/><h1>reVISION Getting Started Guide 2018.3 (UG1265)</h1>
</th>

  </tr>
  <tr>
    <td width="17%" align="center"><a href="../README.md">1. Introduction</a></td>
    <td width="16%" align="center"><a href="overview.md">2. Overview</a></td>
    <td width="17%" align="center"><a href="software-tools-system-requirements.md">3. Software Tools and System Requirements</a></td>
    <td width="17%" align="center">4. Design File Hierarchy</td>
</tr>
<tr>
    <td width="17%" align="center"><a href="operating-instructions.md">5. Installation and Operating Instructions</a></td>
    <td width="16%" align="center"><a href="tool-flow-tutorials.md">6. Tool Flow Tutorials</a></td>
    <td width="17%" align="center"><a href="run-application.md">7. Run the Application</a></td>
    <td width="17%" align="center"><a href="platform-details.md">8. Platform Details</a></td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2"><a href="known-issues-limitations.md">9. Known Issues and Limitations</a></td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. Additional References</a></td>
</tr>
</table>

# 4. Design File Hierarchy

The Zynq® UltraScale+™ MPSoC reVISION platform .zip file is released with the binary and source files required to create projects in the SDx™ environments and build the sample applications. The sample applications are built as GStreamer plugins with test designs to exercise them.


The samples provided with the single-sensor platform include five file I/O examples and four live I/O examples. The file I/O examples read an input image file and produce an output image file, whereas the live I/O examples take live video input from a video source and output live video on a display. The single-sensor reVISION platform contains the following components:

* `zcu102_rv_ss` SDSoC platform
  * `hw` contains the .dsa file describing the hardware platform.
  * `samples` contains the sample app code. Each sample directory has a .json file describing the build process. These are the SDx sample apps that appear in the Template dialog when creating a new project using the reVISION platform.
    * `file_IO` projects are self-contained.
    * `live_IO` projects are more complex, and are built in several steps. See <a href="run-application.md">Run the Application</a>.
  * `sw` contains software; bootloaders and other code, and support files for the processors on the ZCU10x target board.
* `petalinux` contains a PetaLinux BSP with device tree information, hardware description files, and other system setup files. An advanced user has the option of creating their own platform.
* `sd_card` contains pre-built SD card images that enable you to run the live I/O example applications on the ZCU10x board.
* `workspaces` contains a workspace directory structure you can use to build the `live_IO` samples. See <a href="run-application.md">Run the Application</a>.

```
zcu102-rv-ss-2018-3
├── IMPORTANT_NOTICE_CONCERNING_THIRD_PARTY_CONTENT.txt
├── petalinux
│   ├── sdk.sh
│   └── zcu102-prod-rv-ss.bsp
├── README.txt
├── sd_card
│   ├── filter2d
│   ├── optical_flow
│   ├── stereo
│   └── triple
├── workspaces
│   ├── ws_f2d
│   │   ├── gst
│   │   │   ├── apps
│   │   │   └── plugins
│   │   └── scripts
│   ├── ws_of
│   │   ├── gst
│   │   │   ├── apps
│   │   │   └── plugins
│   │   └── scripts
│   ├── ws_sv
│   │   ├── gst
│   │   │   ├── apps
│   │   │   └── plugins
│   │   └── scripts
│   └── ws_triple
│       ├── gst
│       └── scripts
└── zcu102_rv_ss
    ├── hw
    │   └── zcu102_rv_ss.dsa
    ├── samples
    │   ├── file_IO
    │   │   ├── bilateral_fileio
    │   │   ├── harris_fileio
    │   │   ├── opticalflow_fileio
    │   │   ├── steoreolbm_fileio
    │   │   └── warptransform_fileio
    │   └── live_IO
    │       ├── filter2d
    │       ├── optical_flow
    │       ├── stereo
    │       └── triple
    ├── sw
    │   ├── a53_linux
    │   │   ├── a53_linux
    │   │   └── boot
    │   ├── prebuilt
    │   └── zcu102_rv_ss.spfm
    └── zcu102_rv_ss.xpfm
```

The MIN reVISION platform contains the following components:

* `zcu102_rv_min` SDSoC platform
  * `hw` contains the .dsa file describing the hardware platform.
  * `sw` contains software; bootloaders and other code, and support files for the processors on the ZCU10x target board.
* `petalinux` contains a PetaLinux BSP with device tree information, hardware description files, and other system setup files. An advanced user has the option of creating their own platform.


```
zcu102-rv-min-2018-3
├── IMPORTANT_NOTICE_CONCERNING_THIRD_PARTY_CONTENT.txt
├── README.txt
└── zcu102_rv_min
    ├── hw
    │   └── zcu102_rv_min.dsa
    ├── petalinux
    │   ├── sdk.sh
    │   └── zcu102-prod-rv-min.bsp
    ├── samples
    ├── sw
    │   ├── a53_linux
    │   │   ├── a53_linux
    │   │   └── boot
    │   ├── prebuilt
    │   └── zcu102_rv_min.spfm
    └── zcu102_rv_min.xpfm
```

The 8-stream VCU + CNN reVISION platform contains the following components:
* `zcu104` SDSoC platform
  * `hw` contains the .dsa file describing the hardware platform.
  * `sw` contains software; bootloaders and other code, and support files for the processors on the ZCU104 target board.
* `petalinux` contains a PetaLinux BSP with device tree information, hardware description files, and other system setup files. An advanced user has the option of creating their own platform.
* `SDcard` contains pre-built SD card images that enable you to run the "8-stream VCU + CNN" demo.
* `scripts` contains test scripts for running the "8-stream VCU + CNN" demo with one copy of these scripts are in `SDcard` too.

```
zcu104-rv-vcu-ml-2018-3
├── IMPORTANT_NOTICE_CONCERNING_THIRD_PARTY_CONTENT.txt
├── petalinux
│   ├── sdk.sh
│   └── zcu104_vcu_ml.bsp
├── README.txt
├── scripts
│   ├── demo_8_streams_1080.sh
│   └── demo_8_streams_4k.sh
├── SDcard
└── zcu104
    ├── hw
    │   └── zcu104.dsa
    ├── samples
    ├── sw
    │   ├── a53_linux
    │   │   ├── a53_linux
    │   │   └── boot
    │   ├── prebuilt
    │   └── zcu104.spfm
    └── zcu104.xpfm
```
<hr/>

:arrow_forward:**Next Topic:**  [5. Installation and Operating Instructions](operating-instructions.md)

:arrow_backward:**Previous Topic:**  [3. Software Tools and System Requirements](software-tools-system-requirements.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018 Xilinx</sup></p>
