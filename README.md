# Overview

The Current Value Table (CVT) module allows for storing and managing data in a single location that can be accessed in different parts of the application. In DCAF applications, the CVT module enables sharing data between the DCAF Tag Bus and parallel loops and processes.

# Description

The DCAF CVT module installs a class implementation which depends on the [LabVIEW Current Value Table Library](http://forums.ni.com/t5/Reference-Design-Content/LabVIEW-Current-Value-Table-CVT-Library/ta-p/3514251) which provides an API for storing and managing data. CVT module channels may be configured to read or write from tags. The DCAF CVT module enforces the safe practice of exactly one writer for tag data. When writing current values with the CVT API, minimize the chance for race conditions by using a single write per CVT value. The CVT API may then be used to share data between the tag bus and the Host Main VI. In the case shown below, “CVT Write” is written to and “CVT Read” is read from the Host Main VI of the DCAF application.

![image001.png](https://ni.i.lithium.com/t5/image/serverpage/image-id/207558i9989CE4D19919DB1/image-size/large?v=1.0&px=999 "image001.png")

To share data between CVT and tag bus, the names need to match exactly (case sensitive) between CVT reads and writes, CVT module configuration, and Tags module configuration.

The CVT may be accessed within modules, but should not be used as an alternative to the DCAF tag bus. The CVT may serve as a convenient mechanism to debug DCAF applications by providing access to selected tags with UI Reference modules to view and API calls to save a subset or all of the CVT to disk.

# Configuration of the CVT Module

CVT channel mappings are configured in the configuration UI (CVT editor node.lvclass:configuration UI.vi) in the Standard Configuration Editor.

![image003.png](https://ni.i.lithium.com/t5/image/serverpage/image-id/207564i528FDA157B35B48A/image-size/large?v=1.0&px=999 "image003.png")

In the screenshot above, “CVT Write” tag is updated from CVT while the “CVT Read” element of the CVT is updated from the tag bus.

### Steps before Configuration

If your application requires a UI for the user to set CVT values or read CVT values, create a UI.

![image005.png](https://ni.i.lithium.com/t5/image/serverpage/image-id/207565i654EA729067D7A65/image-size/large?v=1.0&px=999 "image005.png")

Then, add a UI Reference module and configure it from the UI VI.

# Using the CVT Module

Outside of a DCAF CVT Module, the CVT can also be accessed using the CVT API which can be found in the palettes at Functions>>Addons>>Current Value Table.

![image006.png](https://ni.i.lithium.com/t5/image/serverpage/image-id/207566i54DEA064D9670EC1/image-size/large?v=1.0&px=999 "image006.png")

Within the same LabVIEW context running your DCAF application, you may use the API VIs to read and write individual values as shown in the screenshot of the Host Main VI shown in the Description Section. The API also enables efficient data access for values and groups of values. Refer to [LabVIEW Current Value Table Library](http://forums.ni.com/t5/Reference-Design-Content/LabVIEW-Current-Value-Table-CVT-Library/ta-p/3514251) for a more comprehensive treatment of using the CVT API.

# Source Code Design

The DCAF CVT Module code is a class based implementation of a DCAF plugin module that wraps the functionalities of the Tag Bus Module and the LabVIEW Current Value Table Library. You can see how tags can be iteratively added and removed during configuration by investigating CVT editor node.lvclass:configuration UI.vi.

At runtime, the DCAF tag bus API and the CVT API are used together to share data between Engine tags and CVT values. Note that the input VI (called for inputs to the engine) calls down into the CVT API to read ‘from CVT’ update mapped tags.

![image007.png](https://ni.i.lithium.com/t5/image/serverpage/image-id/207567i111216703832F50D/image-size/large?v=1.0&px=999 "image007.png")

The output VI (called to update outputs from the engine) reads DCAF tags and calls down into the CVT API to write ‘to CVT.’

![image009.png](https://ni.i.lithium.com/t5/image/serverpage/image-id/207568iF1F54C1D83538FC1/image-size/large?v=1.0&px=999 "image009.png")

# Performance

All CVT writes and reads are optimized. To get the best possible performance, write and read CVT values in bulk by index.

# Software Requirements

+   LabVIEW 2014 or later

# Limitations

+   The CVT library only supports plain old datatypes which does not include classes, waveforms, clusters, nor variants.
