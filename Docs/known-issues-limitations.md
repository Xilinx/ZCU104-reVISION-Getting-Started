<p align="right">
            Read this page in other languages:<a href="../../Japanese-master/known-issues-limitations.md">日本語</a>    <table style="width:100%"><table style="width:100%">
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
    <td width="17%" align="center"><a href="platform-details.md">8. Platform Details</a></td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2">9. Known Issues and Limitations</td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. Additional References</a></td>
</tr>
</table>

# 9. Known Issues and Limitations

## 9.1 Known Issues

* The SDSoC™ environment accelerator code runs very slowly in pure software implementation when the Debug configuration is used.

  **Solution:** Set project build configurations to Release, which sets the SDSoC compiler to optimize most (-O3).

* The following error message is shown when compiling the SDx project:

  `WARNING: [DMAnalysis 83-4492] Unable to determine the memory attributes passed to _mapx_mat.data of function w1_xf_remap at /home/workspaces/ws_sv/stereo/src/stereo_sds.cpp:257, please use mem_attribute pragma to specify`

  **Solution:** The message is benign and can be ignored.

## 9.2 Limitations

* Do not connect a DisplayPort cable and an HDMI TX at the same time.
* Make sure the DisplayPort or HDMI TX cable is plugged in when you power on the board.
* DP-to-HDMI adapters are not supported. See [AR 67462](https://www.xilinx.com/support/answers/67462.html).
* An HDMI RX does _not_ support the following:
  * YUV 4:2:0 input.
  * HDCP encrypted input.
  * Hotplug or dynamic resolution changes while the application is running.
* The provided image signal processor (ISP) pipeline does not include any auto algorithms. The IMX274, gamma, and color correction controls have to be adjusted manually based on the surrounding environment.
* The `optical_flow` live I/O sample does not have a software implementation of the algorithm; only the hardware optimized implementation is available.
* The SDSoC environment does not support performance estimation for the `xfopenCV` library and in general for all the C++ templates (the part of performance estimation flow not yet supported is the estimate of software performance for function templates). When the HLS estimate of hardware resources pops up, the Ethernet P2P communication process between the SDSoC IDE and the board stalls indefinitely and no error message is displayed.
* The 8-stream VCU + CNN platform demo is tested with the provided input files only. With different input files (that is, with different encoding rates, file resolution/quality, and number of streams), the results might be different.
* A full understanding of the system is required for effective usage.

<hr/>

:arrow_forward:**Next Topic:**  [10. Additional References](additional-references.md)

:arrow_backward:**Previous Topic:**  [8. Platform Details](platform-details.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018 Xilinx</sup></p>
