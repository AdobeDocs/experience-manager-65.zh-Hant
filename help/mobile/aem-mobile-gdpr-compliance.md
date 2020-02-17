---
title: AEM Mobile - GDPR就緒性
seo-title: AEM Mobile - GDPR就緒性
description: 'null'
seo-description: 'null'
uuid: 817c434f-4b78-40f7-99d6-6efafdedb77e
contentOwner: trushton
discoiquuid: 9399dd3d-a485-4f53-a6f2-7b190da4235b
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# AEM Mobile - GDPR就緒性 {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR在以下幾節中是以範例形式使用，但涵蓋的詳細資訊適用於所有資料保護和隱私權法規；例如GDPR、CCPA等。

## AEM Mobile GDPR支援 {#aem-mobile-gdpr-support}

AEM mobile已準備好協助客戶履行其GDPR合規性義務。 AEM mobile中不會儲存任何個人資料。 如果您已布建，則可以使用您的Adobe ID登入Adobe Experience Mobile。

[https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html)

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

Adobe的數位出版產品（先於AEM Mobile）支援Adobe的GDPR整備計畫。 請參閱 [https://www.adobe.com/privacy/general-data-protection-regulation.html](https://www.adobe.com/privacy/general-data-protection-regulation.html)。 以下將詳細說明Digital Publishing suite產品中支援GDPR相關功能的細節，包括如何與Adobe合作以啟始GDPR要求。

為確保您不會將AEM mobile與舊版Digital Publishing suite產品混淆，您可以在這裡登入Digital Publishing Suite產品：

[https://digitalpublishing.acrobat.com/welcome.html](https://digitalpublishing.acrobat.com/welcome.html)

### 開始GDPR請求 {#initiating-a-gdpr-request}

請聯絡Adobe客戶服務，以提出Digital Publishing Suite的GDPR要求。

找到客戶資料時需要下列ID。 收到的任何子集都表示其他ID不適用於此使用者。

必要:

* 客戶的合約ID: *dpsc-contractId*

至少提供下列1項：

* 一般使用者的客戶提供OAuth ID（用於客戶直接權益系統的ID）: *dpsc-directEntitlementId*
* 對於Windows應用程式使用者，使用者的App Store ID: *dpsc-windowsAppStoreId*
* 一般使用者用來與DPS應用程式互動的電子郵件地址：電子 *郵件*

### 常見問答集(FAQ) {#frequently-asked-questions-faq}

**Adobe會在起始DELETE請求時刪除我的App Store購買項目嗎？**

Adobe將刪除其擁有的App Store購買項目（訂閱等）的資訊不過，在App商店中，購買仍會記錄在案。 如果應用程式（使用者）登入App Store，這些回執會再次被取出並傳送至Adobe，然後會視為新購買項目，而且應用程式會還原這些回執，以再次存取。

**Adobe會在啟動DELETE請求時刪除客戶提供的權益嗎？**

Adobe將刪除其擁有的客戶額外直接權益津貼資訊。 如果應用程式（一般使用者）登入客戶使用的OAuth機制，它會傳送資訊給Adobe，而服務會再次取得額外權益。

**一般使用者預期會如何？**

由於指派應用程式權益的金鑰是位於檢視器軟體的裝置上，因此使用者應解除安裝應用程式。 使用者應意識到，如果他們重新安裝應用程式，現有的購買項目（與App Store使用者相關）和直接權益配額（與客戶的OAuth使用者相關）仍會復原。

**當應用程式在裝置上與人共用時，會發生什麼情況？**

Adobe幾乎沒有直接與特定使用者建立關聯的資訊。 它會使用隨機建立的UUID來關聯資料，此UUID會保留在應用程式的資料中，並會傳遞至應用程式啟動的每個請求。 這表示在相同裝置上共用應用程式的使用者將使用相同的UUID，而且所有資料都會被提出GDPR要求的使用者視為擁有。 對於存取和刪除請求，DPSC會將共用應用程式的人員視為一人。

**Analytics會追蹤哪些個人資料？**

無. 有資料在追蹤中，但是在應用程式層級（非個人）。 這包括啟動、當機、關閉、活動、購買或對開本覆蓋等事件。 不會追蹤地理位置、名稱、裝置ID或IP位址。

**最終用戶提供了他們的資訊，但沒有找到任何資訊。 為什麼不呢？**

隨著Digital Publishing suite產品的發展，服務實作已變更，而且有更多資料被模糊化。 如果使用者提供的資料找不到任何資料，表示無法將使用者的資料追蹤回該人。

### 例如 {#example}

請聯絡Adobe客戶服務以提出GDPR要求。

以下是Digital Publishing Suite GDPR要求的輸入和產生輸出範例：

#### 輸入： {#inputs}

```
dpsc-contractId = “12345-1234-12416234” 
directEntitlementId = “1234-1234-1234” 
windowsAppStoreId = “testWinAppStoreId” 
email = “test@what.com”
```

#### 輸出 {#outputs}

```
{

    "jobId": "test-1524750204384",

    "product": "DPSC",

    "action": "access",

    "userIDS": [

        {

        "namespace": "email",

        "value": "test@what.com"

        },

        {

        "namespace": "windowsAppStoreId",

        "value": "testWinAppStoreId"

        },

        {

        "namespace": "directEntitlementId",

        "value": "1234-1234-1234"

        }

    ],

    "receiptData": {

    "recordsFound": 6,

    "recordsAffected": 0,

    "tablesModified": 0,

    "subscriptionsFound": 24,

    "entitlementsFound": 24

    },

    "records": {

        "DPS_Stage_EntitlementUserDevices": [

        {

            "user_id": "testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "device_id": "appleStore:test1b16-f032-4d9c-9200-0d19999405c4",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test967d-5179-4dc6-958c-facd9d94da38",

            "device_id": "appleStore:test3f07-d5aa-4b32-8fac-b2b690b7ccd7",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test1838-6494-4e74-912c-1edf61581d0e",

            "device_id": "appleStore:test3813-f8cc-49ce-b021-50eb0814a3bb",

            "account_id": "1234-1234-1234"

        },

        {

            "user_id": "test5468-1a11-4e4c-be43-274181a9ef81",

            "device_id": "appleStore:testf082-2783-498d-ab62-b1b2e3eb67ae",

            "account_id": "1234-1234-1234"

        }

        ],

            "DPS_Stage_EntitlementUsers": [

        {

            "id": "store:test04a7-33a3-4b90-863d-79981ead0f19:appleStore",

            "part_id": "0",

            "alias_user_id": "testWinAppStoreId"

        },

        {

            "id": "internal:testd2da-0606-4444-87ef-0d5a1d4a121d:adobe",

            "part_id": "0",

            "user_id": "test@what.com"

        }

        ],

            "DPS_Stage_Subscriptions": [

        {

            "id": "appleStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test3531-a209-4391-beb9-951c7822244e",

            "overflow": "test4e59-86a8-4b75-b699-77e980c287ab",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "test491b-379e-4d24-96ef-e481bf8d3062",

            "overflow": "test931b-7422-485d-85a5-134828187b6c",

            "entitlement_count": "12"

        }

        ],

            "DPS_Stage_Entitlements": [

        {

            "id": "samsungStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test7332-60a0-42b8-a508-474668d83d2e",

            "overflow": "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "testf766-102a-460d-8f5a-42f7bb9d68b7",

            "overflow": "test4d96-2197-45a8-9caf-2aa2846b770c",

            "entitlement_count": "12"

        }

        ],

            "s3Buckets": {

            "name": "DPS-Entitlements-Overflow",

            "folder": "stage/",

            "overflows": {

            "subscriptions": [

            "test4e59-86a8-4b75-b699-77e980c287ab",

            "test931b-7422-485d-85a5-134828187b6c"

        ],

            "entitlements": [

            "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "test4d96-2197-45a8-9caf-2aa2846b770c"

                ]

            }

        }

    }

}
```

