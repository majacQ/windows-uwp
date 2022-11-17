---
description: Use this method in the Microsoft Store analytics API to get aggregate conversions by channel data for an add-on during a given date range and other optional filters.
title: Get add-on conversions by channel
ms.date: 08/04/2017
ms.topic: article
keywords: windows 10, uwp, Store services, Microsoft Store analytics API, add-on conversions, channel
ms.localizationpriority: medium
---
# Get add-on conversions by channel

Use this method in the Microsoft Store analytics API to get aggregate conversions by channel for an add-on during a given date range and other optional filters.

* A *conversion* means that a customer (signed in with a Microsoft account) has newly obtained a license to your add-on (whether you charged money or you've offered it for free).
* The *channel* is the method in which a customer arrived at your app's listing page (for example, via the Store or a [custom app promotion campaign](/windows/apps/publish/create-a-custom-app-promotion-campaign)).

This information is also available in the [Add-on acquisitions report](/windows/apps/publish/add-on-acquisitions-report.md#add-on-page-views-and-conversions-by-campaign-id) in Partner Center.

## Prerequisites

To use this method, you need to first do the following:

* If you have not done so already, complete all the [prerequisites](access-analytics-data-using-windows-store-services.md#prerequisites) for the Microsoft Store analytics API.
* [Obtain an Azure AD access token](access-analytics-data-using-windows-store-services.md#obtain-an-azure-ad-access-token) to use in the request header for this method. After you obtain an access token, you have 60 minutes to use it before it expires. After the token expires, you can obtain a new one.

## Request


### Request syntax

| Method | Request URI       |
|--------|----------------------|
| GET    | ```https://manage.devcenter.microsoft.com/v1.0/my/analytics/inappchannelconversions``` |


### Request header

| Header        | Type   | Description                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| Authorization | string | Required. The Azure AD access token in the form **Bearer** &lt;*token*&gt;. |


### Request parameters

| Parameter        | Type   |  Description      |  Required  
|---------------|--------|---------------|------|
| applicationId | string | The [Store ID](in-app-purchases-and-trials.md#store-ids) of the app for which you want to retrieve add-on conversion data. An example Store ID is 9WZDNCRFJ3Q8. |  Yes  |
| inAppProductId | string | The [Store ID](in-app-purchases-and-trials.md#store-ids) of the add-on for which you want to retrieve conversion data.  | Yes  |
| startDate | date | The start date in the date range of conversion data to retrieve. The default is 1/1/2016. |  No  |
| endDate | date | The end date in the date range of conversion data to retrieve. The default is the current date. |  No  |
| top | int | The number of rows of data to return in the request. The maximum value and the default value if not specified is 10000. If there are more rows in the query, the response body includes a next link that you can use to request the next page of data. |  No  |
| skip | int | The number of rows to skip in the query. Use this parameter to page through large data sets. For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on. |  No  |
| filter | string  | One or more statements that filter the response body. Each statement can use the **eq** or **ne** operators, and statements can be combined using **and** or **or**. You can specify the following strings in the filter statements.  For descriptions, see the [conversion values](#conversion-values) section in this article. <ul><li><strong>applicationName</strong></li><li><strong>appType</strong></li><li><strong>customCampaignId</strong></li><li><strong>referrerUriDomain</strong></li><li><strong>channelType</strong></li><li><strong>storeClient</strong></li><li><strong>deviceType</strong></li><li><strong>market</strong></li></ul><p>Here is an example *filter* parameter: <em>filter=deviceType eq 'PC'</em>.</p> | No   |
| aggregationLevel | string | Specifies the time range for which to retrieve aggregate data. Can be one of the following strings: <strong>day</strong>, <strong>week</strong>, or <strong>month</strong>. If unspecified, the default is <strong>day</strong>. | No |
| orderby | string | A statement that orders the result data values for each conversion. The syntax is <em>orderby=field [order],field [order],...</em>. The <em>field</em> parameter can be one of the following strings:<ul><li><strong>date</strong></li><li><strong>applicationName</strong></li><li><strong>inAppProductName</strong></li><li><strong>appType</strong></li><li><strong>customCampaignId</strong></li><li><strong>referrerUriDomain</strong></li><li><strong>channelType</strong></li><li><strong>storeClient</strong></li><li><strong>deviceType</strong></li><li><strong>market</strong></li></ul><p>The <em>order</em> parameter is optional, and can be <strong>asc</strong> or <strong>desc</strong> to specify ascending or descending order for each field. The default is <strong>asc</strong>.</p><p>Here is an example <em>orderby</em> string: <em>orderby=date,market</em></p> |  No  |
| groupby | string | A statement that applies data aggregation only to the specified fields. You can specify the following fields:<p/><ul><li><strong>date</strong></li><li><strong>applicationName</strong></li><li><strong>inAppProductName</strong></li><li><strong>appType</strong></li><li><strong>customCampaignId</strong></li><li><strong>referrerUriDomain</strong></li><li><strong>channelType</strong></li><li><strong>storeClient</strong></li><li><strong>deviceType</strong></li><li><strong>market</strong></li></ul><p>The returned data rows will contain the fields specified in the <em>groupby</em> parameter as well as the following:</p><ul><li><strong>date</strong></li><li><strong>applicationId</strong></li><li><strong>inAppProductId</strong></li><li><strong>inAppProductName</strong></li><li><strong>conversionCount</strong></li><li><strong>clickCount</strong></li></ul><p>The <em>groupby</em> parameter can be used with the <em>aggregationLevel</em> parameter. For example: <em>groupby=ageGroup,market&amp;aggregationLevel=week</em></p> |  No  |


### Request example

The following example demonstrates several requests for getting app conversion data. Replace the *applicationId* value with the Store ID for your app.

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/inappchannelconversions?applicationId=9NBLGGGZ5QDR&startDate=1/1/2017&endDate=2/1/2017&top=10&skip=0  HTTP/1.1
Authorization: Bearer <your access token>

GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/inappchannelconversions?applicationId=9NBLGGGZ5QDR&startDate=1/1/2017&endDate=4/31/2017&skip=0&filter=market eq 'US'  HTTP/1.1
Authorization: Bearer <your access token>
```

## Response


### Response body

| Value      | Type   | Description                  |
|------------|--------|-------------------------------------------------------|
| Value      | array  | An array of objects that contain aggregate conversion data for the add-on. For more information about the data in each object, see the [conversion values](#conversion-values) section below.                     |
| @nextLink  | string | If there are additional pages of data, this string contains a URI that you can use to request the next page of data. For example, this value is returned if the **top** parameter of the request is set to 10 but there are more than 10 rows of conversion data for the query. |
| TotalCount | int    | The total number of rows in the data result for the query.                                                                                                                                                                                                                             |

### Conversion values

Objects in the *Value* array contain the following values.

| Value               | Type   | Description                           |
|---------------------|--------|-------------------------------------------|
| date                | string | The first date in the date range for the conversion data. If the request specified a single day, this value is that date. If the request specified a week, month, or other date range, this value is the first date in that date range. |
| inAppProductId      | string  | The [Store ID](in-app-purchases-and-trials.md#store-ids) of the add-on for which you are retrieving conversion data.     |
| inAppProductName    | string  | The display name of the add-on for which you are retrieving conversion data.   |
| applicationId       | string | The  [Store ID](in-app-purchases-and-trials.md#store-ids) of the app for which you are retrieving conversion data.     |
| applicationName     | string | The display name of the app for which you are retrieving conversion data.        |
| appType          | string |  The type of the product for which you are retrieving conversion data. For this method, the only supported value is **Add-On**.            |
| customCampaignId           | string |  The ID string for a [custom app promotion campaign](/windows/apps/publish/create-a-custom-app-promotion-campaign) that is associated with the app.   |
| referrerUriDomain           | string |  Specifies the domain where the app listing with the custom app promotion campaign ID was activated.   |
| channelType           | string |  One of the following strings that specifies the channel for the conversion:<ul><li><strong>CustomCampaignId</strong></li><li><strong>Store Traffic</strong></li><li><strong>Other</strong></li></ul>    |
| storeClient         | string | The version of the Store where the conversion occurred. Currently, the only supported value is **SFC**.    |
| deviceType          | string | One of the following strings:<ul><li><strong>PC</strong></li><li><strong>Phone</strong></li><li><strong>Console-Xbox One</strong></li><li><strong>Console-Xbox Series X</strong></li><li><strong>IoT</strong></li><li><strong>Holographic</strong></li><li><strong>Unknown</strong></li></ul>            |
| market              | string | The ISO 3166 country code of the market where the conversion occurred.    |
| clickCount              | number  |     The number of customer clicks on your app listing link.      |           
| conversionCount            | number  |   The number of customer conversions.         |         


### Request and Response example

The following code snippets demonstrates some example request and JSON response body for those request.

#### Sample Request 

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/inappchannelconversions?applicationId=9NBLGGGZ5QDR&startDate=12/19/2019&endDate=12/20/2021&top=10&skip=0
HTTP/1.1
Authorization: Bearer <your access token>
```
#### Sample Response

```json
{
    "Value": [
        {
            "inAppProductId": "9NN2HW33ZB2G",
            "applicationId": "9NBLGGGZ5QDR",
            "clickCount": 220636,
            "conversionCount": 154
        },
        {
            "inAppProductId": "9PN07J0WC18B",
            "applicationId": "9NBLGGGZ5QDR",
            "clickCount": 277061,
            "conversionCount": 187
        }
    ],
    "@nextLink": "",
    "TotalCount": 2
}
```

#### Sample Request 

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/inappchannelconversions?applicationId=9NBLGGGZ5QDR&startDate=12/19/2021&endDate=12/20/2021&top=10&skip=0&groupby=date,applicationName,inAppProductName,appType,customCampaignId,referrerUriDomain,channelType,storeClient,deviceType,market
HTTP/1.1
Authorization: Bearer <your access token>
```
#### Sample Response

```json
{
    "Value": [
        {
            "inAppProductId": "9WZDNCRCWW61",
            "inAppProductName": "SeasonPass0",
            "appType": "Add-On",
            "date": "2022-06-21",
            "applicationId": "9NBLGGGZ5QDR",
            "applicationName": "Contoso Demo",
            "customCampaignId": "mcg_mahjong_othergames",
            "channelType": "CustomCampaignId",
            "storeClient": "SFW",
            "deviceType": "Unknown",
            "market": "BR",
            "clickCount": 1,
            "conversionCount": 1
        },
        {
            "inAppProductId": "9WZDNCRCWW5H",
            "inAppProductName": "OEMFreePurchase",
            "appType": "Add-On",
            "date": "2022-07-06",
            "applicationId": "9NBLGGGZ5QDR",
            "applicationName": "Contoso Demo",
            "customCampaignId": "mcg_solitaire_othergames",
            "channelType": "CustomCampaignId",
            "storeClient": "SFW",
            "deviceType": "Unknown",
            "market": "AT",
            "clickCount": 1,
            "conversionCount": 1
        },
        {
            "inAppProductId": "9WZDNCRCWW5Z",
            "inAppProductName": "Episode1Combo",
            "appType": "Add-On",
            "date": "2022-07-09",
            "applicationId": "9NBLGGGZ5QDR",
            "applicationName": "Contoso Demo",
            "customCampaignId": "vungle",
            "channelType": "CustomCampaignId",
            "storeClient": "SFW",
            "deviceType": "Unknown",
            "market": "CZ",
            "clickCount": 1,
            "conversionCount": 1
        },
        {
            "inAppProductId": "9WZDNCRCWW5H",
            "inAppProductName": "OEMFreePurchase",
            "appType": "Add-On",
            "date": "2022-07-09",
            "applicationId": "9NBLGGGZ5QDR",
            "applicationName": "Contoso Demo",
            "customCampaignId": "vungle",
            "channelType": "CustomCampaignId",
            "storeClient": "SFW",
            "deviceType": "Unknown",
            "market": "CZ",
            "clickCount": 1,
            "conversionCount": 1
        },
        {
            "inAppProductId": "9WZDNCRCWW4Z",
            "inAppProductName": "Episode1Grandfathered",
            "appType": "Add-On",
            "date": "2022-07-11",
            "applicationId": "9NBLGGGZ5QDR",
            "applicationName": "Contoso Demo",
            "customCampaignId": "|autosuggest",
            "channelType": "CustomCampaignId",
            "storeClient": "SFW",
            "deviceType": "Unknown",
            "market": "ES",
            "clickCount": 1,
            "conversionCount": 1
        },
        {
            "inAppProductId": "9WZDNCRCWW5W",
            "inAppProductName": "Episode2Combo",
            "appType": "Add-On",
            "date": "2022-07-11",
            "applicationId": "9NBLGGGZ5QDR",
            "applicationName": "Contoso Demo",
            "customCampaignId": "vungle",
            "channelType": "CustomCampaignId",
            "storeClient": "SFW",
            "deviceType": "Unknown",
            "market": "CZ",
            "clickCount": 1,
            "conversionCount": 1
        },
        {
            "inAppProductId": "9WZDNCRCWW4P",
            "inAppProductName": "SeasonPass24",
            "appType": "Add-On",
            "date": "2022-07-12",
            "applicationId": "9NBLGGGZ5QDR",
            "applicationName": "Contoso Demo",
            "customCampaignId": "vungle",
            "channelType": "CustomCampaignId",
            "storeClient": "SFW",
            "deviceType": "Unknown",
            "market": "CZ",
            "clickCount": 1,
            "conversionCount": 1
        },
        {
            "inAppProductId": "9WZDNCRCWW5H",
            "inAppProductName": "OEMFreePurchase",
            "appType": "Add-On",
            "date": "2022-07-13",
            "applicationId": "9NBLGGGZ5QDR",
            "applicationName": "Contoso Demo",
            "customCampaignId": "9wzdncrfjbd8",
            "channelType": "CustomCampaignId",
            "storeClient": "SFW",
            "deviceType": "Unknown",
            "market": "CA",
            "clickCount": 1,
            "conversionCount": 1
        },
        {
            "inAppProductId": "9WZDNCRCWW61",
            "inAppProductName": "SeasonPass0",
            "appType": "Add-On",
            "date": "2022-07-17",
            "applicationId": "9NBLGGGZ5QDR",
            "applicationName": "Contoso Demo",
            "customCampaignId": "scom-web-store",
            "channelType": "CustomCampaignId",
            "storeClient": "SFW",
            "deviceType": "Unknown",
            "market": "US",
            "clickCount": 1,
            "conversionCount": 1
        }
    ],
    "@nextLink": "",
    "TotalCount": 9
}
```
## Related topics

* [Add-on acquisitions report](/windows/apps/publish/add-on-acquisitions-report)
* [Access analytics data using Microsoft Store services](access-analytics-data-using-windows-store-services.md)
* [Get add-on acquisitions](get-in-app-acquisitions.md)
