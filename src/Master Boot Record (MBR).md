The MBR is a small but important piece of code that is located at the beginning of a storage device. It serves as a "starting point" for the computer to boot up(the very first 512 bytes).
## MBR Structure

- **Bootloader Code (first 446 bytes):** This is the part that runs first when the computer is powered on and starts the process of loading the operating system.

- **Partition Table (next 64 bytes):** This part contains the information about the partitions on the disk, including which partition is marked as active (the one you want to boot from).

- **Boot Signature (last 2 bytes):** These are specific bytes (0x55AA) that indicate the disk has a valid MBR.