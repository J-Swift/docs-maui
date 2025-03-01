---
title: "Haptic Feedback"
description: "Learn how to use the .NET MAUI IHapticFeedback class in the Microsoft.Maui.Devices namespace. This interface lets you control haptic feedback on a device."
ms.date: 09/02/2022
no-loc: ["Microsoft.Maui", "Microsoft.Maui.Devices"]
---

# Haptic feedback

This article describes how you can use the .NET Multi-platform App UI (.NET MAUI) `IHapticFeedback` interface to control haptic feedback on a device. Haptic feedback is generally manifested by a gentle vibration sensation provided by the device to give a response to the user. Some examples of haptic feedback are when a user types on a virtual keyboard or when they play a game where the player's character has an encounter with an enemy character.

The default implementation of the `IHapticFeedback` interface is available through the `HapticFeedback.Default` property. Both the `IHapticFeedback` interface and `HapticFeedback` class are contained in the `Microsoft.Maui.Devices` namespace.

## Get started

To access the haptic feedback functionality, the following platform-specific setup is required.

<!-- markdownlint-disable MD025 -->
# [Android](#tab/android)

The `Vibrate` permission is required and must be configured in the Android project. This can be added in the following ways:

- Add the assembly-based permission:

  Open the _AssemblyInfo.cs_ file under the **Properties** folder and add:

  ```csharp
  [assembly: UsesPermission(Android.Manifest.Permission.Vibrate)]
  ```

  \- or -

- Update the Android Manifest:

  Open the _AndroidManifest.xml_ file under the **Properties** folder and add the following in the `manifest` node:

  ```xml
  <uses-permission android:name="android.permission.VIBRATE" />
  ```

<!-- TODO not yet supported

  \- or -

- Use the Android project properties:

  Right-click on the Android project and open the project's properties. Under _Android Manifest_ find the **Required permissions:** area and check the **VIBRATE** permission. This will automatically update the _AndroidManifest.xml_ file.

-->

# [iOS\macOS](#tab/ios)

No setup is required.

# [Windows](#tab/windows)

No setup is required.

-----
<!-- markdownlint-enable MD025 -->

## Use haptic feedback

The haptic feedback functionality is performed in two modes: a short `Click` or a `LongPress`. The following code example initiates a `Click` or `LongPress` haptic feedback response to the user based on which `Button` they click:

:::code language="csharp" source="../snippets/shared_1/DeviceDetailsPage.xaml.cs" id="hapticfeedback":::
