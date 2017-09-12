---
layout: page
title: Features
group: navigation
order: 2
description: ""
---
{% include JB/setup %}

<table>
  <tbody>
    <tr>
      <td style="text-align: center;"> <img src="{{ site.url }}/assets/images/Trackers.png" /><br />
        Position data acquisition from various devices, including electromagnetic trackers (Ascension, NDI Aurora) and optical trackers (NDI Polaris and Certus, Claron MicronTracker)
      </td>
      <td style="text-align: center;"> <img src="{{ site.url }}/assets/images/NavSystems.png" /><br />
        Data acquisition from commercial surgical navigation systems: Medtronic StealthStation navigation system (receives tracking data and planning volume), BrainLab navigation system (receives tracking data, planning volume, and landmarks; through OpenIGTLink)
      </td>
      <td style="text-align: center;"> <img src="{{ site.url }}/assets/images/PositioningDevices.png" /><br />
        Data acquisition from various positioning devices: prostate LDR brachytherapy steppers (CIVCO, CMS Accuseed, Burdette Medical Systems), daVinci surgical systems (experimental), Kuka LightWeight robot (through OpenIGTLink)
      </td>
    </tr>
    <tr>
      <td style="text-align: center;"><img src="{{ site.url }}/assets/images/Ultrasound.png" /><br />
        Image acquisition from ultrasound systems: &nbsp;through direct digital interface (for Ultrasonix, BK, Interson, Telemed, Philips ultrasound scanners) and through framegrabbers
      </td>
      <td style="text-align: center;"><img src="{{ site.url }}/assets/images/UsSimulator.png" /><br />
        Ultrasound image simulation: B-mode images are generated from multiple moving objects (such as bones, soft tissue, tools), each defined by a simple surface mesh.
      </td>
      <td style="text-align: center;"><img src="{{ site.url }}/assets/images/ImagingDevices.png" /><br />
        Image acquisition from various other devices including surgical microscopes, video endoscopes, webcams, USB cameras, Siemens MRI scanners (receives slices in real-time, through OpenIGTLink)
      </td>
    </tr>
    <tr>
      <td style="text-align: center;"><img src="{{ site.url }}/assets/images/Imu.png" /><br />
        Data acquisition from orientation sensors and controllers: PhidgetSpatial, CHRobotics, Microchip inertial sensors; 3Dconnexion 3D mouse
      </td>
      <td style="text-align: center;"><img src="{{ site.url }}/assets/images/Spectrometer.png" /><br />
        Data acquisition from ThorLabs compact CCD spectrometers for real-time navigated optical spectroscopy applications.
      </td>
      <td style="text-align: center;"><img src="{{ site.url }}/assets/images/Arduino.png" /><br />
        Data acquisition and control using Arduino devices (through serial interface)
      </td>
    </tr>
    <tr>
      <td style="text-align: center;"><img src="{{ site.url }}/assets/images/fCal.png" /><br />
        Fully automatic spatial and temporal ultrasound probe calibration: with convenient GUI application, tutorial, 3D printable calibration phantom. Fully automatic temporal calibration of multiple tracking systems.
      </td>
      <td style="text-align: center;"><img src="{{ site.url }}/assets/images/PlusServer.png" /><br />
        Streaming of live tracked&nbsp;image data to <a href="http://www.slicerigt.org">3D Slicer / SlicerIGT</a> and other OpenIGTLink-compatible applications.
      </td>
      <td style="text-align: center;"><img src="{{ site.url }}/assets/images/VolRec.png" /><br />
        Ultrasound volume reconstruction: performance-optimized, multi-threaded, with advanced hole filling, skin surface contact detection.
      </td>
    </tr>
    <tr>
      <td style="text-align: center;"><img src="{{ site.url }}/assets/images/4dUs.png" /><br />
        Support of 8/16-bit grayscale, 24-bit RGB images in 2D+t and 3D+t image streams.  Ultrasound RF to B-mode conversion: brightness conversion and scan conversion, for linear and curvilinear transducers.
      </td>
      <td style="text-align: center;"><img src="{{ site.url }}/assets/images/ModelCatalog.png" /><br />
        <a href="http://perk-software.cs.queensu.ca/plus/doc/nightly/modelcatalog/"><strong>Catalog of freely usable printable 3D models of tools and tracking fixtures </strong></a>
      </td>
      <td style="text-align: center;">&nbsp;</td>
    </tr>
  </tbody>
</table>

<p>

- Matlab interface for real-time sending and receiving of transforms or reading/writing of transforms and image data to/from files (implemented as readily usable Matlab scripts, no need for compiling MEX files, etc.)
- Automatic testing infrastructure, diagnostic tools, simulators for development and testing without having access to hardware devices
- Fully supported on Windows 32 and 64 bit with VS2008, limited testing is performed with VS2010, VS2012,&nbsp;and with gcc on Linux, occasionally tested on Mac OS X
- Many research groups and companies use the toolkit worldwide
- Completely free, no restriction BSD license (for everything, including source code, documentation, CAD models, etc.)
