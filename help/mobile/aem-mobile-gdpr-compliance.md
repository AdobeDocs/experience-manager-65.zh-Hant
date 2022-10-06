---
title: AEM Mobile - GDPR整備
seo-title: AEM Mobile - GDPR Readiness
description: 「AEM Mobile - GDPR整備」
seo-description: null
uuid: 817c434f-4b78-40f7-99d6-6efafdedb77e
contentOwner: trushton
discoiquuid: 9399dd3d-a485-4f53-a6f2-7b190da4235b
exl-id: d06e675f-fb61-47da-85de-e0b50dd44153
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# AEM Mobile - GDPR整備 {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR是以下各節中的範例，但涵蓋的詳細資訊適用於所有資料保護和隱私權法規；例如GDPR、CCPA等

## AEM Mobile GDPR支援 {#aem-mobile-gdpr-support}

AEM Mobile已準備好協助客戶履行其GDPR法規遵循義務。 不會將個人資料儲存在AEM Mobile中。 如果您已布建，則可使用Adobe ID登入Adobe Experience Mobile。

[https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html)

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

Adobe的數位發佈產品(在AEM Mobile之前)支援Adobe的GDPR整備計畫。 請參閱 [https://www.adobe.com/privacy/general-data-protection-regulation.html](https://www.adobe.com/privacy/general-data-protection-regulation.html). 以下將詳細說明Digital Publishing Suite產品中GDPR相關功能的支援，包括如何與Adobe合作以起始GDPR請求。

若要確保不會將AEM Mobile與舊版Digital Publishing Suite產品混淆，您可以在此處登入Digital Publishing Suite產品：

[https://digitalpublishing.acrobat.com/welcome.html](https://digitalpublishing.acrobat.com/welcome.html)

### 起始GDPR請求 {#initiating-a-gdpr-request}

請連絡Adobe客戶服務，以起始Digital Publishing Suite的GDPR請求。

找到客戶資料需要下列ID。 收到的任何子集都表示其他ID不適用於此使用者。

必要:

* 客戶合約ID: *dpsc-contractId*

至少提供下列1項：

* 一般使用者的客戶提供的OAuth ID（用於客戶直接權限系統的ID）: *dpsc-directEntitlementId*
* 若為Windows應用程式使用者，一般使用者的App Store ID: *dpsc-windowsAppStoreId*
* 一般使用者用來與DPS應用程式互動的電子郵件地址： *電子郵件*

### 常見問題集(FAQ) {#frequently-asked-questions-faq}

**起始Adobe請求時，DELETE是否會刪除我的App Store購買？**

Adobe會刪除其擁有的應用程式商店購買項目（訂閱等）的資訊 但App商店的購買量仍會記錄在案。 如果應用程式（一般使用者）登入App Store，系統會再次擷取這些收據並傳送至Adobe，之後再將這些收據視為新購買，並由應用程式還原以重新存取。

**Adobe在起始DELETE請求時是否會刪除客戶提供的權益？**

Adobe將刪除其擁有的客戶額外直接權利津貼資訊。 如果應用程式（一般使用者）登入客戶使用的OAuth機制，會將資訊傳送至Adobe，而服務會再次取用額外的權益。

**最終用戶期望什麼？**

由於將權限指派給應用程式的關鍵，是檢視器軟體的一部分，位於裝置上，因此使用者應解除安裝應用程式。 使用者應了解，如果他們重新安裝應用程式，則現有購買（與應用程式商店使用者相關聯）和直接權限配額（與客戶的OAuth使用者相關聯）仍會還原。

**當裝置上的使用者共用應用程式時會發生什麼事？**

Adobe幾乎沒有直接與特定使用者建立關聯的資訊。 它會使用隨機建立的UUID來建立資料關聯，此UUID會保留在應用程式的資料中，並會在應用程式起始的每個請求中傳遞。 這表示在相同裝置上共用應用程式的一般使用者將使用相同的UUID，而所有資料將視為由提出GDPR請求的人擁有。 對於存取和刪除請求，DPSC會將共用應用程式的使用者視為同一人。

**Analytics會追蹤哪些個人資料？**

無. 有資料會受到追蹤，但是在應用程式層級（非個人）。 這包括啟動、當機、關閉、活動、購買或對開本覆蓋等事件。 不會追蹤地理位置、名稱、裝置ID或IP位址。

**最終用戶提供了其資訊，但找不到任何內容。 為什麼不呢？**

隨著Digital Publishing Suite產品的演化，服務實作已變更，且更多資料已模糊化。 如果使用者提供的資料找不到任何資料，表示無法將使用者的資料追蹤回該人員。

### 範例 {#example}

請連絡Adobe客戶服務以起始GDPR請求。

以下是Digital Publishing Suite GDPR要求的輸入項目和產生的輸出範例：

#### 輸入： {#inputs}

```
dpsc-contractId = "12345-1234-12416234" 
directEntitlementId = "1234-1234-1234" 
windowsAppStoreId = "testWinAppStoreId" 
email = "test@what.com"
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
