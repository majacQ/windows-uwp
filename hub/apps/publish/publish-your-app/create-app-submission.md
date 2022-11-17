---
title: Create an app submission for your app
description: Create an app submission to tell the Microsoft Store about your app
ms.topic: article
ms.date: 08/16/2022
zone_pivot_groups: store-installer-packaging
---

# Create an app submission for your app

> [!NOTE]
> This section of the documentation describes how to create an app submission in Partner Center. Alternatively, you can use the [Microsoft Store submission API](/windows/uwp/monetize/create-and-manage-submissions-using-windows-store-services) to automate app submissions.

Once you've [created your app by reserving a name](reserve-your-apps-name.md), you can start working on getting it published. The first step is to create a submission.

You can start your submission when your app is complete and ready to publish, or you can start entering info before you have written a single line of code. Updates you make to your submission are saved, so you can come back and work on it whenever you're ready.

After your app is published, you can publish an updated version by creating another submission in Partner Center. Creating a new submission lets you make and publish whatever changes are needed, whether you're uploading new packages or just changing details such as price or category. To create a new submission for a published app, click **Update** next to the most recent submission shown on its **Overview** page.

:::zone pivot="store-installer-msix,store-installer-pwa,store-installer-msi-exe"

## App submission checklist

Here are the details that you can provide when creating your app submission, with links to more info.

Items that you are required to provide or specify are noted below. Some areas are optional, or have default values provided that you can change as desired. You don't have to work on these sections in the order listed here.
:::zone-end

:::zone pivot="store-installer-add-on"

## What are add-ons?

Add-ons (also sometimes referred to as in-app products) are supplementary items for your app that can be purchased by customers. An add-on can be a fun new feature, a new game level, or anything else you think will keep users engaged. Not only are add-ons a great way to make money, but they help to drive customer interaction and engagement.

Add-ons are published through Partner Center, and require you to have an active developer account. You'll also need to enable the add-ons in your app's code.

An add-on must be associated with an app that you've created in [Partner Center](https://partner.microsoft.com/dashboard) (even if you haven't submitted it yet). You can find the button to **Create a new add-on** on your app's **Overview** page or on its **add-ons** page.

After you select **Create a new add-on**, you'll be prompted to specify a product type and assign a product ID for your add-on.

:::zone-end

:::zone pivot="store-installer-msix,store-installer-pwa"
[!INCLUDE [name](../../../includes/store/msix/create-app-submission.md)]
:::zone-end

:::zone pivot="store-installer-msi-exe"
[!INCLUDE [name](../../../includes/store/msi/create-app-submission.md)]
:::zone-end

:::zone pivot="store-installer-add-on"
[!INCLUDE [name](../../../includes/store/add-on/create-app-submission.md)]
:::zone-end

> [!IMPORTANT]
> You can no longer upload new XAP packages built using the Windows Phone 8.x SDK(s). Apps that are already in Store with XAP packages will continue to work on Windows 10 Mobile devices. For more info, see this [blog post](https://blogs.windows.com/windowsdeveloper/2018/08/20/important-dates-regarding-apps-with-windows-phone-8-x-and-earlier-and-windows-8-8-1-packages-submitted-to-microsoft-store).

> [!NOTE]
> You must have an active [developer account](https://developer.microsoft.com/store/register) in [Partner Center](https://partner.microsoft.com/dashboard) in order to submit apps to the Microsoft Store. All the users added to your developer account in Partner Center can submit EXE or MSI apps to the Microsoft Store. They can also modify all the existing EXE or MSI apps in Partner Center. The roles and permissions set for account users do not currently apply to EXE or MSI apps.

> [!NOTE]
> After submiting an app, the [owner](/windows/uwp/publish/set-custom-permissions-for-account-users) of your developer account is notified of publishing status and required actions through email and the Action Center in Partner Center. For more information about Action Center, see [Action Center Overview](/windows/uwp/publish/set-custom-permissions-for-account-users).
