﻿---
author: jnHs
Description: If your app displays ads using the Microsoft Advertising SDK, use the In-app ads page of the Dev Center dashboard to manage your use of ads.
title: In-app ads
ms.assetid: 09970DE3-461A-4E2A-88E3-68F2399BBCC8
ms.author: wdg-dev-content
ms.date: 2/24/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, uwp
ms.localizationpriority: high
---

# In-app ads

Use the **Monetize** &gt; **In-app ads** page in the Dev Center dashboard to create and manage ad units for:

* Universal Windows Platform (UWP) apps that use the [Microsoft Advertising SDK](http://aka.ms/ads-sdk-uwp).
* Windows 8.x and Windows Phone 8.x apps that use the [Microsoft Advertising SDK for Windows and Windows Phone 8.x](http://aka.ms/store-8-sdk).

For more information about how to integrate these SDKs with your apps to display ads, see [Display ads in your app with the Microsoft Advertising SDK](../monetize/display-ads-in-your-app.md).

<span id="create-ad-unit" />
## Create ad units

To create an ad unit for a [banner ad](../monetize/banner-ads.md), [interstitial ad](../monetize/interstitial-ads.md), or [native ad](../monetize/native-ads.md) in your app:

1.  Go to the **Monetize** &gt; **In-app ads** page in the dashboard and click **Create ad unit**.

2.  In the **App name** drop-down, select the app in which your ad unit will be used.

3.  In the **Ad unit name** field, enter a name for the ad unit. This can be any descriptive string that you want to use to identify the ad unit for reporting purposes.

4.  In the **Ad unit type** drop-down, select the ad type.

    * If you are using an [AdControl](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.adcontrol.aspx) in your app to show banner ads, select **Banner**.

    * If you are using an [InterstitialAd](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.interstitialad.aspx) in your app to show interstitial video ads or interstitial banner ads, select **Video interstitial** or **Banner interstitial** (be sure to select the appropriate option for the type of interstitial ad you want to show).

    * If you are using a [NativeAd](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.nativead.aspx) in your app to show native ads, select **Native**.
      > [!NOTE]
      > The ability to create **Native** ad units is currently available only to select developers who are participating in a pilot program, but we intend to make this feature available to all developers soon. If you are interested in joining our pilot program, reach out to us at aiacare@microsoft.com.

5. In the **Device family** drop-down, select the device family targeted by the app in which your ad unit will be used. The available options are: **UWP (Windows 10)**, **PC/Tablet (Windows 8.1)**, or **Mobile (Windows Phone 8.x)**.

6. Configure the following additional settings as desired:

    * If you select the **UWP (Windows 10)** device family for the ad unit, you can optionally configure [mediation settings](#mediation) for the ad unit.

    * If you select the **PC/Tablet (Windows 8.1)** or **Mobile (Windows Phone 8.x)** device family for a banner ad unit, you can optionally select **Show community ads in your app** to opt in to [community ads](about-community-ads.md).

7.  If you haven't yet set the COPPA compliance for the selected app, choose an option in the [COPPA compliance](#coppa) section.

8.  Click **Create ad unit**.

After you create the new ad unit, it appears in the table of available ad units in the **Monetize** &gt; **In-app ads** page.

<span id="available-ad-units" />
## Review and edit ad units

After you create ad units for one or more apps in your account, these ad units appear in a table at the bottom of the **Monetize** &gt; **In-app ads** page. This table displays the **Application ID** and **Ad unit ID** for each ad unit, along with other information. To show ads in your app, you'll need to use these values in your code. For more information, see [Set up ad units in your app](../monetize/set-up-ad-units-in-your-app.md).

* If your app shows [banner ads](../monetize/banner-ads.md), assign these values to the [ApplicationId](https://msdn.microsoft.com/library/mt313174.aspx) and [AdUnitId](https://msdn.microsoft.com/library/mt313171.aspx) properties of your [AdControl](https://msdn.microsoft.com/library/mt313154.aspx) object.

* If your app shows [interstitial ads](../monetize/interstitial-ads.md), pass these values to the [RequestAd](https://msdn.microsoft.com/library/mt313192.aspx) method of your [InterstitialAd](https://msdn.microsoft.com/library/mt313189.aspx) object.

* If your app shows [native ads](../monetize/native-ads.md), pass these values to the *applicationId* and *adUnitId* parameters of the [NativeAdsManager](https://msdn.microsoft.com/library/windows/apps/microsoft.advertising.winrt.ui.nativeadsmanager.nativeadsmanager.aspx) constructor.
  > [!IMPORTANT]
  > You can use each ad unit in only one app. If you use an ad unit in more than one app, ads will not be served for that ad unit.

  > [!NOTE]
  > You can use multiple banner, interstitial, and native ad controls in a single app. In this scenario, we recommend that you assign a different ad unit to each control. Using different ad units for each control enables you to separately [configure the mediation settings](../publish/in-app-ads.md#mediation) and get discrete [reporting data](../publish/advertising-performance-report.md) for each control. This also enables our services to better optimize the ads we serve to your app.

To edit the [mediation settings](#mediation) for a UWP ad unit or the [COPPA compliance](#coppa) for the app in which the ad unit is used, click the ad unit name.

Note that if an ad unit has no activity for the past six months, we will label it as **Inactive**, and eventually remove it from your dashboard. You can use filters to show only **Active** or **Inactive** ad units. If you see any ad units that you believe are inaccurately marked as **Inactive**, [contact support](http://aka.ms/storesupport).

<span id="mediation" />
## Mediation settings

When you [create a new UWP ad unit](#create-ad-unit) or [edit an existing UWP ad unit](#available-ad-units), use the options in this section to configure ad mediation for the ad unit. Ad mediation enables you to maximize your ad revenue and app promotion capabilities by displaying ads from multiple ad networks, including ads from other paid ad networks and non-revenue generating ads for Microsoft app promotion campaigns. We take care of mediating banner ad requests from the ad networks you choose. If you have a UWP ad unit that is already associated with a banner, interstitial, or native ad in your app, enabling ad mediation requires no code changes in your app.

> [!NOTE]
> When you enable ad mediation for a UWP ad unit, you do not need to obtain an ad unit from third-party ad networks. Our ad mediation service automatically creates any necessary third-party ad units.

To configure ad mediation settings for a UWP ad unit in your app:

1. [Create an ad unit](#create-ad-unit) or [select an existing ad unit](#available-ad-units).

2. On the **In-app ads** page, go to the **Mediation settings** section.

3. By default, the **Let Microsoft choose the best mediation settings for your app** check box is selected. This option uses machine-learning algorithms to automatically choose the ad mediation settings for your app to help you maximize your ad revenue across the markets your app supports. We recommend that you use this option. Otherwise, if you want to choose your own ad mediation settings, clear this check box.
    > [!NOTE]
    > The remaining steps in this section are only applicable if you clear this check box and choose your own ad mediation settings.

4. In the **Target** drop-down, choose **Baseline** to configure the default configuration for your ad mediation settings. This default configuration will be applied to all markets, except for markets where you define market-specific configurations.

6. Next, specify the ratio of ads you want to show in your control from paid networks (which pay you revenue for impressions) and other ad networks (which do not pay you revenue for impressions). To do this, enter a value between 0 and 100 in the **Weight** fields for **Paid ad networks** and **Other ad networks**.  

7. In the **Paid ad networks** section, select the check box in the **Active** column for each [paid network](#paid-networks) you want to use, and then use the arrows in the **Rank** column to order the networks by rank (this specifies how often each network should be used by your control).

8. If you have selected a **Banner** or **Banner interstitial** ad unit, you will also see a section named **Other ad networks**. The networks in this section do not earn you revenue for ad impressions. Instead, these networks show ads from sources such as app promotion campaigns.

    In the **Other ad networks** section, select the check box in the **Active** column for each [other network](#other-networks) you want to use, and then use the arrows in the **Rank** column to order the networks by rank (this specifies how often each network should be used by your control). The following other networks are currently supported:

9. For each market where you want to override the default mediation configuration, select the market in the **Target** drop-down, and update the ad network selections and ranking.

10. Click **Create ad unit** (if you are creating a new ad unit) or **Save** (if you are editing an existing ad unit).

<span id="paid-networks" />
### Supported paid ad networks

The following table lists the paid networks we currently support for each ad type. Note that some of these networks are [not available in all markets](#network-markets).

|  Ad network  |  Description  |  Supported ad types  |
|--------------|---------------|---------------------|
| AOL and AppNexus |  This is a Microsoft-managed ad network that serves ads through our partner networks, AOL and AppNexus.<p/>**Note**: AOL and AppNexus is always ranked first in the **Paid ad networks** list for Banner ad units, and it cannot be changed to a lower ranking for these types of ads. | Banner, Video interstitial |
| AppNexus (direct) | Select this option to serve video interstitial ads from [AppNexus](https://www.appnexus.com). | Video interstitial, Native  |
| Microsoft App install ads | Select this option to serve app install ads or app re-engagement ads created by other developers in the Windows ecosystem who [create promotional ad campaigns for their apps](create-an-ad-campaign-for-your-app.md).  |  Banner, Banner interstitial, Native  |
| Outbrain |  Select this option to serve ads from [Outbrain](https://www.outbrain.com/). |  Banner  |
| Revcontent |  Select this option to serve ads from [Revcontent](http://www.revcontent.com/). |  Banner  |
| Smaato |  Select this option to serve ads from [Smaato](https://www.smaato.com/). |  Banner  |
| smartclip |  Select this option to serve ads from [smartclip](http://www.smartclip.com/). |  Video interstitial  |
| SpotX |  Select this option to serve ads from [SpotX](https://www.spotx.tv/). |  Video interstitial  |
| Taboola |  Select this option to serve ads from [Taboola](https://www.taboola.com/). |  Banner  |


<span id="other-networks" />
### Other ad networks

The following table lists the other networks we currently support for each ad type.

|  Ad network  |  Description  |  Supported ad types  |
|--------------|---------------|---------------------|
| Microsoft Community ads |  If you [create a promotional ad campaign for one of your apps](create-an-ad-campaign-for-your-app.md) and configure this campaign as a [community ad campaign](about-community-ads.md), select this options to show ads from this campaign. | Banner, Banner interstitial |
| Microsoft House ads | If you [create a promotional ad campaign for one of your apps](create-an-ad-campaign-for-your-app.md) and configure this campaign as a [house ad campaign](about-house-ads.md), select this options to show ads from this campaign. | Banner, Banner interstitial  |


<span id="network-markets" />
### Supported markets for ad networks

The available ad networks serve ads in all [supported markets](define-pricing-and-market-selection.md#microsoft-store-consumer-markets), with the following exceptions.

|  Ad network  |  Supported markets  |
|--------------|---------------------|
| Revcontent | Brazil, Canada, France, Germany, Italy, Japan, Spain, United Kingdom, United States  |
| Smaato | Brazil, Canada, France, Germany, Italy, Japan, Spain, United Kingdom, United States |
| smartclip | Austria, Belgium, Denmark, Finland, Germany, Italy, Netherlands, Norway, Sweden, Switzerland  |

<span id="coppa" />
## COPPA compliance

When you [create an ad unit](#create-ad-unit) or [select an existing ad unit](#available-ad-units), the **COPPA compliance** section appears at the bottom of the dashboard page if the selected app for the ad unit has at least one submission that has reached the [in the Store](../publish/the-app-certification-process.md#in-the-store) step in the app certification process.

For purposes of the Children's Online Privacy Protection Act (“COPPA”), you must select **This application is directed at children under the age of 13** in this section if your app is directed at children under the age of 13. If you select this option, Microsoft will take steps to disable its behavioral advertising services when delivering advertising into your app.

The **COPPA compliance** setting you choose is automatically applied to all ad units for the selected app.

> [!IMPORTANT]
> If your app is directed at children under the age of 13, you have certain obligations under COPPA. For more information on your obligations, please see [this page](http://go.microsoft.com/fwlink/p/?linkid=536558).
