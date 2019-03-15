<p align="right">
            Read this page in other languages:<a href="../../Japanese-master/platform-details.md">日本語</a>    <table style="width:100%"><table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://www.xilinx.com/content/dam/xilinx/imgs/press/media-kits/corporate/xilinx-logo.png" width="30%"/><h1>reVISION Getting Started Guide 2018.3 (UG1265)</h1>
</th>

  </tr>
  <tr>
    <td width="17%" align="center"><a href="../README.md">1. Introduction</a></td>
    <td width="16%" align="center"><a href="overview.md">2. Overview</a></td>
    <td width="17%" align="center"><a href="software-tools-system-requirements.md">3. Software Tools and System Requirements</a></td>
    <td width="17%" align="center"><a href="design-file-hierarchy.md">4. Design File Hierarchy</a></td>
</tr>
<tr>
    <td width="17%" align="center"><a href="operating-instructions.md">5. Installation and Operating Instructions</a></td>
    <td width="16%" align="center"><a href="tool-flow-tutorials.md">6. Tool Flow Tutorials</a></td>
    <td width="17%" align="center"><a href="run-application.md">7. Run the Application</a></td>
    <td width="17%" align="center">8. Platform Details</td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2"><a href="known-issues-limitations.md">9. Known Issues and Limitations</a></td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. Additional References</a></td>
</tr>
</table>

# 8. Platform Details

The below instructions refer to the `zcu102_rv_ss` platform. Follow the same instructions, replacing only the file name, for the `zcu104_rv_ss`, `zcu102_rv_min`, `zcu104_rv_min`, and `8-stream VCU + CNN` platforms.

## 8.1. Vivado Hardware Design

The Vivado® hardware design is packaged inside the DSA located in the `hw` folder of the platform (example: `zcu102_rv_ss/hw/zcu102_rv_ss.dsa`). The DSA also includes the `hpfm` file that describes the available AXI interfaces, clocks, resets, and interrupts. To open the hardware design in Vivado, run the following command from the Tcl console:

```
% open_dsa <platform>/hw/<platform>.dsa
```


## 8.2. PetaLinux BSP

The PetaLinux BSP is located at `<platform>/sw/petalinux_bsp`. The `.hdf` file exported from the corresponding Vivado project is available in the `project-spec/hw-description/` subfolder inside the PetaLinux BSP.

To configure and build the PetaLinux BSP, run the following commands:

```
% cd petalinux
% petalinux-create -t project -s zcu102-prod-rv-ss.bsp -n bsp
% petalinux-config --get-hw-description=../zcu102_base_trd/hw --oldconfig
% petalinux-build
```

**:pushpin: NOTE** The `tmp` directory might relocate to a different folder, especially if your PetaLinux project is located on an NFS mount. Check your PetaLinux configuration.

The generated output products are located inside the `images/linux/` subfolder. The relevant files that are packaged as part of the platform are listed below:
* ``bl31.elf``
* ``pmufw.elf``
* ``u-boot.elf``
* ``zynqmp_fsbl.elf``
* ``image.ub``

To generate the SDK/sysroot, run the following command:

```
% petalinux-build -s
```

The generated SDK installer will be located at `images/linux/sdk.sh`.

<hr/>

:arrow_forward:**Next Topic:**  [9. Known Issues and Limitations](known-issues-limitations.md)

:arrow_backward:**Previous Topic:**  [7. Run the Application](run-application.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018 Xilinx</sup></p>
