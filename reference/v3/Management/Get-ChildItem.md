---
external help file: PSITPro3_Management.xml
schema: 2.0.0
---

# Get-ChildItem
## SYNOPSIS
Gets the items and child items in one or more specified locations.

## SYNTAX

### UNNAMED_PARAMETER_SET_1
```
Get-ChildItem [[-Path] <String[]>] [[-Filter] <String>] [-Exclude <String[]>] [-Force] [-Include <String[]>]
 [-Name] [-Recurse] [-UseTransaction]
```

### UNNAMED_PARAMETER_SET_2
```
Get-ChildItem [[-Filter] <String>] [-Exclude <String[]>] [-Force] [-Include <String[]>] [-Name] [-Recurse]
 -LiteralPath <String[]> [-UseTransaction]
```

## DESCRIPTION
The Get-ChildItem cmdlet gets the items in one or more specified locations.
If the item is a container, it gets the items inside the container, known as child items.
You can use the Recurse parameter to get items in all child containers.

A location can be a file system location, such as a directory, or a location exposed by a different Windows PowerShell provider, such as a registry hive or a certificate store.

## EXAMPLES

### -------------------------- EXAMPLE 1 --------------------------
```
PS C:\>Get-ChildItem
```

This command gets the child items in the current location.
If the location is a file system directory, it gets the files and sub-directories in the current directory.
If the item does not have child items, this command returns to the command prompt without displaying anything.

The default display lists the mode \(attributes\), last write time, file size \(length\), and the name of the file.
The valid values for mode are d \(directory\), a \(archive\), r \(read-only\), h \(hidden\), and s \(system\).

### -------------------------- EXAMPLE 2 --------------------------
```
PS C:\>Get-ChildItem –Path *.txt -Recurse -Force
```

This command gets all of the .txt files in the current directory and its subdirectories.
The Recurse parameter directs Windows PowerShell to get objects recursively, and it indicates that the subject of the command is the specified directory and its contents.
The Force parameter adds hidden files to the display.

To use the Recurse parameter on Windows PowerShell 2.0 and earlier versions of Windows PowerShell, the value use the Path parameter must be a container.
Use the Include parameter to specify the .txt file type.
For example, Get-ChildItem –Path .\* -Include *.txt -Recurse

### -------------------------- EXAMPLE 3 --------------------------
```
PS C:\>Get-ChildItem –Path C:\Windows\Logs\* -Include *.txt -Exclude A*
```

This command lists the .txt files in the Logs subdirectory, except for those whose names start with the letter A.
It uses the wildcard character \(*\) to indicate the contents of the Logs subdirectory, not the directory container.
Because the command does not include the Recurse parameter, Get-ChildItem does not include the content of directory automatically; you need to specify it.

### -------------------------- EXAMPLE 4 --------------------------
```
PS C:\>Get-ChildItem –Path HKLM:\Software
```

This command gets all of the registry keys in the HKEY_LOCAL_MACHINE\SOFTWARE key in the registry of the local computer.

### -------------------------- EXAMPLE 5 --------------------------
```
PS C:\>Get-ChildItem -Name
```

This command gets only the names of items in the current directory.

### -------------------------- EXAMPLE 6 --------------------------
```
PS C:\>Import-Module Microsoft.PowerShell.Security
PS C:\>Get-ChildItem –Path Cert:\* -Recurse -CodeSigningCert
```

This command gets all of the certificates in the Windows PowerShell Cert: drive that have code-signing authority.

The first command imports the Microsoft.PowerShell.Security module into the session.
This module includes the Certificate provider that creates the Cert: drive.

The second command uses the Get-ChildItem cmdlet.
The value of the Path parameter is the Cert: drive.
The Recurse parameter requests a recursive search.
The CodeSigningCertificate parameter is a dynamic parameter that the Certificate provider adds to the Get-ChildItem cmdlet.
This parameter gets only certificates that have code-signing authority.

For more information about the Certificate provider and the Cert: drive, go to http://go.microsoft.com/fwlink/?LinkID=113433http://go.microsoft.com/fwlink/?LinkID=113433 or use the Update-Help cmdlet to download the help files for the Microsoft.PowerShell.Security module and then type "Get-Help Certificate".

### -------------------------- EXAMPLE 7 --------------------------
```
PS C:\>Get-ChildItem –Path C:\Windows –Include *mouse* -Exclude *.png
```

This command gets all of the items in the C:\Windows directory and its subdirectories that have "mouse" in the file name, except for those with a .png file name extension.

## PARAMETERS

