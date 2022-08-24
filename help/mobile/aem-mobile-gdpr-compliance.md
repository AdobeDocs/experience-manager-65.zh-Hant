---
title: AEM Mobile- GDPR就緒性
seo-title: AEM Mobile - GDPR Readiness
description: 「AEM Mobile- GDPR就緒」
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

# AEM Mobile- GDPR就緒性 {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR在以下各節中用作示例，但所涵蓋的詳細資訊適用於所有資料保護和隱私法規；如GDPR、CCPA等。

## AEM MobileGDPR支援 {#aem-mobile-gdpr-support}

AEM Mobile已準備好協助客戶履行其GDPR合規義務。 沒有個人資料儲存在AEM Mobile。 如果已設定，則可以使用您的Adobe ID登錄Adobe Experience Mobile。

[https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html)

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

Adobe的數字出版產品(先於AEM Mobile)支援Adobe的GDPR就緒計畫。 請參閱 [https://www.adobe.com/privacy/general-data-protection-regulation.html](https://www.adobe.com/privacy/general-data-protection-regulation.html)。 下面將詳細介紹如何支援數字發佈套件產品中的GDPR相關功能，包括如何與Adobe協作啟動GDPR請求。

為確保您不會將AEM Mobile與舊版數字發佈套件產品混淆，您可以登錄到以下位置的數字發佈套件產品：

[https://digitalpublishing.acrobat.com/welcome.html](https://digitalpublishing.acrobat.com/welcome.html)

### 啟動GDPR請求 {#initiating-a-gdpr-request}

請聯繫Adobe客戶服務部門以啟動數字發佈套件的GDPR請求。

查找客戶資料需要以下ID。 接收的任何子集都意味著其他ID不適用於此用戶。

必要:

* 客戶合同ID: *dpsc-contractId*

至少提供以下1項：

* 最終用戶的客戶提供了OAuth ID（在客戶的直接權利系統中使用的ID）: *dpsc-directEntitlementId*
* 對於Windows應用用戶，最終用戶的App StoreID: *dpsc-windowsAppStoreId*
* 最終用戶用於與DPS應用交互的電子郵件地址： *電子郵件*

### 常見問題(FAQ) {#frequently-asked-questions-faq}

**Adobe是否會在啟動DELETE請求時刪除我的App Store採購？**

Adobe將刪除其擁有的App應用商店購買資訊（訂閱等） 但App商店的購物仍將記錄在案。 如果應用（最終用戶）登錄到應用商店，這些回執將再次被提取併發送到Adobe，隨後，這些回執將被視為新購買，並將由應用還原以重新訪問。

**Adobe是否會在啟動DELETE請求時刪除客戶提供的權利？**

Adobe將刪除其擁有的客戶額外直接權利津貼的資訊。 如果應用程式（最終用戶）登錄到客戶使用的OAuth機制，它將向Adobe發送資訊，服務將再次獲取額外的權利。

**最終用戶期望得到什麼？**

由於將權利分配給應用程式的密鑰作為查看器軟體的一部分駐留在設備上，因此最終用戶應卸載應用程式。 最終用戶應意識到，如果他們重新安裝應用，則現有購買（與應用商店用戶關聯）和直接權利津貼（與客戶的OAuth用戶關聯）仍將恢復。

**當應用在設備上的人之間共用時，會發生什麼情況？**

Adobe幾乎沒有直接與特定用戶關聯的資訊。 它使用隨機建立的UUID關聯資料，該UUID保存在應用程式的資料中，並在應用程式啟動的每個請求中傳遞。 這意味著在同一設備上共用App的最終用戶將使用相同的UUID，並且所有資料都將被視為由發出GDPR請求的人擁有。 對於訪問和刪除請求，DPSC將將共用應用的人員視為一人。

**使用分析跟蹤哪些個人資料？**

無. 正在跟蹤資料，但資料位於應用級別（不是個人級別）。 這包括啟動、崩潰、關閉、活動、購買或對開疊蓋等事件。 不跟蹤地理位置、名稱、設備ID或IP地址。

**最終用戶提供了他們的資訊，但未找到任何資訊。 為什麼不呢？**

隨著數字發佈套件產品的發展，服務實現也發生了變化，更多資料被模糊化。 如果沒有使用用戶提供的資料找到資料，則表示無法將用戶的資料跟蹤回該人。

### 範例 {#example}

請與Adobe客戶服務部門聯繫以啟動GDPR請求。

以下是數字發佈套件GDPR請求的輸入和結果的示例：

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
