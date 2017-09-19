---
layout: page
title: Download
group: navigation
order: 3
description: ""
---
{% include JB/setup %}

Download
--------

Pre-compiled binary releases are available for Windows 7 / 8 / 10 / embedded XP only. Plus can be built on Linux and Mac OSX operating systems as described in the [Developer's guide](developersguide.md). Plus applications running on a different operating systems can exchange data between each other through OpenIGTLink.

- **[Latest stable release](http://perk-software.cs.queensu.ca/plus/packages/stable/)**
- **[Latest development snapshot](http://perk-software.cs.queensu.ca/plus/packages/nightly):** contains the latest features and fixes but it is not tested as thoroughly as stable releases

**Editions**

- PlusApp-...**-Win32**: Generic 32-bit release. To be used on 32/64-bit Windows 7, 8, 10 systems. Executables are 32-bit applications.
- PlusApp-...**-Win64**: Generic 64-bit release. Package to be used on 64-bit, Windows 7, 8, 10 systems. Executables are 64-bit applications. It can record more frames in memory and reconstruct larger volumes than the 32-bit release but less hardware devices are supported
- PlusApp-...-**Ultrasonix-5.7-Win32**: Package to be used on Ultrasonix systems (running on Windows XP embedded or Windows 7 operating system); running Ultrasonix Exam software version between 5.7.0 and 6.0.2. MicronTracker and Microsoft Media Foundation imaging devices are not supported. Executables are 32-bit applications.
- PlusApp-...-**Ultrasonix-6.1-Win32**: Package to be used on Ultrasonix systems (running on Windows XP embedded or Windows 7 operating system); running Ultrasonix Exam software version 6.1.1 and later. MicronTracker and Microsoft Media Foundation imaging devices are not supported. Executables are 32-bit applications.
- PlusApp-...-**ThorLabs-Win32**: Package to be used for connecting to ThorLabs spectrometers on 32/64-bit, Windows 7 and Windows 8 systems. Requires ThorLabs drivers installed (otherwise Plus applications will fail to start). Executables are 32-bit applications.
- PlusApp-...-**Interson-MTC-3.6-Win32**: Package to be used for connecting to Interson USB ultrasound probes on 32/64-bit, Windows 7 and Windows 8 systems. Requires Interson USB probe drivers installed (otherwise Plus applications will fail to start). With MicronTracker 3.6 SDK support. Executables are 32-bit applications.
- PlusApp-...-**Interson-MTC-3.7-Win32**: Package to be used for connecting to Interson USB ultrasound probes on 32/64-bit, Windows 7 and Windows 8 systems. Requires Interson USB probe drivers installed (otherwise Plus applications will fail to start). With MicronTracker 3.7 SDK support. Executables are 32-bit applications.
- PlusApp-...-**Telemed-Win32**: Package to be used for connecting to Telemed Ultrasound systems on 32/64-bit, Windows 7 and Windows 8 systems. Executables are 32-bit applications.
- PlusApp-...-**BK-Win32**: Package to be used for connecting to BK Ultrasound systems on 32/64-bit, Windows 7 and Windows 8 systems. Requires BK OEM interface license. Package is available on request.
- PlusApp-...-**StealthLink-Win32**: Package to be used for connecting to Medtronic navigation systems through StealthLink interface on 32/64-bit, Windows 7 and Windows 8 systems. Requires StealthLink license. Package is available on request.
- Mac OS X and Linux packages can be built with limited hardware device support. Post a message on the message board if help is needed.

**Supported devices in latest development snapshots**

<table border="0" cellspacing="0">
	<colgroup>
		<col />
		<col />
		<col />
		<col />
		<col />
		<col />
		<col />
		<col />
		<col />
	</colgroup>
	<tbody>
		<tr height="20">
			<td height="20" style="width: 89px; height: 20px;"> </td>
			<td style="width: 64px;">Win32</td>
			<td style="width: 79px;">Win64</td>
			<td style="width: 99px;">Telemed<br />
			Win32</td>
			<td style="width: 107px;">Ultrasonix-5.7<br />
			Win32</td>
			<td style="width: 152px;">Ultrasonix-6.1<br />
			Win32</td>
			<td style="width: 135px;">MTC-3.7<br />
			Win32</td>
			<td style="width: 139px;">Interson-MTC-3.7<br />
			Win32</td>
			<td style="width: 139px;">ThorLabs<br />
			Win32</td>
			<td style="width: 128px;">StealthLink</td>
		</tr>
		<tr height="20">
			<td height="20" style="height: 20px;">NDI Polaris &amp; Aurora</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
		</tr>
		<tr height="20">
			<td height="20" style="height: 20px;">NDI Ascension</td>
			<td>Y</td>
			<td>N</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
		</tr>
		<tr height="20">
			<td height="20" style="height: 20px;">NDI Certus</td>
			<td>Y</td>
			<td>N</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
		</tr>
		<tr height="20">
			<td height="20" style="height: 20px;">MicronTracker (3.7)</td>
			<td>Y</td>
			<td>N</td>
			<td>Y</td>
			<td>N</td>
			<td>N</td>
			<td>Y</td>
			<td>Y</td>
			<td>N</td>
			<td>Y</td>
		</tr>
		<tr height="20">
			<td height="20" style="height: 20px;">OpticalMarkerTracker</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>N</td>
			<td>N</td>
			<td>Y</td>
			<td>Y</td>
			<td>N</td>
			<td>Y</td>
		</tr>
		<tr height="20">
			<td height="20" style="height: 20px;">Stealthlink</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>Y</td>
		</tr>
		<tr height="20">
			<td height="20" style="height: 20px;">Ultrasonix (5.7)</td>
			<td>Y</td>
			<td>N</td>
			<td>Y</td>
			<td>Y</td>
			<td>N</td>
			<td>Y</td>
			<td>N</td>
			<td>Y</td>
			<td>Y</td>
		</tr>
		<tr height="20">
			<td height="20" style="height: 20px;">Ultrasonix (6.1)</td>
			<td>Y</td>
			<td>N</td>
			<td>Y</td>
			<td>N</td>
			<td>Y</td>
			<td>N</td>
			<td>N</td>
			<td>Y</td>
			<td>Y</td>
		</tr>
		<tr height="20">
			<td height="20" style="height: 20px;">Telemed</td>
			<td>N</td>
			<td>N</td>
			<td>Y</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>Y</td>
		</tr>
		<tr height="20">
			<td height="20" style="height: 20px;">Interson</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>Y</td>
			<td>N</td>
			<td>N</td>
		</tr>
		<tr height="20">
			<td height="20" style="height: 20px;">Microsoft Media foundation</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>N</td>
			<td>N</td>
			<td>Y</td>
			<td>Y</td>
			<td>N</td>
			<td>Y</td>
		</tr>
		<tr height="20">
			<td height="20" style="height: 20px;">Brachy steppers</td>
			<td>Y</td>
			<td>N</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
			<td>Y</td>
		</tr>
		<tr height="20">
			<td height="20" style="height: 20px;">ThorLabs spectrometer</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>N</td>
			<td>Y</td>
			<td>N</td>
		</tr>
	</tbody>
</table>

**Notes**

- Note: some browsers may indicate that the installers are malicious files. This is a common problem when offering download of executable files (for example see discussion [here](https://productforums.google.com/forum/#!topic/chrome/r-9JQIboUmc)). If you doubt the safety of a package, download it and before you run it, submit to online malware scanners, such as https://www.metascan-online.com or https://www.virustotal.com/.
- If Plus applications fail to start, install Microsoft Visual Studio redistributable packages:
  - MSVCP120.dll missing => [install VS2013 redistributable](http://www.microsoft.com/en-us/download/details.aspx?id=40784) and restart your computer
  - MSVCP140.dll missing => [install VS2015 redistributable](https://www.microsoft.com/en-ca/download/details.aspx?id=48145) and restart your computer
	- Embedded XP requires XP SP3 and Visual Studio 2013 Redistributable x86 installed.

<p style="text-align: right;"> <a href="http://c3.gostats.com/summary.xml?id=352601" target="_blank" title="statistics"><img alt="statistics" border="0" src="http://c3.gostats.com/bin/count/a_352601/t_4/i_79/z_0/show_visitors/counter.png" style="border-width: 0px; width: auto; height: auto; display: none !important;" /></a></p>
