# Issue

**Title:** Extensions to the SOP classes and Transfer Syntaxes hardcoded lists.

## Description

### Changes by acceptance criteria

> * The list of supported SOP classes and the list of supported transfer syntaxes should both be 
> extensible independently, via configuration.
>   * Let's try using new categories in confs/server.xml for this.

Schema example is shown further ahead.

>  * Each custom SOP class or transfer syntax should specify a UID and alias. Once done,
that entry is added alongside the hardcoded default list (so these records cannot be 
removed) 

All entries are successfully added alongside the lists at:
  * TransfersStorage. However, they are not added right after the hardcoded lists’ initialization, for the reason that the settings (ServerSettingsManager.inner and thus, the additional entries 
present in server.xml) are initialized a posteriori. To solve this problem, the “additionals” are completed right after the settings reading process, in this case using TransfersStorage.completeList().
  * SOPList. The situation is similar. The list is updated after the settings’ initialization, in SOPList.updateList(). There is, in this function, however, one other aspect. Since the hardcoded list is initialized prior to the settings, and that in that initialization, each SOP class is associated with the list of transfer syntaxes, that list is also updated (with the new transfer syntaxes, if any).
  * SOPClassSettings. There is no need for posterior updates, since this class is only instantiated after the settings.

>  * This configuration can be empty or unspecified.

Empty tags are ignored.

>  * This list is not sufficient for the DICOM storage server to accept those SOP classes and transfer syntaxes. This must be configured as usual. 

All SOP classes in the transfer options, be it the hardcoded or the additional ones, will have the additional transfer syntaxes unchecked in their list.

> * Server settings should be validated for unspecified UIDs, but it must let users specify well 
configured UIDs and have that applied in the DICOM storage server. 

All additional SOP classes as well as TSs will have their UIDs validated using `UIDUtils.isValid(uid)` from dcm4che2.

> * The user interface should acknowledge the extended list of SOP classes and show options 
for the extended list of transfer syntaxes.

Done successfully.

### New schema at settings example
```xml
<config>
...
    <additional-sop-classes>
      <additional-sop-class uid="1.2.840.100008.5.1.4.1.1.131 " alias="BasicStructuredDisplayStorage" />
    </additional-sop-classes>
    <additional-transfer-syntaxes>
      <additional-transfer-syntax uid="1.2.840.100008.1.2.4.95" alias="JPIPReferencedDeflated" explicitVR="true" deflated="true" encapsulated="false"/>
    </additional-transfer-syntaxes>
...
</config>
```
Note: Element `additional-transfer-syntax` can have the following attributes:
* `explicitVR`: VR representation, "true" means explicit (**default**) and "false" means implicit
* `bigEndian`: Endianness, "true" is for Big Endian and "false" means Little Endian (**default**);
* `encapsulated`: Encapsulated pixel data ("true", **default**) or native pixel data ("false")
* `deflated`: whether the whole data set is deflated (**default** is "false").

### Testing
The `ServerSettingsTest` class tests the process of reading the new schema section from the server.xml configuration file into the `ServerSettingsManager` (inner) settings.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `50c568ade601`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.