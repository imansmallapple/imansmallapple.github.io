---
layout: default
title: Resource Categories and Access
parent: Application Development
nav_order: 4
has_children: true
---

Text source from [here](https://github.com/eclipse-oniro-mirrors/docs/blob/OpenHarmony-4.1-Release/en/application-dev/quick-start/resource-categories-and-access.md)

During application development, you may need to use different resources, such as **colors**, **fonts**, **spacing**, and **images**, based on the device or configuration. Depending on the resource type, you can achieve this using the following methods:

- Application resources: configure device- or configuration-specific resources in the resource files.

- System resources: Obtain the ID and configuration-specific values of colors, fonts, or other resources in [Resources](https://gitee.com/openharmony/docs/blob/master/en/design/ux-design/design-resources.md); obtain system icons in [HarmonyOS Symbol](https://developer.huawei.com/consumer/cn/design/harmonyos-symbol/).

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

## Resource Access

### HAP Resources

 - Use **$r** or **$rawfile** to reference resources.<br>To reference resources of the color, float, string, plural, media, or profile type, use the "$r('app.type.name')" format, where **app** indicates the resource defined in the **resources** directory, **type** indicates the resource type or resource save path, and **name** indicates the name you assign to the resource.<br>To reference strings with multiple placeholders in the **string.json** file, use the "$r('app.string.label','aaa','bbb',444)" format.<br>To reference resources in the **rawfile** subdirectory, use the "$rawfile('filename')" format. Wherein **filename** indicates the relative path of a file in the **rawfile** subdirectory, which must contain the file name extension and cannot start with a slash (/).

The usage is as follows:

  ```typescript
    Text('Hello')
    .fontColor($r('sys.color.ohos_id_color_emphasize'))
    .fontSize($r('sys.float.ohos_id_text_size_headline1'))
    .fontFamily($r('sys.string.ohos_id_text_font_family_medium'))
    .backgroundColor($r('sys.color.ohos_id_color_palette_aux1'))

    Image($r('sys.media.ohos_app_icon'))
    .border({
      color: $r('sys.color.ohos_id_color_palette_aux1'),
      radius: $r('sys.float.ohos_id_corner_radius_button'), width: 2
    })
    .margin({
      top: $r('sys.float.ohos_id_elements_margin_horizontal_m'),
      bottom: $r('sys.float.ohos_id_elements_margin_horizontal_l')
    })
    .height(200)
    .width(300)
  ```

- Obtain a **ResourceManager** object through the application context, and then call resource management APIs to access different resources.<br>For example, call **getContext.resourceManager.getStringByNameSync('app.string.XXX')** to obtain string resources; call **getContext.resourceManager.getRawFd('rawfilepath')** to obtain the descriptor of the HAP where the raw file is located, and then use the descriptor ({fd, offset, length}) to access the raw file.

### Cross-HAP/HSP Resources

#### Cross-Bundle Access (for System Applications Only)

- Call **createModuleContext(bundleName, moduleName)** to obtain the context of the target HAP/HSP module in another application. Obtain a **ResourceManager** object through the context, and then call [resource management APIs](../reference/apis-localization-kit/js-apis-resource-manager.md) to access different resources.<br>Example: **getContext.createModuleContext(bundleName, moduleName).resourceManager.getStringByNameSync('app.string.XXX')**

#### Inter-Bundle, Cross-Module Access

- Call **createModuleContext(moduleName)** to obtain the context of the target HAP/HSP module in the same application. Obtain a **ResourceManager** object through the context, and then call resource management APIs to access different resources.<br>Example: **getContext.createModuleContext(moduleName).resourceManager.getStringByNameSync('app.string.XXX').**

- Use **$r** or **$rawfile** to reference resources. Specifically, perform either of the following:

  1. Use *[hsp].type.name*, where **hsp** indicates the HSP module name, **type** indicates the resource type, and **name** indicates the resource name. The following is an example:
  
    ```ts
      Text($r('[hsp].string.test_string'))
        .fontSize($r('[hsp].float.font_size'))
        .fontColor($r('[hsp].color.font_color'))  
      Image($rawfile('[hsp].icon.png'))
    ```
  2. Use variables. The following is an example:

   ```ts
    @Entry
    @Component
    struct Index {
      text: string = '[hsp].string.test_string';
      fontSize: string = '[hsp].float.font_size';
      fontColor: string = '[hsp].color.font_color';
      image: string = '[hsp].media.string';
      rawfile: string = '[hsp].icon.png';
  
      build() {
        Row() {
          Text($r(this.text))
            .fontSize($r(this.fontSize))
            .fontColor($r(this.fontColor))
  
          Image($r(this.image))
  
          Image($rawfile(this.rawfile))
        }
      }
    }
   ```
  > **NOTE**
  >
  > The HSP module name must be placed in the brackets ([]). If the **rawfile** directory contains multiple levels of folders, the path must start from the first level, for example, **\$rawfile('[hsp].oneFile/twoFile/icon.png')**. When **$r** or **$rawfile** is used for cross-HSP resource access, resource verification is not available at compile time, and you need to manually check that the target resources exist in the corresponding location.

### System Resources

Apart from custom resources, you can use system resources to develop different applications with the same visual style. For details about the system resource IDs and their values in different configurations, see [Resources](../../design/ux-design/design-resources.md).

During development, the usage of layered parameters is basically the same as that of qualifiers. To reference a system resource, use the "$r('sys.type.resource_id')" format. Wherein: **sys** indicates a system resource; **type** indicates the resource type, which can be **color**, **float**, **string**, or **media**; **resource_id** indicates the resource ID.

> **NOTE**
>
> - The use of system resources is only supported in the declarative development paradigm.
>
> - For preset applications, you are advised to use system resources. For third-party applications, you can choose to use system resources or custom application resources as required.

  ```ts
    Text('Hello')
    .fontColor($r('sys.color.ohos_id_color_emphasize'))
    .fontSize($r('sys.float.ohos_id_text_size_headline1'))
    .fontFamily($r('sys.string.ohos_id_text_font_family_medium'))
    .backgroundColor($r('sys.color.ohos_id_color_palette_aux1'))

    Image($r('sys.media.ohos_app_icon'))
    .border({
      color: $r('sys.color.ohos_id_color_palette_aux1'),
      radius: $r('sys.float.ohos_id_corner_radius_button'), width: 2
    })
    .margin({
      top: $r('sys.float.ohos_id_elements_margin_horizontal_m'),
      bottom: $r('sys.float.ohos_id_elements_margin_horizontal_l')
    })
    .height(200)
    .width(300)
  ```

## Resource Matching

When your application needs to use a resource, the system preferentially searches the qualifiers subdirectories that match the current device state. The system searches the **base** subdirectory for the target resource only when the **resources** directory does not contain any qualifiers subdirectories that match the current device state or the target resource is not found in the qualifiers subdirectories. The **rawfile** directory is not searched for resources.

**Rules for Matching Qualifiers Subdirectories and Device Resources**

- Qualifiers are matched with the device resources in the following priorities: MCC&MNC > locale (options: language, language_script, language_country/region, and language_script_country/region) > screen orientation > device type > color mode > screen density

- If the qualifiers subdirectories contain the MCC, MNC, language, script, screen orientation, device type, and color mode qualifiers, their values must be consistent with the current device status so that the subdirectories can be used for matching the device resources. For example, the qualifiers subdirectory **zh_CN-car-ldpi** cannot be used for matching the resource files labeled **en_US**.

For more information about how resources are loaded in applications, see the internationalization and localization documents.

**Overlay Mechanism**

Overlay is a resource replacement mechanism. With overlay resource packages, you enable your application GUI to adapt to different styles of various brands and products, without having to repack your application HAPs. The overlay mechanism works in dynamic and static modes. Overlay resource packages contain only resource files, resource index files, and configuration files.

- Using overlay in dynamic mode

1. Place the overlay resource package in the target application installation path and install the package using **hdc install**. For example, for the com.example.overlay application, place the overlay resource package in **data/app/el1/bundle/public/com.example.overlay/**.

2. The application uses [addResource(path)](../reference/apis-localization-kit/js-apis-resource-manager.md#addresource10) to load overlay resources and uses [removeResource(path)](../reference/apis-localization-kit/js-apis-resource-manager.md#removeresource10) to remove overlay resources. The path to an overlay resource consists of the application's sandbox root directory (obtained through **getContext().BundleCodeDir**) and the overlay resource package name. For example, **let path = getContext().bundleCodeDir + "Overlay resource package name"**, such as **/data/storage/el1/bundle/overlayResourcePackageName**.

- Using overlay in static mode

The **module.json5** file in the inter-application overlay resource package supports the following fields:
```{
  "app":{
    "bundleName": "com.example.myapplication.overlay",
    "vendor" : "example",
    "versinCode": "1000000",
    "versionName": "1.0.0.1",
    "icon": "$media:app_icon",
    "label": "$string:app_name",
  },
  "module":{
    "name": "entry_overlay_module_name",
    "type": "shared",
    "description": "$string:entry_overlay_desc",
    "deviceTypes": [
      "default",
      "tablet",
    ],
    "deliverywithInstall": true,

    "targetModuleName": "entry_module_name",
    "targetPriority": 1,
  }
}
```

The **module.json5** file in the cross-application overlay resource package supports the following fields, which are available for system applications only:
```{
  "app":{
    "bundleName": "com.example.myapplication.overlay",
    "vendor" : "example",
    "versinCode": "1000000",
    "versionName": "1.0.0.1",
    "icon": "$media:app_icon",
    "label": "$string:app_name",
    "targetBundleName": "com.example.myapplication",
    "targetPariority": 1,
  },
  "module":{
    "name": "entry_overlay_module_name",
    "type": "shared",
    "description": "$string:entry_overlay_desc",
    "deviceTypes": [
      "default",
      "tablet",
    ],
    "deliverywithInstall": true,

    "targetModuleName": "entry_module_name",
    "targetPriority": 1,
  }
}
```
> **NOTE**
> - **targetBundleName**: name of the target application to apply the overlay feature. The value is a string.
>
> - **targetModuleName**: name of the target module to apply the overlay feature. The value is a string.
>
> - **targetPriority**: overlay priority. The value is an integer.
>
> - Other fields such as **Ability**, **ExtensionAbility**, and **Permission** are not supported.
>
> - The overlay feature does not support JSON images.

If the **module.json5** file of a module contains the **targetModuleName** and **targetPriority** fields during project creation on DevEco Studio, the module is identified as a module with the overlay feature in the installation phase. Modules with the overlay feature generally provide an overlay resource file for other modules on the device, so that the module specified by **targetModuleName** can display different colors, labels, themes, and the like by using the overlay resource file in a running phase.

The overlay feature is enabled by default. For details about how to enable and disable this feature, see [@ohos.bundle.overlay (overlay)](../reference/apis-ability-kit/js-apis-overlay.md).
