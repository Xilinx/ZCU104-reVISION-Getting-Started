2018.3<p align="right">
            Read this page in other languages:<a href="../../Japanese-master/run-application.md">日本語</a>    <table style="width:100%"><table style="width:100%">
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
    <td width="17%" align="center">7. Run the Application</td>
    <td width="17%" align="center"><a href="platform-details.md">8. Platform Details</a></td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2"><a href="known-issues-limitations.md">9. Known Issues and Limitations</a></td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. Additional References</a></td>
</tr>
</table>

# 7. Run the Application

To use the GStreamer plugins, a video pipeline that includes them must be set up and launched. The command line utility `gst-launch-1.0` can be used to do this. Use your laptop connected to the target board over a serial terminal emulator, interacting with the system using a standard Linux console session  (see [Build the Live I/O Optical Flow Sample Application](tool-flow-tutorials.md#611-build-the-live_io-optical-flow-sample-application)). You can construct video pipeline graphs consisting of one or more sources, zero, one or more accelerators, and one sink. GStreamer is responsible for initializing the capture, memory-to-memory, and display pipelines as well as managing the video buffer flow through the pipeline stages.

The ``gst-launch`` utility is really a debugging tool. The other way to set up and launch your plugins is with a compiled application that sets up and runs the pipeline using API calls to the GStreamer libraries. The sample code is provided for test apps that do this. See the `./gst/apps/<name> `folder in the single-sensor platform for each of the live I/O samples.


## 7.1. Run the Live I/O Sample Applications (Single-Sensor Platform)

The bottom project containing the hardware accelerated code is an SDx™ environment project (for example, `./ws_f2d/filter2d`). When it completes, it creates an SD card image with files you need to copy to the SD card you'll use on the target board. All the libraries and plugins must be copied to the ``sd_card`` root directory. The following sections list the exact files for each case.

:pushpin: **IMPORTANT**: For the stereo and triple case, you also need the camera configuration file on the SD card (see [Single-Sensor Platform Stereo Demo: Special Considerations](#74-single-sensor-platform-stereo-demo-special-considerations)).

### 7.1.1. Files for filter2d

After building the bottom library, your ``sd_card`` directory will contain the following files:
* `./ws_f2d/filter2d/Release/sd_card/image.ub`
* `./ws_f2d/filter2d/Release/sd_card/BOOT.BIN`
* `./ws_f2d/filter2d/Release/sd_card/libfilter2d.so`

The top projects generate the shared library and the demo app.
* `./ws_f2d/gst/plugins/filter2d/Debug/libgstsdxfilter2d.so`
* `./ws_f2d/gst/apps/filter2d/Debug/gstdemo.`

>**:information_source: TIP** Copy all images  directly into the root folder of the SD card.

### 7.1.2. Files for opticalflow

After building the bottom library, your ``sd_card`` directory will contain the following files:
* `./ws_of/opticalflow/Release/sd_card/image.ub`
* `./ws_of/opticalflow/Release/sd_card/BOOT.BIN`
* `./ws_of/opticalflow/Release/sd_card/libopticalflow.so`

The top projects generate the shared library and the demo app.
* `./ws_of/gst/plugins/optical_flow/Debug/libgstsdxopticalflow.so`
* `./ws_of/gst/apps/optical_flow/Debug/gstdemo.`

>**:information_source: TIP** Copy all images  directly into the root folder of the SD card.

### 7.1.3. Files for stereo

After building the bottom library, your ``sd_card`` directory will contain the following files:
* `./ws_sv/stereo/Release/sd_card/image.ub`
* `./ws_sv/stereo/Release/sd_card/BOOT.BIN`
* `./ws_sv/stereo/Release/sd_card/libstereo.so`

The top projects generate the shared library and the demo app.
* `./ws_sv/gst/plugins/stereo/Debug/libgstsdxstereo.so`
* `./ws_sv/gst/apps/stereo/Debug/gstdemo.`

>**:information_source: TIP** Copy all images  directly into the root folder of the SD card.

### 7.1.4. Files for triple

After building the bottom library, your ``sd_card`` directory will contain the following files:
* `./ws_triple/triple/Release/sd_card/image.ub`
* `./ws_triple/triple/Release/sd_card/BOOT.BIN`
* `./ws_triple/triple/Release/sd_card/libtriple.so`

The top projects generate the shared library and the demo app.
* `./ws_triple/gst/plugins/filter2d/Debug/libgstsdxfilter2d.so`
* `./ws_triple/gst/plugins/optical_flow/Debug/libgstsdxopticalflow.so`
* `./ws_triple/gst/plugins/stereo/Debug/libgstsdxstereo.so`
* `./ws_triple/gst/apps/triple/Debug/gstdemo.`

>**:information_source: TIP** Copy all images  directly into the root folder of the SD card.

### 7.1.5. Instructions

1. Insert the SD card in the SD card slot on your target board.
2. Power on the board; make sure the large INIT_B LED and the DONE LED next to it go green after a few seconds.
3. Control the system from your computer: start a terminal session using TeraTerm, PuTTY or similar (see [Build the Live I/O Optical Flow Sample Application](tool-flow-tutorials.md#611-build-the-live_io-optical-flow-sample-application)). With the USB-UART cable connected and the board powered up, you can locate the COM port that is responsive. You'll see several pages of Linux bootstrap and debug messages scroll by, finishing at the Linux command line prompt.
4. Using ``cd``, go to the `/media/card` directory. This directory contains all the files you copied to your SD card.
```
# cd /media/card

```
5. Copy the shared libraries where they need to go; see the examples for each case below.

**:pushpin: NOTE:** The following steps are not required if you are using reVISION BSP/images, because the ``PATH`` environment variable is appended to ``/media/card/``.

  * filter2d case:

	```
	# cp libfilter2d.so /usr/lib
	# cp libgstsdxfilter2d.so /usr/lib/gstreamer-1.0

	```
  * opticalflow case:

	```
	# cp libopticalflow.so /usr/lib
	# cp libgstsdxopticalflow.so /usr/lib/gstreamer-1.0

	```

  * stereo case:
	```

	# cp libstereo.so /usr/lib
	# cp libgstsdxstereo.so /usr/lib/gstreamer-1.0

	```

  * triple case:
	```

	# cp libtriple.so /usr/lib
	# cp libgstsdxfilter2d.so /usr/lib/gstreamer-1.0
	# cp libgstsdxopticalflow.so /usr/lib/gstreamer-1.0
	# cp libgstsdxstereo.so /usr/lib/gstreamer-1.0

	```


### 7.1.6 Gstreamer Application

To create and run the gstreamer pipeline, you can either use the ``gst`` demo applications that are compiled from source, or you can use the prebuilt `gst-launch` utility. Use your compiled demo program:
```

# ./gstdemo

```

  * All the demo programs use the HDMI output, through the mixer.
  * The filter2d demo uses the HDMI input.
  * The opticalflow demo uses the MIPI input.
  * The stereo demo uses the USB ZED stereo camera input.
  * The triple demo uses all of the above.

The following code example is a ``gst-launch`` command to run the ``filter2d`` pipeline, from MIPI, 1920x1080, YUY2, to the HDMI output through mixer plane 29.
```

gst-launch-1.0 \
    xlnxvideosrc src-type="mipi" ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxfilter2d filter-preset=4 filter-mode=1 ! queue ! \
    xlnxvideosink sink-type="hdmi" plane-id=29 sync=false fullscreen-overlay=true

```

The following code example is a ``gst-launch`` command to run the ``opticalflow`` pipeline, from HDMI, 1920x1080, YUY2, to the HDMI output through mixer plane 29.
```

gst-launch-1.0 \
    xlnxvideosrc src-type="hdmi" ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxopticalflow filter-mode=1 ! queue ! \
    xlnxvideosink sink-type="hdmi" sync=false fullscreen-overlay=true

```


The following code example is a ``gst-launch`` command to run the stereo pipeline, from USB, 3840x1080 side-by-side input, YUY2, 1920x1080 output to HDMI through mixer plane 29. You must substitute your camera serial number for the ``config-filename property``. See the section below on [Single-Sensor Platform Stereo Demo: Special Considerations](#74-single-sensor-platform-stereo-demo-special-considerations).
```

gst-launch-1.0 \
    xlnxvideosrc src-type="usbcam"  ! \
    "video/x-raw, width=3840, height=1080, format=YUY2" ! \
    sdxstereo filter-mode=1 config-filename=/media/card/SN12263.conf ! queue ! \
    xlnxvideosink sink-type="hdmi" plane-id=29 sync=false fullscreen-overlay=true

```


The following example shows an alternative way to run ``filter2d`` with frames-per-second display enabled. Notice the output pipe stage is ``fpsdisplaysink``, and that the previously used ``xlnxvideosink....`` string is a property of ``fpsdisplaysink`` called ``video-sink``.
```

gst-launch-1.0 \
    xlnxvideosrc src-type="mipi" ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxfilter2d filter-preset=4 filter-mode=1 ! queue ! \
    fpsdisplaysink video-sink="xlnxvideosink sink-type=hdmi plane-id=29 fullscreen-overlay=true" sync=false text-overlay=false -v

```
## 7.2. Run the Traffic Detect Sample Applications (8-Stream VCU + CNN Platform)

The C-callable project containing the hardware accelerated code is an SDx™ environment project (for example, `./ws_dpu/dpu130_4096`). When it completes, it creates an SD card image with files you need to copy to the SD card you'll use on the target board. All the libraries and plugins must be copied to the ``sd_card`` root directory. The following sections list the exact files for each case.

### 7.2.1. Files for Traffic Detect

After building the C-callable library, your ``sd_card`` directory will contain the following files:
* `./ws_dpu/dpucore130_4096/Debug/sd_card/image.ub`
* `./ws_dpu/dpucore130_4096/Debug/sd_card/uENV.txt`
* `./ws_dpu/dpucore130_4096/Debug/sd_card/BOOT.BIN`
* `./ws_dpu/dpucore130_4096/Debug/sd_card/libdpucore130_4096.so`

  **:pushpin: NOTE:**  When using ``libdpucore130_4096.so``, rename it to ``libdpucore.so`` or create a soft link that points to it.

The ``gstsdxtrafficdetect`` projects generate the shared library.
* `./ws_dpu/gstsdxtrafficdetect/Debug/libgstsdxtrafficdetect.so`

Add the prebuilt libraries:
* `./run_dpu/lib/libn2cube.so`
* `./run_dpu/lib/libdputils.so`
* `./run_dpu/libmodel/libdpumodelssd.so`

>**:information_source: TIP** Copy all images  directly into the root folder of the SD card.

### 7.2.2. Instructions

1. Insert the SD card in the SD card slot on your target board.
2. Power on the board; make sure the large INIT_B LED and the DONE LED next to it go green after a few seconds.
3. Control the system from your computer: start a terminal session using TeraTerm, PuTTY or similar (see [Build the Live I/O Optical Flow Sample Application](tool-flow-tutorials.md#611-build-the-live_io-optical-flow-sample-application)). With the USB-UART cable connected and the board powered up, you can locate the COM port that is responsive. You'll see several pages of Linux bootstrap and debug messages scroll by, finishing at the Linux command line prompt.
4. Using ``cd``, go to the `/media/card` directory. This directory contains all the files you copied to your SD card.
```
# cd /media/card

```
5. Copy the shared libraries where they need to go.

**:pushpin: NOTE:** The following steps are not required if you are using reVISION BSP/images, because the ``PATH`` environment variable is appended to ``/media/card/``.

>
```
# cp libdpucore.so /usr/lib
# cp libn2cube.so /usr/lib
# cp libdputils.so /usr/lib
# cp libdpumodelssd.so /usr/lib
# cp libgstsdxtrafficdetect.so /usr/lib/gstreamer-1.0

```
### 7.2.3. Examples

The following code example is a ``gst-launch`` command to run the single-stream VCU + CNN  pipeline, with input from an H264 encoded file already in the ``demo_input`` folder, and HDMI output through mixer plane 29.
```

  gst-launch-1.0 multifilesrc location=demo_inputs/file_%02d.dmp loop=true ! h264parse !          omxh264dec internal-entropy-buffers=3 ! xlnxscale need-tdm=true !  \
  video/x-raw, width=480, height=360, format=BGR !  \
          sdxtrafficdetect ! queue ! \
          fpsdisplaysink video-sink="kmssink plane-id=29 bus-id="a0070000.v_mix" render-rectangle=\"<0,0,480,360>\"" text-overlay=false sync=false -v


```

For the 8-stream platform, eight similar instances could be run with a different mixer ``plane-id`` numbered from 29 to 36. Check `demo_8_streams_4k.sh` for the complete pipeline. If you have a 1600x1200 resolution monitor, run the script as shown in the following example:
```
  source demo_8_streams_4k.sh
```
If your monitor does not support 1600x1200, run the script as shown in the following example:
```
source demo_8_streams_1080.sh
```

The ``demo_input`` folder contains traffic video files with H264 encoding. These files are broken into small chunks by Gstreamer plugin ``multifilesink`` to keep usage of DDR to a minimum.

```
gst-launch-1.0 filesrc location=<input_largefile.264> ! multifilesink location="file%d.dmp" next-file=4 max-file-size=<keep based on current input fragmented file>
```

The above fragmentation is not really necessary; you can also try to complete the file with ``filesrc``, as shown in the example below:
```

  gst-launch-1.0 filesrc location=<testfile.h264> ! h264parse ! omxh264dec internal-entropy-buffers=3 ! xlnxscale need-tdm=true !  \
  video/x-raw, width=480, height=360, format=BGR !  \
          sdxtrafficdetect ! queue ! \
          fpsdisplaysink video-sink="kmssink plane-id=29 bus-id="a0070000.v_mix" render-rectangle=\"<0,0,480,360>\"" text-overlay=false sync=false -v
```


## 7.3. Gstreamer Elements

These pipelines use the elements ``xlnxvideosrc``, ``queue``, ``xlnxvideosink``, and ``sdxfilter2d`` (or ``sdxopticalflow``, or ``sdxstereo``). You can display properties and other information about any of these elements using the ``gst-inspect-1.0`` Gstreamer utility.

### 7.3.1. xlnxvideosrc

```

# gst-inspect-1.0 xlnxvideosrc

```

  * ``src-type`` property
    - (-1): none: Video Source NONE
    - (0): vivid: Virtual Video Device
    - (1): mipi: MIPI CSI2 RX
    - (2): hdmi: HDMI Input
    - (3): usbcam: USB Webcam
    - (4): tpg: Test Pattern Generator
    - (5): mipi_quad_vc0: MIPI Quad Virtual Channel 0
    - (6): mipi_quad_vc1: MIPI Quad Virtual Channel 1
    - (7): mipi_quad_vc2: MIPI Quad Virtual Channel 2
    - (8): mipi_quad_vc3: MIPI Quad Virtual Channel 3

  * Children:
    - ``v4l2src0``



### 7.3.2. queue

This is not strictly necessary, but using it delivers better performance (that is, the highest possible frame rate).

### 7.3.3. xlnxvideosink

To inspect the xlnxvideosink plugin:
```

gst-inspect-1.0 xlnxvideosink

```

* ``sink-type`` property
  * (-1): none: None.
  * (0): dp: DisplayPort.
  * (1): hdmi: HDMI output.

* ``plane-id`` property
  - If you are using ``b00c0000.v_mix`` (HDMI output):
    - ``29`` is a YUY2 plane.
    - ``30`` is a YUY2 plane.
    - ``31`` is a UYUV plane.
* If you are using ``fd4a0000.zynqmp-display`` (DP output):
    - ``35`` supports a number of RGB.
    - ``34`` supports YUY2 and UYVY.
* Children:
  - ``kmssink0``

### 7.3.4. xlnxscale

  To inspect the ``xlnxscale`` plugin:
  ```

  # gst-inspect-1.0 xlnxscale

  ```

  * ``need-tdm`` property
    * true: Enables time division multiplexing.
    * false: Disables time division multiplexing.

### 7.3.5. sdx&lt;accelerator&gt;

To inspect the ``sdxfilter2d`` plugin:
```

# gst-inspect-1.0 sdxfilter2d

```

* ``filter_mode`` property
  * 1: Use HW acceleration.
  * 0: Use SW (the filter2d code executes entirely on the Arm™ processor).
* ``filter_preset`` property
  * Values 1 - 10 select a number of preset filters. The example uses 4, which is the emboss or edge enhancement filter.
* ``coefficients`` property
  * Array with a 3x3 coefficient matrix (for example,`coefficients="<<0,0,0>,<0,-1,0>,<0,0,0>>"`).

To inspect the ``sdxopticalflow`` plugin:
```

# gst-inspect-1.0 sdxopticalflow

```

* ``filter_mode`` property
  * 1: Use HW acceleration.
  * 0: Use SW (the optical flow code executes entirely on the ARM processor).

To inspect the ``sdxstereo`` plugin:
```

# gst-inspect-1.0 sdxstereo

```

* ``filter_mode`` property
  * 1: Use HW acceleration.
  * 0: Use SW (the optical flow code executes entirely on the Arm processor).
* ``config-filename`` property
  * This is how you specify the ZED camera configuration file, which must be present on the SD card (see [Single-Sensor Platform Stereo Demo: Special Considerations](#74-single-sensor-platform-stereo-demo-special-considerations)).

## 7.4. Single-Sensor Platform Stereo Demo: Special Considerations

The stereo vision demo is special in several ways. First, you _must_ use the ZED stereo camera connected to the USB video input. Second, and particular to this app, the width of the input image resolution is twice the width of the output resolution. The input consists of two images side-by-side, with the synchronized left and right stereo input supplied by the camera. Two cases are possible: 2560x720 in to 1280x720 out, and 3840x1080 in to 1920x1080 out. The default 3840x2160 output resolution is not supported by the Stereo Vision app.

The other special consideration is that a configuration file must be used that corresponds to the camera you have connected to your system. Each StereoLabs ZED camera has a unique parameters file associated with it. This text file comes from StereoLabs, and must be present on the SD Card for the Stereo Vision demo to work properly. You need the file unique to your camera, identified by its serial number (found on the ZED camera box and also on a black tag near the USB plug of the ZED camera itself). This number will be, for example, S/N 000012345. The parameter file for that camera would be named ``SN12345.conf``. To download your parameter file, enter the following URL into your browser, http://calib.stereolabs.com/?SN=XXXXX, adding the correct serial number. This downloads the configuration file to your computer.

The stereo block-matching algorithm calculates depth based on binocular parallax, similar to the way human eyes perceive depth. The depth map is coded in false colors. Objects far away appear deep blue. Closer objects appear in rainbow succession: green, yellow, orange, red, purple and finally white at about two feet from the camera in the 720p case, and about five feet away in the 1080p case. Any object closer than that cannot be tracked, and smooth areas with no texture in the image cannot be tracked, and show up as black. Areas with a lot of detail (especially with lots of vertical edges) are tracked best. It is normal that a large area on the left is black; this is 128 pixels wide, representing the range of the horizontal search for the best match between the right and left binocular images.



<hr/>

:arrow_forward:**Next Topic:**  [8. Platform Details](platform-details.md)

:arrow_backward:**Previous Topic:**  [6. Tool Flow Tutorials](tool-flow-tutorials.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018 Xilinx</sup></p>
