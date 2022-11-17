---
title: Enhance UI with the Visual layer (Windows App SDK)
description: The Windows App SDK implementation of the UWP Visual layer.
ms.topic: article
ms.date: 11/16/2021
keywords: 
ms.author: jimwalk
author: jwmsft
ms.localizationpriority: medium
---

# Enhance UI with the Visual layer

The Visual layer provides a high performance, retained-mode API for graphics, effects, animations, and input, and is the foundation for all UI across Windows devices. [Microsoft.UI.Composition](/windows/windows-app-sdk/api/winrt/microsoft.ui.composition) is the [Windows App SDK/WinUI 3](index.md) implementation of the [UWP Visual layer](/windows/uwp/composition/visual-layer).

Microsoft.UI.Composition provides access to nearly identical functionality as the UWP Visual layer, with some exceptions. The primary difference is the namespace.

- In WinUI 3, [SwapChainPanel](/windows/windows-app-sdk/api/winrt/microsoft.ui.xaml.controls.swapchainpanel) does not support transparency, nor does it support applying [AcrylicBrush](/windows/windows-app-sdk/api/winrt/microsoft.ui.xaml.media.acrylicbrush) and other effects that use a [CompositionBackdropBrush](/windows/windows-app-sdk/api/winrt/microsoft.ui.composition.compositionbackdropbrush) over it. `AcrylicBrush` and these other `CompositionBackdropBrush`-based effects are not able to sample from a `SwapChainPanel`.
- In a desktop app, `Window.Current` is `null`, so you can't get an instance of the [Compositor](/windows/windows-app-sdk/api/winrt/microsoft.ui.composition.compositor) from `Window.Current.Compositor`. In XAML apps (both UWP and desktop), we recommend that you call [ElementCompositionPreview.GetElementVisual(UIElement)](/windows/windows-app-sdk/api/winrt/microsoft.ui.xaml.hosting.elementcompositionpreview.getelementvisual) to get a Composition [Visual](/windows/windows-app-sdk/api/winrt/microsoft.ui.composition.visual), and get the `Compositor` from the visual's [Compositor](/windows/windows-app-sdk/api/winrt/microsoft.ui.composition.compositionobject.compositor) property. In cases where you don't have access to a `UIElement` (for example, if you create a [CompositionBrush](/windows/windows-app-sdk/api/winrt/microsoft.ui.composition.compositionbrush) in a class library), you can call [CompositionTarget.GetCompositorForCurrentThread](/windows/windows-app-sdk/api/winrt/microsoft.ui.xaml.media.compositiontarget.getcompositorforcurrentthread).

For more details about the Visual layer see the [Visual layer overview](/windows/uwp/composition/visual-layer) in the UWP documentation. The documentation and samples are applicable to Microsoft.UI.Composition in most cases.

## Prerequisites to using Microsoft.UI.Composition

To use Microsoft.UI.Composition APIs in the Windows App SDK:

1. Download and install the latest release of the Windows App SDK. For more information, see [Install tools for the Windows App SDK](set-up-your-development-environment.md).
2. Follow the instructions to [Create your first WinUI 3 project](../winui/winui3/create-your-first-winui3-app.md) or to [use the Windows App SDK in an existing project](use-windows-app-sdk-in-existing-project.md).

To learn more about the availability of Microsoft.UI.Composition in the Windows App SDK, see [release channels](release-channels.md).

## Sample Gallery

We've updated the Windows Composition Samples Gallery to now take a dependency on the Windows App SDK Composition APIs. Please visit [WindowsCompositionSamples](https://github.com/microsoft/WindowsCompositionSamples) to see the Microsoft.UI.Composition APIs in action!

![app gif](https://media.giphy.com/media/Hx2beMDfEA7QqWPvD4/giphy.gif)

## Related topics

- [UWP Visual layer overview](/windows/uwp/composition/visual-layer)
- [Using the Visual layer in desktop apps](../desktop/modernize/visual-layer-in-desktop-apps.md)
