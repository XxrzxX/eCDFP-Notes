# Windows Artifacts 💻

---

## Open Files & Folders

- LNK
- Thumb Cache
- Jump Lists
- Shellbags
- ComDlg32
- OpenSavePidMRU: Files
- RecentDocs

## LNK Files (Shortcuts) - 0x4C

LNK files are data objects that provide a direct link to another object, such as a file, folder, or application on the system.

**File Extension:** `.lnk`

**Forensic Value of LNK Files**

- **Path to the Original File:** Provides the location of the linked file, though not the absolute path.
- **MAC Addresses:** Useful if the file is shared over a network, revealing the MAC address of the host.
- **Network Volume Share Name:** Identifies the network share name if the file is stored on a network.
- **Size of the Target:** Records the size of the linked file at the time it was last accessed.
- **Serial Number of the Volume:** Stores the volume serial number where the file was stored.
- **File Attribute:** Contains attributes of the linked file.
- **Distributed Link Info:** Provides information about distributed links, useful for tracking files across different locations.

**Timestamps**

- **Creation Time:** When the LNK file was first created.
- **Modification Time:** When the LNK file was last altered.

Note: **If the time in the file system matches the time in the LNK file**: This indicates the file was opened only once from the location mentioned in the LNK file's information.

**Where to Find LNK Files?**

You can find LNK files (shortcuts) in the following locations:

- `%USERPROFILE%/Recent`
- `C:\Users\%USERNAME%\AppData\Roaming\Microsoft\Windows\Recent`

These locations store recently accessed shortcuts, making them valuable for forensic analysis.

---

### Thumb Cache

Thumbnails are reduced-size versions of pictures or videos. Windows creates and stores these thumbnails in the thumb cache (e.g., `thumbs.db` or `thumbcache_xxx.db`). This cache helps the system quickly display preview images when you open a folder containing pictures or videos.

**Forensic Value of Thumb Cache** 

- The presence of a thumbnail can indicate that an image or video file was opened or viewed on the system.
- **Version of the Picture:** Helps identify which version of an image was viewed.
- **File Name:** Indicates the name of the image or video file.
- **Date of the Last Modification:** Shows the last time the image or video was modified.

**Where to Find Thumb Cache?**

You can find the thumb cache in these locations:

- `\Users\%USERPROFILE%\AppData\Local\Microsoft\Windows\Explorer`
- `ESE C:\ProgramData\Microsoft\Search\Data\Applications\Windows`

**List of AppID**

