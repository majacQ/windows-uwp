---
description: You can help customers discover your app by linking to your app's listing in the Microsoft Store.
title: Link to your app
ms.assetid: 5420B65C-7ECE-4364-8959-D1683684E146
ms.date: 10/31/2018
ms.topic: article
keywords: windows 10, uwp, link, windows store protocol, linking to an app, link to app
ms.localizationpriority: medium
---
# Link to your app

You can help customers discover your app by linking to your app's listing in the Microsoft Store on Windows.

## Getting the link to your app's Store listing

To get the URL for your app's Store listing, navigate to the app's [Product Identity identity](view-app-identity-details.md) page in the **Product management** section of [Partner Center](https://partner.microsoft.com/). The URL is in the format **`https://apps.microsoft.com/store/detail/<your app's Store ID>`**.

When a customer clicks this link, it opens the web-based listing page for your app. From there, customers on Windows devices can launch the Microsoft Store to download and install your app.

## Linking to your app's Store listing with the Microsoft Store badge

You can link directly to your app's listing with a custom badge to let customers know your app is in the Microsoft Store.

To create your badge, visit the [Microsoft Store badges](https://developer.microsoft.com/store/badges) page. You'll need to have your app's 12-character **Store ID** in order to generate the badge and link. You can find your app's **Store ID** in [Partner Center](https://partner.microsoft.com/) on the [Product identity](view-app-identity-details.md) page in the **Product management** section.

> [!NOTE]
> See [App marketing guidelines](app-marketing-guidelines.md) for info and requirements related to your use of the Microsoft Store badge.

## Linking directly to your app in the Microsoft Store

You can create a link that launches the Microsoft Store and goes directly to your app's listing page without opening a browser by using the **ms-windows-store:** URI scheme.

These links are useful if you know your users are on a Windows device and you want them to arrive directly at the listing page in the Store. For example, you might want to use this link after checking user agent strings in a browser to confirm that the user's operating system supports the Store, or when you are already communicating via a UWP app.

To use this URI scheme to link directly to your app's Store listing, append your app's Store ID to this link:

**`ms-windows-store://pdp/?ProductId=<your app's Store ID>`**

For more about launching the Microsoft Store app using a URI, see [Launch the Microsoft app](/windows/uwp/launch-resume/launch-store-app).
