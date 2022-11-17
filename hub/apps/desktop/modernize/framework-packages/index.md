---
description: Learn about using MSIX framework packages dynamically from your desktop app.
title: Use MSIX framework packages dynamically from your desktop app
ms.topic: article
ms.date: 07/30/2021
ms.localizationpriority: medium
---

# Use MSIX framework packages dynamically from your desktop app

The [Windows App SDK](../../../windows-app-sdk/index.md) and the Windows 11 OS both enable your apps to reference and use [MSIX framework packages](framework-packages-overview.md) dynamically at run time by using a feature called *dynamic dependencies*. This feature is intended to be used primarily by unpackaged desktop apps to use APIs and other content provided by MSIX framework packages.

The most common scenario for using the dynamic dependencies feature is to reference the [Windows App SDK](../../../windows-app-sdk/index.md) framework package in an unpackaged app. In some scenarios, you may want to use the dynamic dependencies feature to reference a different framework package from an unpackaged app, such as the framework package for [WinUI 2](../../../winui/winui2/index.md) or the DirectX Runtime.

For an overview of the dynamic dependencies feature and guidance about using it in your apps, see the following articles.

| Article | Description |
|---------|-------------|
|  [MSIX framework packages and dynamic dependencies](framework-packages-overview.md) | Introduces important concepts related to MSIX framework packages and describes the purpose of dynamic dependencies feature. This article includes details about the package graph for framework package references and the servicing model for framework packages. |
|  [Use the Windows App SDK runtime for apps packaged with external location or unpackaged](../../../windows-app-sdk/use-windows-app-sdk-run-time.md) | Describes how to use dynamically take a dependency on the Windows App SDK framework package in an unpackaged app at run time. This scenario enables unpackaged apps to use Windows App SDK features.   |
|  [Reference framework packages at run time](use-the-dynamic-dependency-api.md) | Describes how to use the *dynamic dependency API* to dynamically take a dependency on different framework packages (other than the Windows App SDK framework package) in an unpackaged app at run time. |

## How packaged desktop apps run on Windows

For a deeper dive on what happens to files and registry entries when you create a Windows app package for your desktop application, see [Understanding how packaged desktop apps run on Windows](/windows/msix/desktop/desktop-to-uwp-behind-the-scenes).

## Related topics

- [Windows App SDK deployment guide for framework-dependent apps packaged with external location or unpackaged](../../../windows-app-sdk/deploy-unpackaged-apps.md)
- [Runtime architecture for the Windows App SDK](../../../windows-app-sdk/deployment-architecture.md)
- [MSIX documentation](/windows/msix)
