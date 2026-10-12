**LVM (Logical Volume Management)** in disk partitioning, you're replacing the traditional method of partitioning with a more flexible system that allows you to manage storage across multiple disks. Instead of dealing with fixed partitions, LVM enables you to create and manage **logical volumes (LVs)** that span across multiple **physical volumes (PVs)**.

### How LVM Works in Partitioning:

1. **Physical Volumes (PVs)**: These are the actual physical disks or disk partitions. You can combine several physical volumes into a **volume group (VG)**. This represents a physical storage device or partition(SSD...) that is initialized to be used by LVM.

**Example:** `/dev/sda or /dev/sdb1`.
    
2. **Volume Group (VG)**: The volume group is a pool of storage created by combining multiple physical volumes. Once you create a volume group, you can dynamically allocate space from this pool.

**Example:** `Combine /dev/sda and /dev/sdb1 into a Volume Group called my_vg`.
    
3. **Logical Volumes (LVs)**: These are the "partitions" within a volume group. Logical volumes can span across multiple physical disks and can be resized, extended, or shrunk as needed. Logical Volumes act as partitions that you can format with a[[ filesystem]]

**Example:** `Create a drawer called my_lv inside my_vg`.

[[image(7).webp]]

In **LVM (Logical Volume Management)**, the concepts of **PE (Physical Extent)** and **LE (Logical Extent)** are fundamental to how storage is allocated and managed. Here’s a deeper explanation:

**Physical Extent (PE):**

- **PE** is the smallest unit of storage on a physical volume (PV), which can be a hard drive, SSD, or a partition on a storage device. Think of it as a "chunk" or "block" of space on the physical disk.
- The size of a PE is defined when you create a volume group (VG). For example, if you set the PE size to 4 MB, then the entire disk is divided into 4 MB blocks.
- When data is written to the volume group, it’s stored in these PEs, which help in organizing and managing the data on physical storage.

**Logical Extent (LE):**

- **LE** is the smallest unit of storage on a logical volume (LV). Logical volumes are virtual partitions created inside the volume group.
- LEs map directly to PEs in the physical volume. Each LE corresponds to a PE from the physical volume, so when you create a logical volume, you’re essentially asking the system to allocate a certain number of LEs (from the pool of PEs in the volume group).
- The size of an LE is typically the same as the size of a PE, which ensures that data in the logical volume is stored in a uniform manner.

**How They Work Together:**

- When you create a **Volume Group (VG)**, it’s essentially a pool of storage created from one or more physical volumes (PVs). Each PV is divided into PEs.
- **Logical Volumes (LVs)** are created from this pool of PEs. Each LV is made up of a series of LEs, and each LE maps directly to a PE in the underlying physical volume(s).

**Example:**

- Suppose you have a physical disk `sda` with 1 TB of space, and you set the PE size to 4 MB. The disk is divided into 250,000 PEs.
- When you create a volume group (`vg_data`) with this physical disk, you can then create logical volumes (`lv_root`, `lv_home`, etc.) inside the volume group. These logical volumes will be made up of LEs, which are essentially just pointers to the PEs on the physical disk.

## LVM commands used to manage storage :
### 1. **`pvcreate`**: Create a Physical Volume

- This command is used to prepare a disk or partition to be used in an LVM setup.
- Example:`pvcreate /dev/sda`
- This makes `/dev/sda` available as a physical volume for use in a volume group.
### 2. **`vgcreate`**: Create a Volume Group

- This command creates a volume group (VG) from one or more physical volumes (PVs).
- Example:`vgcreate vg_data /dev/sda`
- This creates a volume group `vg_data` using the physical volume `/dev/sda`.
### 3. **`lvcreate`**: Create a Logical Volume

- This command creates a logical volume (LV) inside a volume group.
- Example:`lvcreate -L 10G -n lv_root vg_data
- This creates a logical volume `lv_root` of size 10GB in the volume group `vg_data`.
### 4. **`lvextend`**: Extend the Size of a Logical Volume

- You can extend a logical volume to add more space from the volume group.
- Example: `lvextend -L +5G /dev/vg_data/lv_root`
- This command adds 5GB to the `lv_root` logical volume.
### 5. **`lvreduce`**: Reduce the Size of a Logical Volume

- This command allows you to shrink a logical volume (note: the volume must have sufficient free space).
- Example:`lvreduce -L -5G /dev/vg_data/lv_root`
- This reduces the size of the `lv_root` logical volume by 5GB.
### 6. **`vgextend`**: Add a Physical Volume to a Volume Group

- This command adds more storage to an existing volume group by adding additional physical volumes.
- Example:`vgextend vg_data /dev/sdb`
- This command adds `/dev/sdb` as a new physical volume to the `vg_data` volume group.
### 7. **`vgreduce`**: Remove a Physical Volume from a Volume Group

- This command removes a physical volume from a volume group.
- Example:`vgreduce vg_data /dev/sdb
- This removes `/dev/sdb` from the `vg_data` volume group.
### 8. **`lvremove`**: Remove a Logical Volume

- This command removes a logical volume.
- Example:
    `lvremove /dev/vg_data/lv_root`
- This deletes the `lv_root` logical volume from the `vg_data` volume group.

### 9. **`vgremove`**: Remove a Volume Group

- This removes a volume group, but only after removing all logical volumes inside it.
- Example:  `vgremove vg_data`
- This deletes the `vg_data` volume group.
### 10. **`pvremove`**: Remove a Physical Volume

- This removes a physical volume from the system.
- Example:`pvremove /dev/sda`
- This removes `/dev/sda` as a physical volume from LVM.