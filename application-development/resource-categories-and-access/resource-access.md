---
layout: default
title: Resource Access
parent: Resource Categories and Access
grand_parent: Application Development
nav_order: 2
---


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