# Adding a Device
When adding a new device, it can seem like a daunting task. The information contained below exists to help understand how Plus is structured, and what is necessary to do when adding a new device. The four major categories of steps to complete are in CMake, C++, configuration/XML, and documentation.

First, we'll explore the use of an external SDK or API provided by your devices manufacturer (or open-source community).

## Device SDK/API
If a device needs to make calls to an SDK, you will have to make it available for inclusion and linking. 

### CMake enabled SDK
If an API is in a public repository, and is "CMake-ified", you can add it as an external project in the [PlusBuild](https://github.com/PlusToolkit/PlusBuild) project.

* In your cloned PlusBuild folder, navigate to
  * `<PlusBuild>\SuperBuild`
* Add a file (where ExternalSDK is the name of the SDK, for example, `External_OpenCV`)
  * `<PlusBuild>\SuperBuild\External_DeviceSDK.cmake`
* In that file, add the following contents, customized to your SDK

``` cmake
IF(<externalSDK>_DIR)
  # <externalSDK> has been built already
  FIND_PACKAGE(<externalSDK> <optional_sdk_version> REQUIRED NO_MODULE)

  MESSAGE(STATUS "Using <externalSDK> available at: ${<externalSDK>_DIR}")

  # Copy libraries to CMAKE_RUNTIME_OUTPUT_DIRECTORY
  PlusCopyLibrariesToDirectory(${CMAKE_RUNTIME_OUTPUT_DIRECTORY} ${<externalSDK>_LIBRARIES})

  SET (PLUS_<externalSDK>_DIR ${<externalSDK>_DIR} CACHE INTERNAL "Path to store <externalSDK> binaries")
ELSE()
  # <externalSDK> has not been built yet, so download and build it as an external project
  SetGitRepositoryTag(
    <externalSDK>
    <your_git_url>
    <your_git_tag>
    )

  SET (PLUS_<externalSDK>_SRC_DIR "${CMAKE_BINARY_DIR}/Deps/<externalSDK>")
  SET (PLUS_<externalSDK>_DIR "${CMAKE_BINARY_DIR}/Deps/<externalSDK>-bin" CACHE INTERNAL "Path to store <externalSDK> binaries")
  ExternalProject_Add( <externalSDK>
    "${PLUSBUILD_EXTERNAL_PROJECT_CUSTOM_COMMANDS}"
    PREFIX "${CMAKE_BINARY_DIR}/Deps/<externalSDK>-prefix"
    SOURCE_DIR "${PLUS_<externalSDK>_SRC_DIR}"
    BINARY_DIR "${PLUS_<externalSDK>_DIR}"
    #--Download step--------------
    GIT_REPOSITORY ${<externalSDK>_GIT_REPOSITORY}
    GIT_TAG ${<externalSDK>_GIT_TAG}
    #--Configure step-------------
    CMAKE_ARGS 
      ${ep_common_args}
      -DCMAKE_RUNTIME_OUTPUT_DIRECTORY:PATH=${CMAKE_RUNTIME_OUTPUT_DIRECTORY}
      -DCMAKE_LIBRARY_OUTPUT_DIRECTORY:PATH=${CMAKE_LIBRARY_OUTPUT_DIRECTORY}
      -DCMAKE_ARCHIVE_OUTPUT_DIRECTORY:PATH=${CMAKE_ARCHIVE_OUTPUT_DIRECTORY}
      -DBUILD_SHARED_LIBS:BOOL=${PLUSBUILD_BUILD_SHARED_LIBS}
      <your_library_configure_flags>
      -DCMAKE_CXX_FLAGS:STRING=${ep_common_cxx_flags}
      -DCMAKE_C_FLAGS:STRING=${ep_common_c_flags}
    #--Build step-----------------
    BUILD_ALWAYS 1
    #--Install step-----------------
    INSTALL_COMMAND ""
    DEPENDS ${<externalSDK>_DEPENDENCIES}
    )
ENDIF()
```

### Non-CMake enabled SDK
If your SDK comes from another source, such as an installer, you will be required to write a find module that locates the necessary include directories and library files.

You should place your find module in the `<PlusBuild>\Modules` folder in order for PlusBuild to be able to use it. There are many examples online and in the `Modules` folder of how to write a find module. If you are stuck, you can create a discussion on the [PlusLib](https://github.com/PlusToolkit/PlusLib/discussions) discussions page.

## CMake
There are a few steps required to add the device to the project.
### PlusBuild
* In the root `CMakeLists.txt` of the [PlusBuild](https://github.com/PlusToolkit/PlusBuild) repository, add an option for the device.
  * Example: `OPTION(PLUS_USE_YourDeviceName "Provide support for <your device description>" OFF)`
* If necessary, add an include of any external SDKs necessary for your device
``` cmake
IF(PLUS_USE_YourDeviceName)
  INCLUDE(SuperBuild/External_DeviceSDK.cmake)
ENDIF()
```
* Add it as a dependency to the PlusLib project (this ensures correct build order in PlusBuild)
* In the `<PlusBuild>\Superbuild\External_PlusLib.cmake` file, add a line to the end of the `ExternalProject_Add(PlusLib ...` command to pass your device option to the PlusLib project
  * Example: `-DPLUS_USE_YourDeviceName:BOOL=${PLUS_USE_YourDeviceName}`
``` cmake
IF(PLUS_USE_YourDeviceName AND NOT <externalSDK>_DIR)
  LIST(APPEND PlusLib_DEPENDENCIES <externalSDK>)
ENDIF()
```

### PlusLib
* In `<PlusLib>\src\PlusConfigure.h.in`, add the following
  * `#cmakedefine PLUS_USE_YourDeviceName`
* In `<PlusLib>\src\UsePlusLib.cmake.in`, add the following
  * `SET(PLUS_USE_YourDeviceName @PLUS_USE_YourDeviceName@)`
* In `<PlusLib>\src\PlusDataCollection\CMakeLists.txt`, add the following
  * Replicate the device option: `OPTION(PLUS_USE_YourDeviceName "Provide support for <your device description>" OFF)`
  * Add the section to include your C++ code and dependencies:
  
```
# --------------------------------------------------------------------------
# YourDevice
IF(PLUS_USE_YourDeviceName)
  # If your device uses an external SDK, keep the following
  FIND_PACKAGE(<externalSDK> REQUIRED)

  SET(YourDeviceName_SRCS
    <YourDeviceDirectory>/vtkPlusYourDeviceNameSource.cxx
    )
  IF(MSVC OR ${CMAKE_GENERATOR} MATCHES "Xcode")
    SET(YourDeviceName_HDRS
      <YourDeviceDirectory>/vtkPlusYourDeviceNameSource.h
      )
  ENDIF()

  LIST(APPEND ${PROJECT_NAME}_HDRS
    ${YourDeviceName_HDRS}
    )

  LIST(APPEND ${PROJECT_NAME}_SRCS
    ${YourDeviceName_SRCS}
    )

  LIST(APPEND ${PROJECT_NAME}_INCLUDE_DIRS
    ${CMAKE_CURRENT_SOURCE_DIR}/<YourDeviceDirectory>
    )

  LIST(APPEND ${PROJECT_NAME}_LIBS
    <YourDevice_Library_Name> # this is the CMake targets produced by the external project or find module
    )
ENDIF()
```

#### Testing
* In `<PlusLib>\src\PlusDataCollection\Testing\CMakeLists.txt`, add the following

``` cmake
#*************************** YourDeviceNameTest1 ***************************
ADD_EXECUTABLE(YourDeviceNameTest1 YourDeviceNameTest.cxx)
SET_TARGET_PROPERTIES(YourDeviceNameTest1 PROPERTIES FOLDER Tests)
TARGET_LINK_LIBRARIES(YourDeviceNameTest1 vtkPlusDataCollection) # add any other dependencies to the test executable

ADD_TEST(YourDeviceNameTest1 
  ${PLUS_EXECUTABLE_OUTPUT_PATH}/YourDeviceNameTest1
  --config-file=${ConfigFilesDir}/Testing/PlusDeviceSet_DataCollectionOnly_YourDeviceName.xml 
  )
SET_TESTS_PROPERTIES(YourDeviceNameTest1 PROPERTIES FAIL_REGULAR_EXPRESSION "ERROR;WARNING")
```

## C++
### Data Collection
* Create the following two files
  * `<PlusLib>\src\PlusDataCollection\<YourDeviceDirectory>\vtkPlusYourDeviceNameSource.cxx`
  * `<PlusLib>\src\PlusDataCollection\<YourDeviceDirectory>\vtkPlusYourDeviceNameSource.h`
* It is highly recommended that you duplicate an existing device and modify it for your purposes. Various aspects to these files are described below.

### Device Factory
Plus uses the factory design pattern to create devices in code. To connect your device to the factory system modify `vtkPlusDeviceFactory.cxx` to add the following:

In headers area:
```c++
#ifdef PLUS_USE_YourDevice
  #include "vtkPlusYourDevice.h"
#endif
```

and in the factory constructor:
```c++
#ifdef PLUS_USE_YourDevice
  RegisterDevice("YourDevice", "vtkPlusYourDevice", (PointerToDevice)& vtkPlusYourDevice::New);
#endif
```

### Channels, Data Sources, and Buffers
The following is the terminology necessary to understanding data storage and manipulation in Plus.
* A data source is a class that contains a buffer, and meta data specific to a source of data from your device. This may be a tool, video, or text field. For example, a tracker may be able to track multiple tools, each of which must have its own data source.
* A buffer is simply storage of tracked frames, which contain [0-1] images, [0-n] transforms, and [0-n] fields.
* A channel is a collection of data sources and must contain [0-1] video sources, [0-n] tool sources, and [0-n] field sources.

Plus devices are able to operate on any number of input channels, and store data to output data sources. A device may configure any number of output channels, which are composed of combinations of output data sources depending on the purpose and design of the underlying device.

The key classes in data storage are `vtkPlusChannel`, `vtkPlusDataSource`, `vtkPlusBuffer`, `igsioTrackedFrame`, `vtkIGSIOTrackedFrameList`, and `PlusBufferItem`.

### Function Breakdown
The following assumes you have a device class called `YourDevice`.

Depending on how your device behaves, and how the SDK is structured (if applicable), there are a number of key concepts which must be implemented.

#### Polling vs. Callback
If your device uses an SDK that needs to be polled regularly, your device will need to set `this->StartThreadForInternalUpdates` to `true` in your constructor(s). This will tell the parent class `vtkPlusDevice` to start a thread that will call logic in `YourDevice::InternalUpdate` at a rate determined by the `AcquisitionRate` attribute in your device's XML configuration. `InternalUpdate` is called from `vtkPlusDevice::vtkDataCaptureThread`.

If your device SDK provides by a callback mechanism, you should set `this->StartThreadForInternalUpdates` to `false` (or leave out, default is `false`). The callback function will be responsible for receiving and processing data from your device.

More advanced devices may require a combination of `InternalUpdate` driven polling and callback updates, which can be performed by merging the two above approaches.

#### Starting/Stopping and Connecting/Disconnecting
Typically `YourDevice::InternalStartRecording` and `YourDevice::InternalStopRecording` are lightweight functions meant to pause or resume collection of data, without setup or tear-down of resources. The parent class logic will prevent calling of `InternalUpdate` if the device recording is stopped. These functions are your opportunity to pause/resume any hardware, if applicable.

Initialization and destruction of resources is performed during `YourDevice::InternalConnect` and `YourDevice::InternalDisconnect` respectively.

#### Configuration
There are three key functions in the configuration mechanism.

`YourDevice::ReadConfiguration` is responsible for reading parameters set in the configuration file (see XML section below) and applying them to your device. This function (when using `vtkPlusDataCollector` as your application data collection backbone) is performed before `YourDevice::InternalConnect`.

`YourDevice::WriteConfiguration` is responsible for recording the current state of your device to XML. This can be called at any time.

`YourDevice::NotifyConfigured` is a multi-purpose function which is called after all devices have been configured, all inputs and outputs have been connected between devices, but before devices begin collecting data. This is the last chance for your device to raise an error about improper or insufficient configuration.

#### Capturing Data
There are a number of entry points for storing data, the most common are documented here.
* `vtkPlusDataSource::AddItem` or `vtkPlusDataSource::AddTimeStampedItem`
* `vtkPlusDevice::AddVideoItemToVideoSources`
* `vtkPlusDevice::ToolTimeStampedUpdate` or `vtkPlusDevice::ToolTimeStampedUpdateWithoutFiltering`

These functions would be typically called once per `InternalUpdate` or callback.

### Common Patterns
* The `vtkPlusDataCollector` class' purpose is to take a configuration, and setup all of the necessary devices, channels, and connections. An example of this is available at [QConfigurationToolbox::ConnectToDevicesByConfigFile](https://github.com/PlusToolkit/PlusApp/blob/master/fCal/Toolboxes/QConfigurationToolbox.cxx#L129). This function is called via the Qt signal/slot mechanism from the `void ConnectToDevicesByConfigFileInvoked(std::string)` signal in [QPlusDeviceSetSelectorWidget](https://github.com/PlusToolkit/PlusLib/blob/master/src/PlusWidgets/QPlusDeviceSetSelectorWidget.h)
* Devices store recorded data into data sources, but choosing which data source is important. In a device with multiple sources (say, a tracker tracking multiple tools), it is expected that you, the developer, have a way of identifying which data belongs to which source. This can be accomplished by using the XML attribute of a `vtkPlusDataSource` and code logic based on data capture metadata (tool identifier provided by SDK, etc...).
* Sometimes, a device only has one data source, and then it's an easy affair of calling (from a method within `YourDevice`) `this->GetFirstVideoSource(...)`, `this->GetFirstActiveTool(...)` or similar. You should verify in `YourDevice::NotifyConfigured` that you have a data source to record too before assuming its existence.

### Testing
* Duplicate an existing device test file into the following file
  * `<PlusLib>\src\PlusDataCollection\Testing\YourDeviceNameTest.cxx`
* Modify the test file to create your device, call any testable functions, and output the success/failure of the device's ability to record data

## XML
All configuration of a device is performed via an XML configuration file provided to a Plus program. Like other steps, it is highly recommended that you reference an existing device for examples of how to make your device configurable. Device parameters are read and written `YourDevice::ReadConfiguration` and `YourDevice::WriteConfiguration`.

Two example devices are shown below. One connects to hardware, and the other is a virtual (software) device that acts on input from other device output.

``` xml
<Device
  Id="VideoDevice"
  Type="SonixVideo" 
  AcquisitionRate="30"
  Depth="100"
  AutoClipEnabled="TRUE"
  ImageGeometryOutputEnabled="TRUE"
  ImageToTransducerTransformName="ImageToProbe" >
  <DataSources>
    <DataSource Type="Video" Id="Video" PortName="B" PortUsImageOrientation="UF"  />
  </DataSources>
  <OutputChannels>
    <OutputChannel Id="VideoStream" VideoDataSourceId="Video" />
  </OutputChannels>
</Device>

<Device 
  Id="TrackedVideoDevice" 
  Type="VirtualMixer" >
  <InputChannels>
    <InputChannel Id="TrackerStream" />
    <InputChannel Id="VideoStream" />
  </InputChannels>
  <OutputChannels>
    <OutputChannel Id="TrackedVideoStream"/>
  </OutputChannels>
</Device>
```

## Documentation
Documentation of your device is critical in order for other users to understand how to properly configure and use your implementation.

* Please create and complete the following file (use an existing device file as a template):
  * `<PlusLib>\src\Documentation\UserManual\DeviceYourDeviceName.dox`
* Add an entry to your device page in `<PlusApp>\Documentation\Configuration.dox`
  * `- \subpage DeviceYourDeviceName`

The Plus documentation build will include your page in the user manual generated nightly.
