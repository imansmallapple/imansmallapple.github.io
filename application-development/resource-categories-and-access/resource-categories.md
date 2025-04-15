---
layout: default
title: Resource Categories
parent: Resource Categories and Access
grand_parent: Application Development
nav_order: 1
---

## Resource Categories

Resource files used during application development must be stored in specified directories for management. There are two types of resource directories, namely, resource directories and resource group directories. 
The resource directories are the **base**, qualifiers, **rawfile**, and **resfile** directories. The resource group directories are the **element**, **media**, and **profile** directories.

> **NOTE**
>
> The common resource files used across projects in the stage model are stored in the **resources** directory under **AppScope**.

Example of the **resources** directory:
```
resources
|---base
|   |---element
|   |   |---string.json
|   |---media
|   |   |---icon.png
|   |---profile
|   |   |---test_profile.json
|---en_US  // Default directory. When the device language is en-us, resources in this directory are preferentially matched.
|   |---element
|   |   |---string.json
|   |---media
|   |   |---icon.png
|   |---profile
|   |   |---test_profile.json
|---zh_CN  // Default directory. When the device language is zh-cn, resources in this directory are preferentially matched.
|   |---element
|   |   |---string.json
|   |---media
|   |   |---icon.png
|   |---profile
|   |   |---test_profile.json
|---en_GB-vertical-car-mdpi // Example of a qualifiers directory, which needs to be created on your own.
|   |---element
|   |   |---string.json
|   |---media
|   |   |---icon.png
|   |---profile
|   |   |---test_profile.json
|---rawfile // Other types of files are saved as raw files and will not be integrated into the resources.index file. You can customize the file name as needed.
|---resfile // Other types of files are saved as raw files and will not be integrated into the resources.index file. You can customize the file name as needed.
```
### Resource Directories

#### base Directory

The **base** directory is provided by default. Under this directory, the **element** subdirectory stores basic elements such as strings, colors, and boolean values, and the **media** and **profile** subdirectories store resource files such as media, animations, and layouts.<br>
Resource files in the subdirectories are compiled into binary files, and each resource file is assigned an ID. Resource files in the subdirectory are referenced based on the resource type and resource name.

#### Qualifiers Directory

**en_US** and **zh_CN** are two default qualifiers directories. You need to create other qualifiers directories on your own. Under this directory, the subdirectories store basic elements such as strings, colors, and boolean values, as well as resource files such as media, animations, and layouts.<br>Resource files in the subdirectories are compiled into binary files, and each resource file is assigned an ID. Resource files in the subdirectories are referenced based on the resource type and resource name.

#### rawfile Directory

You can create multiple levels of subdirectories with custom names to store various resource files.<br>Resource files in the subdirectories are directly packed into the application without being compiled, and no IDs will be assigned to the resource files. The subdirectories are referenced based on the specified file path and file name.

#### resfile Directory

You can create multiple levels of subdirectories with custom names to store various resource files.<br>Resource files in the subdirectories are directly packed into the application without being compiled, and no IDs will be assigned to the resource files. After an application is installed, the **resfile** directory is decompressed to the application sandbox path. You can obtain the path through the resourceDir attribute of **Context**.

### Resource Group Directories

Resource group directories include **element**, **media**, and **profile**, which are used to store resources of specific types.

  **Table 3** Resource group directories

| Directory   | Description                                    | Resource File                                    |
| --------- | ---------------------------------------- | ---------------------------------------- |
| element | Element resources. Each type of data is represented by a JSON file. (Only files are supported in this directory.) The options are as follows:<br>- **boolean**: boolean data<br>- **color**: color data<br>- **float**: floating point number ranging from -2^128 to 2^128<br>- **intarray**: array of integers<br>- **integer**: integer ranging from -2^31 to 2^31-1<br>- **pattern**: style (for system applications only) <br>- **plural**: plural form data<br>- **strarray**: array of strings<br>- **string**: string in the specified format.<br>- theme: theme (for system applications only) | It is recommended that files in the **element** subdirectory be named the same as the following files, each of which can contain only data of the same type:<br>- boolean.json<br>- color.json<br>- float.json<br>- intarray.json<br>- integer.json<br>- pattern.json<br>- plural.json<br>- strarray.json<br>- string.json |
| media   | Indicates media resources, including non-text files such as images, audios, and videos. (Only files are supported in this directory.)<br>Table 4 and Table 5 describe the types of images, audios, and videos.             | The file name can be customized, for example, **icon.png**.                    |
| profile  | Indicates a custom configuration file. (Only JSON files are supported in this directory.)      | The file name can be customized, for example, **test_profile.json**.          |

**Media Resource Types**

Table 4 Image resource types

| Format  | File Name Extension|
| ---- | ----- |
| JPEG | .jpg  |
| PNG  | .png  |
| GIF  | .gif  |
| SVG  | .svg  |
| WEBP | .webp |
| BMP  | .bmp  |

Table 5 Audio and video resource types

| Format                                  | File Name Extension        |
| ------------------------------------ | --------------- |
| H.264 AVC |.3gp |
| Baseline Profile (BP) | .mp4   |

**Resource File Examples**

The content of the **color.json** file is as follows:

```json
{
    "color": [
        {
            "name": "color_hello",
            "value": "#ffff0000"
        },
        {
            "name": "color_world",
            "value": "#ff0000ff"
        }
    ]
}
```

The content of the **float.json** file is as follows:

```json
{
    "float":[
        {
            "name":"font_hello",
            "value":"28.0fp"
        },
        {
            "name":"font_world",
            "value":"20.0fp"
        }
    ]
}
```

The content of the **string.json** file is as follows:

```json
{
    "string":[
        {
            "name":"string_hello",
            "value":"Hello"
        },
        {
            "name":"string_world",
            "value":"World"
        },
        {
            "name":"message_arrive",
            "value":"We will arrive at %1$s."
        },
        {
            "name":"message_notification",
            "value":"Hello, %1$s!,You have %2$d new messages."
        }
    ]
}
```

The content of the **plural.json** file is as follows:

```json
{
    "plural":[
        {
            "name":"eat_apple",
            "value":[
                {
                    "quantity":"one",
                    "value":"%d apple"
                },
                {
                    "quantity":"other",
                    "value":"%d apples"
                }
            ]
        }
    ]
}
```
