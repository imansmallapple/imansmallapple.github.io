---
layout: default
title: Resource Matching
parent: Resource Categories and Access
grand_parent: Application Development
nav_order: 3
---

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
