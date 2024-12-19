# Registry Hives

📍 `C:\Windows\System32\config\`

- `SAM`
- `SOFTWARE`
- `SYSTEM`
- `DEFAULT`

📍 `C:\Users\username\AppData\Local\Microsoft\Windows\NTuser`

- `NTUSER.DAT` (one for each user)

📍 `C:\Users\username\AppData\Local\Microsoft\Windows\UsrClass.dat`

- `USRCLASS.DAT` (one for each user)

# Security Account Manager (SAM)

📍 `C:\Windows\System32\config\SAM`

The SAM file securely stores user account data and is a root key of the `HKEY_LOCAL_MACHINE` hive.

## Content of SAM

- User accounts
- Groups
- User password hashes
- Last logon dates and times
- User logon counts
- SIDs for domain/machine identifiers
- Etc.

### SID

 ![image]()
 
- **S** = Security Identifier
- **1** = Version number
- **5** = Designating authority
- **21** = Identifies this SID globally
- **4170029212-1172637219-35059841** = Domain identifier or machine number
- **1001** = Relative Identifier

### Password Hash and Policy

The SAM file contains the 56-byte NTLM hash of the password.

To determine the password policy in the SAM, check the right nibble of hex offset `0x38`:

- `0`: Active, password required.
- `1`: Account inactive.
- `4`: Password present, but exempt from password policies.
  
  ![image]()



# SOFTWARE

The SOFTWARE file is a root key of the `HKEY_LOCAL_MACHINE` hive.

📍 `C:\Windows\System32\config\SOFTWARE`

## Content of Software Hives

- Installed programs and applications
- Operating system information
- Network information
- File associations
- Logon information
- Attached devices
- Etc.

### Keys

#### Windows Information
`Microsoft\Windows NT\CurrentVersion`

#### User Profiles
`Microsoft\Windows NT\CurrentVersion\ProfileList`

#### Logon Information
- `Microsoft\Windows NT\CurrentVersion\Winlogon`
- `Microsoft\Windows\CurrentVersion\Authentication\LogonUI`

#### Printer
`Microsoft\Windows NT\CurrentVersion\Print\Printers`

#### Install & Uninstall Applications
- **Uninstalled**: `Microsoft\Windows\CurrentVersion\Uninstall`
- **Installed Microsoft Applications**: `Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore`
- **32-bit Applications**: `Software\Wow6432Node`
- **Microsoft Installer Packages**: `Software\Classes\Installer`
- **Windows Built-in Apps**: `Microsoft\Windows\CurrentVersion\Applets`

#### Network
- **Wireless Network Connection**: `Microsoft\Windows NT\CurrentVersion\NetworkList`
- **Installed & Default Internet Browser**: `Software\Clients\StartMenuInternet`

#### Attached Devices
- `Microsoft\Windows Portable Devices\Devices`
- `Microsoft\Windows NT\CurrentVersion\EMDMgmt`



# SYSTEM

The SYSTEM file is a root key of the `HKEY_LOCAL_MACHINE` hive.

📍 `C:\Windows\System32\config\SYSTEM`

**Note:** To investigate the SYSTEM hive, you must first determine the current control set. This step is crucial for understanding which registry settings and configurations are currently active.

## Content of SYSTEM Hive

- System settings
- System configuration
- Services
- Attached devices
- Windows prefetch
- Shim cache/AppCompat cache
- Background activities monitor
- Computer IP
- Etc.

### Keys

#### Current Control Set
`Software\Select`

#### Computer Name
`ControlSet001\Control\ComputerName\ComputerName`

#### Last Shutdown Time
`ControlSet001\Control\Session Manager\Memory Management`

#### Crash Dump Settings and Location
`ControlSet001\Control\CrashControl`

#### Services Set to Run
`Software\ControlSet001\Services`

#### Clear Page File at Shutdown
`ControlSet001\Control\Windows`

#### Prefetch Settings
`ControlSet001\Control\Session Manager\Memory Management\PrefetchParameters`

#### Last Access File Time Settings
`ControlSet001\Control\FileSystem`

#### AppCompat Cache
`ControlSet001\Control\Session Manager\AppCompatCache`

#### Background Activities Monitor (BAM)
`System\ControlSet001\Services\bam`

#### Computer IP
`ControlSet001\Services\Tcpip\Parameters\Interfaces`



# USRClass.dat

📍 `C:\Users\username\AppData\Local\Microsoft\Windows`

The USRClass.dat file is used for storing user-specific registry settings.

## Content of USRClass.dat

- Installed applications for particular user (MuiCache)
- Folder settings and access (ShellBags)
- Microsoft Photo app recent files (ManagedByApp)
- Etc.

### Keys

#### Recent Open Folders
- `Local Settings\Software\Microsoft\Windows\Shell\BagMRU`
- `Local Settings\Software\Microsoft\Windows\Shell\Bags`

#### Installed/Executed Applications for that Particular User
`Local Settings\Software\Microsoft\Windows\Shell\MuiCache`

#### Recent Files (can show what has been accessed in ShellBags)
`Local Settings\Software\Microsoft\Windows\CurrentVersion\AppModel\SystemAppData\##\PersistedStorageItemTable\ManagedByApp`


# Amcache

📍 `C:\Windows\AppCompat\Programs\Amcache`

Amcache is part of the Application Compatibility Cache and stores information about executed programs, including their paths, execution times, and SHA1 hashes.

## Content of Amcache

- Device information
- Application information
- File hashes
- Programs (Windows 10)

### Keys

#### Device Information
`Amcache\Root\DeviceCensus`

#### Applications
`Amcache\Root\InventoryApplication`

#### File Hashes
`Amcache\Root\InventoryApplicationFile`

#### Hardware and Devices Connected to the System
`Amcache\Root\InventoryDevicePnp`

#### Programs
`Amcache\Root\Programs`



# NT user

📍 `C:\Users\username\AppData\Local\Microsoft\Windows\NTuser`

It stores configuration settings for the current user.

## Content of NT user

- Recent opened docx
- Typed URLs
- UserAssist
- Recently used apps
- Run & Run once
- ComDlg32
- RunMRU
- Typed paths
- Microsoft Office MRU
- Word Wheel
- Etc.

### Keys

#### Recent Docs
`Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`

#### UserAssist
`Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist`

#### Recent Apps (can be used with OpenSave)
`Software\Microsoft\Windows\CurrentVersion\Search\RecentApps`

#### Run & RunOnce
- `Software\Microsoft\Windows\CurrentVersion\Run`
- `Software\Microsoft\Windows\CurrentVersion\RunOnce`

#### ComDlg32
- **CIDSizeMRU** (used apps by user): `Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\CIDSizeMRU`
- **FirstFolder** (where programs are installed): `Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\FirstFolder`
- **LastVisitedPidMRU** (identify files in OpenSave): `Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\FirstFolder`
- **OpenSavePidMRU**: `Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\FirstFolder`

#### RunMRU (Win + R Search)
`Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU`

#### Typed Paths
`Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths`

#### Office MRU
`Software\Microsoft\Office`

#### Windows Search
`Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery`