# Overview

The Current Value Table (CVT) module allows for storing and managing data in a single location, enabling users to share data between DCAF engines or between a DCAF engine and any parallel LabVIEW code using the [CVT Library](https://forums.ni.com/t5/Reference-Design-Content/LabVIEW-Current-Value-Table-CVT-Library/ta-p/3514251).

# Using the CVT Module

Outside of a DCAF CVT Module, the CVT can also be accessed using the CVT API which can be found in the palettes at Functions>>Addons>>Current Value Table.

![image006.png](https://ni.i.lithium.com/t5/image/serverpage/image-id/207566i54DEA064D9670EC1/image-size/large?v=1.0&px=999 "image006.png")

Within the same LabVIEW context running your DCAF application, you may use the API VIs to read and write individual values as shown in the screenshot of the Host Main VI shown in the Description Section. The API also enables efficient data access for values and groups of values. Refer to [LabVIEW Current Value Table Library](http://forums.ni.com/t5/Reference-Design-Content/LabVIEW-Current-Value-Table-CVT-Library/ta-p/3514251) for a more comprehensive treatment of using the CVT API.

The CVT may be accessed within modules, but should not be used as an alternative to the DCAF tag bus. The CVT may serve as a convenient mechanism to debug DCAF applications by providing access to selected tags with UI Reference modules to view and API calls to save a subset or all of the CVT to disk.

# Configuration

![Configuration](Documentation/Images/Configuration.png)

**Direction:**

**Filter:** Filter tags displayed in *Available Tags*, *From CVT*, and *To CVT* lists using the LabVIEW [Match Pattern](http://zone.ni.com/reference/en-XX/help/371361L-01/glang/match_pattern/) primitive

**Create Tags?:** When the CVT module initializes during runtime it will look up the indices of all tags to be written to or read from the Current Value Table. If *Create Tags?* is selected, the module will create any tags which it is not able to find, otherwise the module will fail to initialize.

# Software Requirements

+   LabVIEW 2014 or later
+   NI Current Value Table 3.3.0.13 or later
