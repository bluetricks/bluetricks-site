# MFT Structure

### Useful Links

* [Microsoft docs - Master File Table](https://learn.microsoft.com/en-us/windows/win32/fileio/master-file-table)
* [MFTEcmd - Zimmermans Tools](https://github.com/EricZimmerman/MFTECmd)
* [Linux-ntfs documentation](https://flatcap.github.io/linux-ntfs/ntfs/concepts/file\_record.html)

## MFT Description

The Master File Table (MFT) is a structure within the NTFS file system that contains metadata about all files stored within the filesystem, this data includes: file size, file location, timestamps and permissions.

## MFT Structure

The MFT contains multiple records, each 1024 bytes in size, within these records there is a mandatory MFT header and multiple optional metadata headers.

### MFT Header

```
struct MFTHeader {
    char[4] magic; //"FILE" for a populated record
    uint16_t update_offset; // Offset for update sequence
    uint16_t update_size; // Size of update sequence
    uint64_t logfile_seq_no; // $LogFile Sequence Number
    uint16_t sequence_no; // Sequence Number
    uint16_t hardlink_count;
    uint16_t offset_first_attrib; // Offset to first attribute
    uint16_t flags;
    uint32_t real_size; // Real size of FILE record
    uint32_t allocated_size; // Allocated size of FILE record
    uint64_t base_file; // File reference to base FILE record
    uint16_t next_attr; // Next attribute ID
    uint16_t padding; // XP ONLY align to 4 byte boundary
    uint32_t record_no; // XP ONLY record number of this entry
}
```

### Attributes

#### 0x10 $STANDARD\_INFORMATION

```
struct standard_information {
    uint64_t create_time;
    uint64_t altered_time;
    uint64_t modified_time;
    uint64_t read_time;
    uint32_t DOS_permissions;
    uint32_t maximum_versions;
    uint32_t version_no;
    uint32_t class_id;
    uint32_t owner_id;
    uint32_t security_id;
    uint64_t quota_charged;
    uint64_t update_seq_no; // Update sequence number

```

#### 0x20 $ATTRIBUTE\_LIST

#### 0x30 $FILE\_NAME

#### 0x80 $DATA