[GitHub - List of AppIDs](https://github.com/EricZimmerman/JumpList/blob/master/JumpList/Resources/AppIDs.txt)

---

### Jump Lists

Jump Lists provide users with a list of files accessed by a specific application. Each application has a unique AppID (16 hexadecimal characters).

**Forensic Value of Jump Lists**

- **Check Tasks:** Details about tasks performed by the application.
- **Links to Recent Files:** Access to files that were recently opened by the application.
- **Frequently Used Files:** Insight into files that are accessed frequently.
- **Links to Pinned Files:** Information about files that the user has pinned for easy access.
- **Help in Building a Timeline:** Data that helps reconstruct the sequence of user actions and activities.

**Timestamps in Jump Lists**

- **Access Time:** The last time a file was opened.
- **Creation Time:** When the Jump List entry was created.
- **Modification Time:** When the Jump List entry was last modified.

**Where to Find Jump Lists**

- **AutomaticDestinations:** `\Users\%USERNAME%\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations`
- **CustomDestinations:** `\Users\%USERNAME%\AppData\Roaming\Microsoft\Windows\Recent\CustomDestinations`

---

### Shellbags

Registry entries store information about folder views and can reveal user interactions with directories and drives.

**Forensic Value of Shellbags**

- **Folder Interaction:** Tracks user interactions with folders, including creation, opening, and viewing.
- **Folder Path:** Provides paths to folders, helping identify accessed directories.
- **View Settings:** Stores view settings (e.g., details, icons) that can indicate user preference and activity.
- **Timestamps:** Records timestamps for folder creation, modification, and access.
- **User Behavior:** Helps in understanding the structure and organization of user data and behavior over time.
- **Timeline Reconstruction:** Assists in building a timeline of folder access and modifications, contributing to the overall forensic analysis.

**Where to Find Shellbags**

Shellbags information is stored in the Windows Registry at the following locations:

- **User Shell Folders:** `HKCU\Software\Microsoft\Windows\Shell\Bags`
- **User Shell Folders History:** `HKCU\Software\Microsoft\Windows\Shell\BagMRU`
- **System Shell Folders:** `HKLM\Software\Microsoft\Windows\Shell\Bags`
- **System Shell Folders History:** `HKLM\Software\Microsoft\Windows\Shell\BagMRU`

---

### ComDlg32: Common Dialog Box

The **ComDlg32** file, specifically `comdlg32.ocx`, is part of the Visual Basic Runtime suite and is used by many applications to handle common dialog boxes, such as open and save file dialogs, color picker dialogs, and more.

**Forensic Value of ComDlg32**

- **Dialog Handling:** Facilitates the handling of common dialog boxes, providing insights into user interactions.
- **Execution Tracking:** Helps determine when dialog boxes were accessed and by which applications.
- **Error Diagnostics:** Useful for diagnosing issues related to missing, corrupt, or unregistered files.

**Where to Find ComDlg32**

The **ComDlg32** key is located in the Windows Registry at:

**Registry Path:**

 `HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32`

---

### OpenSavePidMRU: Files

The OpenSavePidMRU registry key tracks files that have been accessed through the "Open" or "Save As" dialog boxes in Windows. 

**Forensic Value of OpenSavePidMRU**

- **File Paths:** Stores the full paths of files accessed through the Open/Save As dialog boxes.
- **MRU Order:** Lists the order in which files were accessed, helping to reconstruct user actions.
- **Timestamps:** Contains timestamps indicating when files were last accessed.
- **File Extensions:** Tracks files based on their extensions, providing a detailed view of user interactions.

**Where to Find OpenSavePidMRU**

The OpenSavePidMRU key is located in the Windows Registry at:

**Registry Path:** `HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePidlMRU`

---

### RecentDocs

The RecentDocs registry key stores information about recently accessed documents. This data is valuable in forensic analysis as it helps in tracking user activity and document access.

**Forensic Value of RecentDocs**

- **Recent Documents:** Provides a list of recently opened documents.
- **File Paths:** Contains the file paths of these documents.
- **Timestamps:** Records when the documents were last accessed, which can help in building a timeline.
- **File Types:** Identifies the types of files that were accessed.

**Where to Find RecentDocs**

RecentDocs information is stored in the Windows Registry at the following location:

- **Registry Path:** `HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`

---

## Execution

- Prefetch Files
- UserAssist
- Application Compatibility Cache (Shim Cache)
- CIDSizeMRU
- Start Menu Run MRUs
- MUI Cache
- BAM
- SRUM
- LNK

### Prefetch Files

Prefetch files are used to reduce the loading time for applications and the system. They capture the first 2 minutes of the boot process and the first 10 seconds of application launches.

**Forensic Value of Prefetch Files**

- **File Name:** Identifies the name of the application.
- **Absolute Path:** Shows the exact location of the application on the system.
- **Number of Runs:** Indicates how many times the application has been executed.
- **Last Time the App Ran:** Records the last time the application was used.
- **List of DLLs Used:** Provides a list of Dynamic Link Libraries utilized by the application.

**Assists In**

- **When the Application Ran:** Helps determine the execution timeline.
- **How Many Times:** Shows the frequency of application use.
- **From Which Path:** Identifies the location from where the application was launched.
- **Created Date:** Records the first time the application was run.
- **Last Modified Date:** Indicates the most recent execution of the application.

**Default Files**

- **Ntosboot-b00Dfaad.pf:** System boot file.
- **Layout.ini:** Used by the disk defragmenter.
- **AgAppLaunch.db:** Generated by the SuperFetch system mechanism.

**Where to Find Prefetch Files**

**Registry Path:** `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\PrefetchParameters`

**EnablePrefetcher Values**

- **0:** Disable Prefetcher.
- **1:** Application launch prefetching enabled.
- **2:** Boot prefetching enabled.
- **3:** Application launch and boot prefetching enabled.

---

### UserAssist Keys

The **UserAssist** key contains information about the executable files and links that you open frequently.

**Forensic Value of UserAssist**

- **Understand Frequency of Program Execution:** Tracks how often each program is executed by the user.
- **Identify the Last Time a Program Was Launched:** Logs the timestamp of the most recent execution of each program.
- **Most Frequently Launched Items:** Lists the items launched most often, giving insights into user behavior.
- **Evidence of Programs After Deletion/Uninstall:** Can provide information about programs that have been deleted or uninstalled.
- **Duration of Interaction with Programs:** Records how long a user interacts with a given program.

**Encoded with ROT13**

The values in the UserAssist key are encoded using ROT13. Here are examples:

- **CEBFF5CD** (translates to **PROSS5PQ**)
- **F4E57C4B** (translates to **S4R57P4O**)

**Where to Find UserAssist**

**Registry Path:** `HKEY_USERS\#\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist`

---

### Application Compatibility Cache (Shim Cache)

The Shim Cache tracks executables that require compatibility settings to run properly. It's stored in memory and only written to the cache during system shutdown.

**Forensic Value of Shim Cache**

- **File Name:** Provides the name of the executable.
- **Full Path:** Indicates the complete path to the executable file.
- **Standard Info Last Modified Date:** Shows the last modified date of the executable.
- **Size of the Binary:** Records the size of the executable file.
- **Execution Status:** Indicates whether the file ran on the system.

**Note:** Even if the file metadata changes, it will still be recorded in the shim cache.

**Where to Find Shim Cache**

- **Registry Path:** `HKLM\SYSTEM\CurrentControlSet\Control\SessionManager\AppCompat\AppCompatCache`
- **File Path:** `%SystemRoot%\AppCompat\Programs\`

---

### CIDSizeMRU

The **CIDSizeMRU** registry key tracks the size and position of the File Explorer screen.

**Forensic Value of CIDSizeMRU**

**Screen Position and Size:** Stores data about the size and position of the File Explorer window, which can be used to understand user interface preferences and usage patterns.

**Where to Find CIDSizeMRU**

The CIDSizeMRU key is located in the Windows Registry at:

**Registry Path:** `Computer\HKEY_USERS\#\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32`

---

### Start Menu Run MRUs

The **RunMRUs** registry key tracks the applications that have been previously executed through the Start menu.

**Forensic Value of RunMRUs**

- **Application Tracking:** Stores a list of applications that have been run via the Start menu's Run dialog, helping to reconstruct user activities.
- **Execution Order:** Maintains the order in which the applications were executed, providing insight into user actions and behaviors.
- **Command History:** Useful for analyzing past commands and scripts executed by the user.

**Where to Find RunMRUs**

The RunMRUs key is located in the Windows Registry at:

**Registry Path:** `Computer\HKEY_USERS\#\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU`

---

### MUI Cache

The **MUI (Multilingual User Interface) Cache** is used by Windows to store metadata about programs, specifically the names of executables and their associated paths, to display them in the user interface in the correct language.

**Forensic Value of MUI Cache**

- **Executable Names and Paths:** Stores the names and paths of recently accessed executable files, helping to track program usage.
- **Localization:** Provides localized names for programs, useful in environments with multiple languages.
- **Timestamp Information:** Can sometimes offer insights into when a program was last accessed.

**Where to Find MUI Cache**

The MUI Cache key is located in the Windows Registry at:

**Registry Path:** `HKEY_USERS\#\Software\Microsoft\Windows\ShellNoRoam\MUICache`

---

### Background Activity Moderator (BAM)

The **Background Activity Moderator (BAM)** is a Windows service introduced in Windows 10. BAM tracks the activity of background applications and provides valuable forensic data.

**Forensic Value of BAM**

- **Full Path of Executables:** Records the full path of executable files that were run on the system.
- **Last Execution Date/Time:** Stores the date and time of the last execution of these files.
- **User-Specific Data:** Each user's executed programs are stored under their corresponding SID (Security Identifier).

**Where to Find BAM**

The BAM registry key is located at:

**Registry Path:** `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\bam\State\UserSettings\{SID}`

---


## Deleted Files & Folders

- Recycle Bin
- Shellbags
- RecentDocs
- LNK file
- Prefetch
- Shim Cache

### Recycle Bin

The Recycle Bin in Windows serves as a temporary storage location for deleted files and folders, allowing users to recover them if needed before they are permanently removed from the system.

**Forensic Value of Recycle Bin**

- **File Name:** Lists the names of deleted files and folders.
- **Original Path:** Indicates the original location of the deleted files.
- **Deletion Date:** Shows the date and time when the files were deleted.
- **File Size:** Records the size of the deleted files.
- **Recovery:** Allows for the recovery of deleted files before permanent deletion.
- **Tracking User Activity:** Provides insights into user behavior and actions related to file management.

**Where to Find Recycle Bin Data**

- **Physical Location:** The Recycle Bin is represented by a hidden system folder located at `C:\$Recycle.Bin` for each drive.
- **Logical Location:**
    - On a standard user profile, the path is usually `C:\$Recycle.Bin\S-1-5-21-<User-SID>\`.
    - Each deleted file is renamed with a unique identifier (e.g., `$Rxxxxxx` for the actual file and `$Ixxxxxx` for its metadata).

---

## Persistence Mechanisms

- Auto-run
- Startup
- Windows service
- Scheduled task

### Auto-Run Registry Keys

The auto-run registry keys are used by Windows to specify programs that should automatically run when the system starts or when a user logs in.

**Forensic Value of Auto-Run Keys**

- **Startup Programs:** These keys store the list of applications that are configured to run at system startup or user login, providing insights into the software environment and potential persistence mechanisms used by malware.
- **Execution Tracking:** Helps determine which programs were configured to run automatically and when they were added.

**Where to Find Auto-Run Keys**

- **Current User Run Key:Registry Path:** `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run`
- **Current User RunOnce Key:Registry Path:** `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce`
- **Local Machine Run Key:Registry Path:** `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run`
- **Local Machine RunOnce Key:Registry Path:** `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce`

---

### Startup Folders

The startup folders in Windows are used to specify programs that should automatically run when a user logs into the system.

**Forensic Value of Startup Folders**

- **Auto-Start Programs:** Lists applications that are configured to run automatically at user login, providing insights into the software environment and potential persistence mechanisms used by malware.
- **User-Specific Data:** Each user's startup folder can contain different programs, offering a detailed view of individual user behaviors.
- **Ease of Access:** These folders are easily accessible and modifiable, making them a common target for both legitimate applications and malicious software.

**Where to Find Startup Folders**

- **User-Specific Startup Folder:Path:** `C:\Users\@Username\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup`
- **All Users Startup Folder:Path:** `C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup`

---

### Windows Services Registry

The **Windows Services** registry key is crucial for managing and configuring services on a Windows system. Services can run in the background and perform essential functions for the operating system and applications.

**Forensic Value of Windows Services Registry**

- **Service Configuration:** Details about service configurations, including startup type, dependencies, and paths to executables.
- **Persistence Mechanisms:** Malicious actors often use services to establish persistence on a system.
- **Execution History:** Provides information about when services were last started or stopped.

**Where to Find Windows Services Registry**

- **Registry Path:** `HKLM\SYSTEM\CurrentControlSet\Services`

This path includes all the service entries and their configurations. Each service has its own subkey within this path, providing detailed information about the service.

---

### Scheduled Tasks

Scheduled tasks in Windows are used to automate various system and application tasks. They are often configured to run at specific times, during certain events, or under specified conditions.

**Forensic Value of Scheduled Tasks**

- **Task Automation:** Provides information about automated tasks, including their schedules, triggers, and actions.
- **System Maintenance and Malicious Activity:** Can reveal both legitimate system maintenance activities and potentially malicious scheduled tasks used for persistence or periodic execution of malware.

**Where to Find Scheduled Tasks**

1. **Registry Locations:**
    - **Tasks Key:Registry Path:** `HKLM\Software\Microsoft\Windows NT\CurrentVersion\Schedule\TaskCache\Tasks`
    - **Tree Key:Registry Path:** `HKLM\Software\Microsoft\Windows NT\CurrentVersion\Schedule\TaskCache\Tree`
2. **File Path:**
    - **Tasks Directory:File Path:** `C:\Windows\System32\Tasks`

---

## Mounted Devices

- USBSTOR
- Mounted Devices
- EMDMgmt

### USBSTOR

The **USBSTOR** registry key stores information about USB storage devices that have been connected to the system. This key is valuable for forensic analysis as it provides detailed information about connected USB devices.

**Forensic Value of USBSTOR**

- **Vendor:** Identifies the manufacturer of the USB device.
- **Product:** Provides the product name or model of the USB device.
- **Revision Number:** Indicates the version or revision of the USB device.

**Where to Find USBSTOR**

**Registry Path:** `HKLM\SYSTEM\ControlSet##\Enum\USBSTOR`

---

### Mounted Devices

The **Mounted Devices** registry key stores information about devices that have been mounted and assigned drive letters on the system.

**Forensic Value of Mounted Devices**

- **Installation Date:** Tracks when the device was installed (found in `reg-key-0064`, `setupapi.log`, `setupapi.dev.log`).
- **Last Connection Date/Time:** Records the last date and time the device was connected (found in `0066`, `NTUSER\Mountpoints2`).
- **Last Removal Date/Time:** Logs the last date and time the device was removed from the system (found in `0067`, `mountpoint2`).
- **GUID and Name:** Stores the GUID and name of the device (found in `System\DeviceClasses`, `\MountedDevices`, `\SOFTWARE\Devices`).

**Where to Find Mounted Devices**

**Registry Path:** `HKLM\SYSTEM\MountedDevices`

---

### EMDMgmt

The **EMDMgmt** registry key is related to **ReadyBoost**, a feature in Windows that allows you to use a USB flash drive to improve system performance by acting as additional memory.

**Forensic Value of EMDMgmt**

- **ReadyBoost Configuration:** Stores information about ReadyBoost settings and USB flash drives used for ReadyBoost.
- **USB Drive Information:** Contains details about all USB drives ever connected to the system, including their write speeds and device status.

**Where to Find EMDMgmt**

**Registry Path:** `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\EMDMgmt`

---

## Network Artifacts

- Network Location Awareness (NLA) Cache
- Managed and Unmanaged Networks
- Network List
- Windows Firewall
- Remote Desktop Connection Settings
- DHCP Config
- RUNMRU

### Network Location Awareness (NLA) Cache

The **Network Location Awareness (NLA)** cache stores information about the networks that the computer has connected to, including domain networks, private networks, and public networks.

**Forensic Value of NLA Cache**

- **Network History:** Keeps a record of the networks the computer has connected to, including the type of network (domain, private, public).
- **Network Identification:** Helps the system identify the type of network it is connected to, which can affect firewall settings and network policies.
- **Network Configuration:** Stores details about network configurations and settings.

**Where to Find NLA Cache**

**Registry Path:** `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Nla\Cache`

---

### Managed and Unmanaged Networks

The **NetworkList** registry key within Windows stores information about both managed and unmanaged network profiles.

**Forensic Value of Managed and Unmanaged Keys**

- **Network Profile Management:** Indicates whether a network profile is managed (1) or unmanaged (0).
- **Network Identification:** Helps identify the type of network (e.g., domain, private, public) and its management status.
- **Network Connections:** Records data about various network connections and their statuses.

**Where to Find Managed and Unmanaged Keys**

**Registry Path:**

- **Managed Network:** `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signature\Managed`
- **Unmanaged Network:** `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signature\Unmanaged`

---

### Network List

The **Network List** registry key within Windows stores information about network profiles, including their types (e.g., wired, wireless) and their status (e.g., public, private).

**Forensic Value of Network Types**

- **Network Profile Identification:** Helps identify the type of network (e.g., wired, wireless, broadband) and its status (e.g., public, private).
- **Network Configuration:** Stores details about network configurations and settings, which can be useful in understanding network usage and policies.

**Types of Networks:**

- **Wired Networks:** Typically represented by IDs such as `6`.
- **Broadband Networks:** Often identified with IDs like `17`.
- **Wireless Networks:** Commonly identified with IDs such as `47`.

**Where to Find Network Types**

**Registry Path:** `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles`

---

### Windows Firewall

The Windows Firewall settings are controlled through various registry keys, each corresponding to different profiles and configurations.

**Forensic Value of Windows Firewall Keys**

- **Profile-Specific Settings:** These keys indicate whether the firewall is enabled or disabled for different network profiles (private, public, domain).
- **System Security Configuration:** Provides insights into the firewall settings and their impact on system security.

**Where to Find Windows Firewall Keys**

- **Private Profile:Registry Path:** `SYSTEM\ControlSet###\Services\SharedAccess\Parameters\FirewallPolicy\StandardProfile\EnableFirewall`
- **Public Profile:Registry Path:** `SYSTEM\ControlSet###\Services\SharedAccess\Parameters\FirewallPolicy\PublicProfile\EnableFirewall`
- **Domain Profile:Registry Path:** `SYSTEM\ControlSet###\Services\SharedAccess\Parameters\FirewallPolicy\DomainProfile\EnableFirewall`
- **Standard Profile:** Applies to user-defined settings and standard profiles.

**Values:**

- **Off = 0:** The firewall is disabled.
- **On = 1:** The firewall is enabled.

---

### Remote Desktop Connection Settings

The **FdenyTSConnections** registry key controls whether Remote Desktop connections are allowed on the system.

**Forensic Value of FdenyTSConnections**

- **Remote Access Control:** Indicates whether Remote Desktop connections are permitted or denied, providing insights into system access policies and configurations.

**Where to Find FdenyTSConnections**

**Registry Path:** `SYSTEM\ControlSet##\Control\Terminal Server\FdenyTSConnections`

**Values:**

- **Off = 1:** Remote Desktop connections are denied (disabled).
- **On = 0:** Remote Desktop connections are allowed (enabled).

---

### DHCP Config

The **DHCP Config** settings in Windows are stored in the registry and provide information about the IP addresses assigned by DHCP to network interfaces.

**Forensic Value of DHCP Config**

- **IP Address Assignment:** Stores details about the IP addresses assigned to network interfaces by DHCP.
- **Network Configuration:** Provides insights into the network configuration and how devices obtain IP addresses.

**Where to Find DHCP Config**

**Registry Path:** `HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces\{GUID}\DhcpIPAddress`

---
