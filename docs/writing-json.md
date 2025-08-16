# Writing JSON file
Almost all fields of JSON file are simple. You can take [an example file](https://github.com/sk1project/wixpy/blob/master/samples/wixpy.json)
and modify it for your application. Paths can be absolute or relative. Some field 
description you could find below: 


## "Name" field
Application name. String value.

## "ProductCode" field
Unique product GUID. The field is optional. If not specified the product id will
be generated. String value. For example, "3AC4B4FF-19C5-4B8F-83AD-BAC3238BF690".

## "UpgradeCode" field
Unique GUID used your application to identify itself. Should be the same for all 
application versions. String value. For example, "3AC4B4FF-19C5-4B8F-83AD-BAC3238BF690".

## "Version" field
Application version in format "1.1","1.1.1", "1.1.1.111". Cannot contains any
letters, i.e. versions like "1.1alpha" or "2.3b4" are not valid. String value.

## "Manufacturer" field
Your company/project name. String value.

## "Description" field
Application description. Optional string value. Default is "---"

## "Comments" field
Some comments about application. Suitable app license. Optional string value. 
Default is "-"

## "Keywords" field
Application search keywords for Windows desktop search. Comma separated.
Optional string value. Default is "---"

## "Win64" field
64-bit application identifier. Optional boolean value. Default value "false".
If true application will be installed in 64bit `Program Files` folder. If false,
there will be 32bit `Program Files (x86)` folder.

## "Codepage" field
Installer encoding for file names and messages. Optional string value. Default
is "1252"

## "SummaryCodepage" field
Installer summary encoding. Optional string value. Default is "1252"

## "Language" field
The [Microsoft Windows Language Code identifier](https://msdn.microsoft.com/en-us/library/cc233965.aspx)
used by installer. Optional string value. Default is "1033"

## "Languages" field
The list of language IDs (LCIDs) supported in the package. Optional string value. 
Default is "1033"

## "_OsCondition" field
Minimally suitable OS version. Optional string value. If presents MSI installer 
checks OS version compatibility. Possible values: 

| Code  | OS                                  |
| ----- | ----------------------------------- |
| 501   | Windows XP, Windows Server 2003     |
| 502   | Windows Server 2003                 |
| 600   | Windows Vista, Windows Server 2008  |
| 601   | Windows 7, Windows Server 2008R2    |
| 602   | Windows 8, Windows Server 2012      |
| 603   | Windows 8.1, Windows Server 2012 R2 |
| 1000  | Windows 10, Windows Server 2016     |


## "_CheckX64" field
64bit OS check. Optional boolean value. Default is 'false'. If true installer 
checks OS architecture value.
 
## "_Conditions" field
Optional list of custom conditions. Looks like:
```
 "_Conditions": [[msg, condition, level],
                 [msg, condition, level]]
```

## "_AppIcon" field
Path to installer icon. Optional string value. If not presents, installer icon
will be default MSI icon.

## "_Icons" field
Optional list of icon paths.

## "_ProgramMenuFolder" field
Name of application folder in `Program Menu`. Optional string value.

## "_Shortcuts" field
This field is a most complex because it can contains file associations. 
The field is a list of shortcut definitions. In simple case this will be:

```
  "_Shortcuts": [
      {"Name": "WiX.Py",
       "Description": "Cross-platform MSI builder",
       "Target": "wix.py.exe"
       }
   ]
```

Target is an installation directory relative value, i.e. this will be equal to
`[INSTALL_DIR]\wix.py.exe`

To place shortcut on desktop too just add according flag:

```
  "_Shortcuts": [
      {"Name": "WiX.Py",
       "Description": "Cross-platform MSI builder",
       "Target": "wix.py.exe",
       "AddOnDesktop": true
       }
   ]
```

If you need associating some file extensions with your application in `Open With`
Explorer context submenu, just add list of desired extensions:

```
  "_Shortcuts": [
      {"Name": "WiX.Py",
       "Description": "Cross-platform MSI builder",
       "Target": "wix.py.exe",
       "OpenWith": [".png", ".svg", ".jpg"]
       }
   ]
```

And last option is adding new file type to the Windows registry using "Open" field:

```
  "_Shortcuts": [
      {"Name": "WiX.Py",
       "Description": "Cross-platform MSI builder",
       "Target": "wix.py.exe",
       "Open": [{"Extension": ".json",
                 "Descriptrion": "File \"JSON\"",
                 "IconIndex": "0",
                 "EditWith": false,
                 "MIME": "application/json"}],
       }
   ]
```

The field value is a list of dicts. So you could define several file types 
associated with your application. "IconIndex" is an icon index inside your 
application binary. "EditWith" is a flag to add `Edit With <app name>` Explorer
context menu item. "MIME" - correct [media type description ](https://en.wikipedia.org/wiki/Media_type)


## "_AddToPath" field
List of relative paths in installation folder. Adds paths at the end of 
system PATH environmental variable. For example to add installation folder into 
system PATH this will be:
```
 "_AddToPath": [""]
```
Optional list value.

## "_AddBeforePath" field
The same as  "_AddToPath" but adds paths at the start of system PATH 
environmental variable. Optional list value.

## "_SourceDir" field
Absolute or relative path to application source folder.

## "_InstallDir" field
Name of installation folder.

## "_OutputName" field
Name of created MSI installer.

## "_OutputDir" field
Absolute or relative folder path where to save created MSI installer

## "_SkipHidden" field
Option to skip hidden Unix files which names start with "." Default value "true" 

---

[Return to help TOC](https://wix.sk1project.net/docs.php)