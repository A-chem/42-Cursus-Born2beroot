Is a program that runs when your computer starts up, before the operating system (OS) is loaded.
Its job is to load the OS into memory and start it
## What Does GRUB Do?

The [[BIOS]] or UEFI (which is the software that starts your computer) runs first. It looks for GRUB. Then shows a menu of available operating systems or options to boot into. When you select an option, GRUB loads the kernel (the main part of the operating system) into memory and starts it. After that, your OS runs. GRUB doesn't contain the operating system itself, but it helps find and start the operating system.
## Where is GRUB Installed?

On the hard drive: GRUB is usually installed on your computer's hard drive, specifically in the [[Master Boot Record (MBR)]]

## How They Work Together:

1. **Step 1: BIOS/UEFI Reads the MBR**:
    
    - When the computer starts, the[[ BIOS ]]or UEFI firmware looks for the MBR on the storage device.
    - The MBR contains instructions to load the bootloader (like GRUB).
2. **Step 2: GRUB (or Bootloader) in MBR Points to `/boot`**:
3. 
    - The bootloader then checks the partition table to see where the active partition (the one with the OS) is located.
    - The bootloader in the MBR loads its next stage from the files stored in the **`/boot`** directory.
    - GRUB uses files in **`/boot/grub/`** to present a boot menu and load the kernel.
4. **Step 3: Kernel and System Initialization**:
    
    - Once GRUB (or another bootloader) loads the kernel and initial RAM disk from `/boot`, control is passed to the kernel, which continues the system initialization process.