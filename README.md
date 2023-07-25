[![pt-br](https://img.shields.io/badge/lang-pt--br-green.svg)](https://github.com/lucianothesilva/CustomWindows10Iso/blob/main/README.pt-br.md)
[![es](https://img.shields.io/badge/lang-es-yellow.svg)](https://github.com/lucianothesilva/CustomWindows10Iso/blob/main/README.es.md)


**How to create a custom Windows 10 ISO with pre-installed software.**

Necessary Software:

**Windows ADK for Windows 10 (Deployment Tools):** Please ensure that you download the correct version of the Windows ADK for your Windows 10 version (e.g., Windows 10 version 1909, 20H2, etc.)
   - [Download Windows ADK](https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit)

**Rufus (To Create Bootable USB):**
   - [Download Rufus](https://rufus.ie/)


1. **Format a Machine and Install Software:**
   - Format the machine and create a local account with the desired name.
   - Install the necessary programs and remove bloatware.

2. **Run Disk Cleanup:**
   - Open Disk Cleanup (Search for "Disk Cleanup" in the Start menu).
   - Select the system files you want to clean up and proceed.

3. **Reduce C:\ Drive Size and Create New Partition:**
   - Press Windows key + X and select "Disk Management."
   - Right-click on the C:\ drive (usually labeled "OS (C:)") and choose "Shrink Volume."
   - Enter the desired amount to shrink and create unallocated space.
   - Right-click on the unallocated space and select "New Simple Volume."
   - Assign the drive letter "D" and label it "Image."

4. **Create Folders on D:\ Drive:**
   - Open File Explorer (Win + E) and navigate to the D:\ drive.
   - Right-click an empty area and choose "New" > "Folder."
   - Name the folder "Scratch."
   - Create another folder named "iso_files."

5. **Shut Down the Machine:**
   - Save your work and close all applications.
   - Click on Start > Power > Shut Down.

6. **Boot from Windows USB Drive and Open Command Prompt:**
   - Insert the Windows USB drive and restart your machine.
   - Access the BIOS or boot menu (usually F2, F12, Esc, or Del) during startup.
   - Select the USB drive as the boot device.
   - On the Windows setup screen, press Shift + F10 to open the Command Prompt.

7. **Capture Image in .wim Format:**
   - In the Command Prompt, run the following command:
     ```
     dism /capture-image /imagefile:D:\install.wim /capturedir:C:\ /ScratchDir:D:\Scratch /name:Windows10 /compress:maximum /checkintegrity /verify /bootable
     ```

8. **Mount Windows ISO and Copy Contents:**
   - Mount a Windows ISO (matching the installed version) on your machine.
   - Copy the "Windows10.wim" file from the mounted ISO to "D:\iso_files\Sources" and replace the existing file.

9. **Download and Install Windows ADK:**
   - Download the Windows ADK for Windows 10 from [Microsoft's website](https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit) if you haven't already.

10. **Run Deployment Tools as Administrator:**
    - Run the "Deployment and Imaging Tools Environment" as an Administrator.

11. **Create Customized ISO:**
    - In the opened prompt, run the following command:
      ```
      oscdimg.exe -m -o -u2 -udfver102 -bootdata:2#p0,e,bd:\iso_files\boot\etfsboot.com#pEF,e,bd:\iso_files\efi\microsoft\boot\efisys.bin d:\iso_files d:\Windows10Inside.iso
      ```

12. **Use Rufus to Create Bootable USB:**
    - Use the Rufus tool to create a bootable USB using the customized ISO.
  
13. **Use the bootable USB in you machines 🙂**
