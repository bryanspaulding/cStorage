{{AppVeyor build status badge for master branch}}

#cStorage

The **cStorage** module contains the cDisk, cPartition, and cVolume resources. 

The cPartition and cVolume resources operate under the assumption that one
disk may only have one partition and the parition will be the the same size 
of the disk it is hosted on. A volume (file system) is already limited to 
being the same size as the partition it is hosted on.

This one disk/one partition assumption has been made by cStorage to make sure 
the configurations it is used to describe will always result in the exact 
same configuration. 


## Contributing
Please check out common DSC Resources [contributing guidelines](https://github.com/PowerShell/DscResource.Kit/blob/master/CONTRIBUTING.md).

## Resources

* **cDisk** ensures a RAW disk is initialized for GPT partition styles.
* **cPartition** ensures a Partition is created on a disk.
* **cVolume** ensures a Volume is created on a Partition on a Disk, and 
optionally assigns the volume a drive letter or attaches to a Mount Point.



### cDisk

The cDisk resource allows for an RAW disk to be intialized for first time use. 
In order to *never* be destructive:
- cDisk will only bring online an Offline disk that Get-Disk reports 
the isClustered property is False.
- Will only initialize RAW disks with no partitions.
- There is no code in the cDisk module that takes a disk Offline.

* **DiskNumber**: The disk number of the disk as reported by the `Get-Disk` 
PowerShell cmdlet's Number property.

### cPartition

The cPartition resources allows creation of GPT Partitions on online, 
initialized disks.

In order to *never* be destructive, and to be consistent, predictable, 
and idempotent:
- cPartition only allows the creation of Partitions in empty disk space.
- cPartition will only create a partition that is the same size as the 
disk it is on.

* **DiskNumber**: [Required] The disk number of the disk as reported by the `Get-Disk` 
PowerShell cmdlet's Number property to create the Partition on.
* {{**Property2**: Description of property 2

### cVolume

The cVolume resources allows creation of volumes (NTFS filesystems) on 
partitions.

In order to *never* be destructive and to be consistent, predictable, 
and idempotent:
- cVolume only allows the creation of Volumes in empty, unformatted 
partitions.
- cVolume will only format an empty partition.
- cVolume will never format an existing partition if it doesn't match the
indicated Filesystem. It will throw a warning instead.


* **DiskNumber**: [Required] The disk number of the disk as reported by the `Get-Disk` 
PowerShell cmdlet's Number property to create the Partition on.
* **PartitionNumber**: [Default = 1] The optional ParitionNumber, as returned
 by the `Get-Partition` cmdlet, identifing the volume to configure. This 
parameter is available to allow cVolume to be used to validate the 
configuration of volumes that were not created by the cDisk, cVolume, and 
cPartition.
* **FileSystemLabel**: [Default = $null] The File System Label to apply to the 
volume.
* **AllocationUnitSize**: Specifies the allocation unit size to use when 
formatting the volume.
* **AccessPaths**: [Default = $null] Specifies the Drive Letter to use for the 
volume, and/or the Mount Point to apply to the volume. AccessPaths can be an 
array of multiple Drive letters and/or multiple Mount Paths. 
- All Drive Letters be in the form "X:\", where X is a single digit drive 
letter. For example, "D:\" or "E:\" or "F:\".
- All mount points must be in the form "X:\path", where X is a drive letter, 
and path is some folder to attach the volume to. For example "D:\Data" or 
"D:\Data\Data".
- When specifying a Mount Point, cVolume will fail if the Mount Point doesn't 
already exist. It must be created prior to using cVolume.
must

## Versions

### Unreleased

* {{Description of unreleased changes}}

### {{1.0.1.0}}

* {{Description of changes in the specific version}}

### {{1.0.0.0}}

* {{Initial release with the following resources:}}
    * {{Resource1}}
    * {{Resource2}}

## Examples
### {{Example1 title}}

{{Description of example 1}}

### {{Example2 title}}

{{Description of example 2}}