### -Exclude
Omits the specified items.
The value of this parameter qualifies the Path parameter.
Enter a path element or pattern, such as "*.txt".
Wildcards are permitted.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: 
Accept pipeline input: false
Accept wildcard characters: True
```

### -Filter
Specifies a filter in the provider's format or language.
The value of this parameter qualifies the Path parameter.
The syntax of the filter, including the use of wildcards, depends on the provider.
Filters are more efficient than other parameters, because the provider applies them when retrieving the objects, rather than having Windows PowerShell filter the objects after they are retrieved.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: 2
Default value: 
Accept pipeline input: false
Accept wildcard characters: True
```

### -Force
Allows the cmdlet to get items that cannot otherwise not be accessed by the user, such as hidden or system files.
Implementation varies among providers.
For more information, see about_Providers \(http://go.microsoft.com/fwlink/?LinkID=113250\).
Even when using the Force parameter, the cmdlet cannot override security restrictions.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: False
Accept pipeline input: false
Accept wildcard characters: False
```

### -Include
Gets only the specified items.
The value of this parameter qualifies the Path parameter.
Enter a path element or pattern, such as "*.txt".
Wildcards are permitted.

The Include parameter is effective only when the command includes the Recurse parameter or the path leads to the contents of a directory, such as C:\Windows\*, where the wildcard character specifies the contents of the C:\Windows directory.

```yaml
Type: String[]
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: 
Accept pipeline input: false
Accept wildcard characters: True
```

### -LiteralPath
Specifies a path to one or more locations.
Unlike the Path parameter, the value of the LiteralPath parameter is used exactly as it is typed.
No characters are interpreted as wildcards.
If the path includes escape characters, enclose it in single quotation marks.
Single quotation marks tell Windows PowerShell not to interpret any characters as escape sequences.

```yaml
Type: String[]
Parameter Sets: UNNAMED_PARAMETER_SET_2
Aliases: PSPath

Required: True
Position: Named
Default value: 
Accept pipeline input: true (ByValue, ByPropertyName)
Accept wildcard characters: False
```

### -Name
Gets only the names of the items in the locations.
If you pipe the output of this command to another command, only the item names are sent.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: 
Accept pipeline input: false
Accept wildcard characters: False
```

### -Path
Specifies a path to one or more locations.
Wildcards are permitted.
The default location is the current directory \(.\).

```yaml
Type: String[]
Parameter Sets: UNNAMED_PARAMETER_SET_1
Aliases: 

Required: False
Position: 1
Default value: Current directory
Accept pipeline input: true (ByValue, ByPropertyName)
Accept wildcard characters: True
```

### -Recurse
Gets the items in the specified locations and in all child items of the locations.

In Windows PowerShell 2.0 and earlier versions of Windows PowerShell, the Recurse parameter works only when the value of the Path parameter is a container that has child items, such as C:\Windows or C:\Windows\*, and not when it is an item does not have child items, such as C:\Windows\*.exe.

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: False
Accept pipeline input: false
Accept wildcard characters: False
```

### -UseTransaction
Includes the command in the active transaction.
This parameter is valid only when a transaction is in progress.
For more information, see Includes the command in the active transaction.
This parameter is valid only when a transaction is in progress.
For more information, see

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: false
Accept pipeline input: false
Accept wildcard characters: False
```

## INPUTS

### System.String
You can pipe a string that contains a path to Get-ChildItem.

## OUTPUTS

### System.Object
The type of object that Get-ChildItem returns is determined by the objects in the provider drive path.

### System.String
If you use the Name parameter, Get-ChildItem returns the object names as strings.

## NOTES
You can also refer to Get-ChildItem by its built-in aliases, "ls", "dir", and "gci".
For more information, see about_Aliases.

Get-ChildItem does not get hidden items by default.
To get hidden items, use the Force parameter.

The Get-ChildItem cmdlet is designed to work with the data exposed by any provider.
To list the providers available in your session, type "Get-PSProvider".
For more information, see about_Providers \(http://go.microsoft.com/fwlink/?LinkID=113250\).

## RELATED LINKS

[Online Version:](http://go.microsoft.com/fwlink/?LinkID=113308)

[Get-Alias](00000000-0000-0000-0000-000000000000)

[Get-Item](4ed2b1e1-fde4-4425-90a0-87774477fefa)

[Get-Location](b4c8d674-ba23-4bdf-8322-1f08acdc0ca9)

[Get-Process](b30db241-c0f6-40d3-ab3b-ab86342b36c1)

[about_Providers](55e2974f-3314-48d2-8b1b-abdea6b303cb)

