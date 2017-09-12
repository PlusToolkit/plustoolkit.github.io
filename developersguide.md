---
layout: page
title: Developer's guide
group: navigation
order: 4
description: ""
---
{% include JB/setup %}


API documentation
-----------------

- <a href="http://perk-software.cs.queensu.ca/plus/doc/nightly/dev/">PlusLib API documentation</a>: generated nightly from the latest code version.

Testing dashboards
------------------

- <a href="http://perkdata.cs.queensu.ca/CDash/index.php?project=PlusLib">PlusLib dashboard</a>: results of automatic tests of the Plus library
- <a href="http://perkdata.cs.queensu.ca/CDash/index.php?project=PlusApp">PlusApp dashboard</a>: results of automatic tests of the Plus applications


Source code
-----------

Plus toolkit contains three main repositories:
- PlusLib: Library that contains all data acquisition and processing implementation. It contains a few sipmle tools and test applications but primarily intended to be linked into software applications.
- PlusApp: Software applications with graphical user interface that use PlusLib to make features available to end users.
- PlusBuild: Small project that downloads and builds PlusLib, PlusApp and all their dependencies (VTK, ITK, etc.).


Build instructions
------------------

<p>See the <a class="wiki_link" href="/wiki/show/plus/Developer_prerequisites" title="Developer prerequisites">Developer prerequisites</a> page for recommended background material for developers using PLUS.</p>

<h3 id="build_instructions">Build instructions</h3>
<span style="color: #ff0000;"><strong>Critical:</strong></span> In all repositories, <strong>developers must run Utilities/SetupForDevelopment.sh</strong> before commiting.<br />
&nbsp;
<h4 id="coding_conventions">Coding Conventions</h4>

<div>Much like any collaborative project, it is important for developers to adhere to the coding conventions layed out by the PLUS team. The coding convention adheres closely to the coding conventions of VTK with a few minor customizations. For convenience, the AStyle formatter (available as a standalone command-line tool or as an extension to Visual Studio) can be used with the following parameters:&nbsp;</div>

<div>&nbsp;</div>

<div><span style="font-weight: 600;">--style=allman --indent=spaces=2 --align-pointer=type --indent-switches --indent-namespaces --indent-preproc-block --indent-col1-comments --pad-oper --pad-header --unpad-paren --add-brackets --add-one-line-brackets --keep-one-line-blocks --convert-tabs --mode=c</span></div>

<div>
<h4 id="supported_platforms">Supported platforms</h4>

<div>
<ul>
	<li><span style="line-height: 17px; font-size: 13px;">32/64-bit builds: Plus can be built in either 32-bit or 64-bit mode. 64-bit applications have the advantage of larger available memory space (which is useful for certain applications, such as recording a large number of frames in memory, or reconstructing high-resolution volumes), but only a few hardware devices have 64-bit compatible drivers. If available memory is not a concern &nbsp;then use only 32-bit builds. If lots of memory is needed, and the application does not have to use tracking or imaging hardware devices directly then 64-bit build of Plus can be used. If both hardware support and lots of memory is needed then a 32-bit build of Plus can be used for data acquisition and the acquired data can be passed on to a 64-bit Plus or other application for further processing.</span></li>
	<li><span style="line-height: 17px; font-size: 13px;">Windows 7 32-bit/64-bit, Windows 10 32-bit/64-bit, Windows XP 32-bit embedded, Ubuntu 16.04, and MacOSX operating systems are fully supported and regularly tested.</span></li>
	<li><span style="line-height: 17px; font-size: 13px;">Running on <a class="wiki_link" href="/wiki/show/plus/Linux_Build_Instructions" title="Linux_Build_Instructions">Linux</a> and MacOS: Unfortunately many of the drivers written for devices are Windows specific, and thus capture cannot be done on a Linux or MacOSX machine. It is recommended to do the data acquisition on Windows and stream the acquired data to the Linux or MacOS computer for further processing.</span></li>
</ul>
</div>
</div>

<h4 id="detailed_instructions">Detailed instructions</h4>

<div>
<div>Plus library files and all required libraries and toolkits are automatically downloaded, configured, and built using CMake &quot;superbuild&quot; method (using external projects).</div>

<ul>
	<li><a class="wiki_link" href="/wiki/show/plus/Windows_Build_Instructions" title="Windows Build Instructions">Windows Build Instructions</a></li>
	<li><a class="wiki_link" href="/wiki/show/plus/Linux_Build_Instructions" title="Linux Build Instructions">Linux Build Instructions</a></li>
</ul>
