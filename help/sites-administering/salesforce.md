---
title: 與Salesforce整合
seo-title: Integrating with Salesforce
description: 瞭解與SalesforceAEM的整合。
seo-description: Learn about integrating AEM with Salesforce.
uuid: 3d6a249d-082f-4a10-b255-96482ccd2c65
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bee7144e-4276-4e81-a3a0-5b7273af34fe
docset: aem65
exl-id: 0f3aaa0a-ccfb-4162-97a6-ee5485595d28
source-git-commit: c7958efbc4557ab3e50732da59faabf4e36c3844
workflow-type: tm+mt
source-wordcount: '1564'
ht-degree: 1%

---


# 與Salesforce整合 {#integrating-with-salesforce}

將Salesforce與集AEM成可提供銷售線索管理功能，並利用Salesforce現成提供的現有功能。 您可以配置AEM將銷售線索過帳到Salesforce，並建立直接從Salesforce訪問資料的元件。

Salesforce和Salesforce之間的雙向和可擴展AEM的整合可實現：

* 組織要充分利用和更新資料以增強客戶體驗。
* 從市場營銷到銷售活動的參與。
* 組織自動從Salesforce資料儲存中傳輸和接收資料。

本文檔介紹以下內容：

* 如何配置SalesforceCloud Services(AEM配置為與Salesforce整合)。
* 如何在客戶端上下文和個性化中使用Salesforce Lead/Contact資訊。
* 如何使用Salesforce工作流模型將用戶AEM作為銷售人員過帳。
* 如何建立顯示來自Salesforce的資料的元件。

## 配置AEM以與Salesforce整合 {#configuring-aem-to-integrate-with-salesforce}

要配置AEM以與Salesforce整合，您需要首先在Salesforce中配置遠程訪問應用程式。 然後，您將Salesforce雲服務配置為指向此遠程訪問應用程式。

>[!NOTE]
>
>您可以在Salesforce中建立免費開發人員帳戶。

要配置AEM與Salesforce整合：

>[!CAUTION]
>
>您需要安裝 [Salesforce API](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=salesforce*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=2&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcom.adobe.cq.mcm.salesforce.content-1.0.4.zip) 整合包，然後繼續執行該過程。 有關如何使用包的詳細資訊，請參閱 [如何使用包](/help/sites-administering/package-manager.md#package-share) 的子菜單。

1. 在AEM中，導航到 **Cloud Services**。 在第三方服務中，按一下 **立即配置** 在 **Salesforce**。

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. 建立新配置，例如， **開發者**。

   >[!NOTE]
   >
   >新配置重定向到新頁面： **http://localhost:4502/etc/cloudservices/salesforce/developer.html**。 這與在Salesforce中建立遠程訪問應用程式時在回叫URL中指定的值完全相同。 這些值必須匹配。

1. 登錄到Salesforce帳戶(或者，如果沒有，請在 [https://developer.force.com](https://developer.force.com)。)
1. 在Salesforce中，導航到 **建立** > **應用** 去 **已連接的應用** (在以前版本的salesforce中，工作流 **部署** > **遠程訪問**)。
1. 按一下 **新建** 與SalesforceAEM連接。

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. 輸入 **已連接的應用程式名稱**。 **API名稱**, **聯繫電子郵件**。 選擇 **啟用OAuth設定** 框中，輸入 **回調URL** 並添加OAuth作用域（例如完全訪問）。 回調URL與以下類似： `http://localhost:4502/etc/cloudservices/salesforce/developer.html`

   更改伺服器名稱/埠號和頁名以匹配配置。

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. 按一下 **保存** 保存salesforce配置。 Salesforce建立 **用戶密鑰** 和 **消費者秘密**，這是配置所需AEM的。

   ![chlimage_1-73](assets/chlimage_1-73.png)

   >[!NOTE]
   >
   >您可能需要等待幾分鐘（最多15分鐘），才能激活Salesforce中的遠程訪問應用程式。

1. 在AEM中，導航到 **Cloud Services** 並導航到您之前建立的salesforce配置(例如， **開發者**)。 按一下 **編輯** 從salesforce.com輸入客戶密鑰和客戶密碼。

   ![chlimage_1-15](assets/chlimage_1-15.jpeg)

   | 登入 URL | 這是Salesforce授權終結點。 它的價值是預先填充的，並且適用於大多數情況。 |
   |---|---|
   | 客戶密鑰 | 輸入從salesforce.com中的「遠程訪問應用程式註冊」頁獲取的值 |
   | 客戶機密 | 輸入從salesforce.com中的「遠程訪問應用程式註冊」頁獲取的值 |

1. 按一下 **連接到Salesforce** 連接。 Salesforce請求允許您的配置連接到Salesforce。

   ![chlimage_1-74](assets/chlimage_1-74.png)

   在AEM中，將開啟確認對話框，告訴您已成功連接。

1. 導航到網站的根頁面，然後按一下 **頁面屬性**。 然後選擇 **Cloud Services** 添加 **Salesforce** 並選擇正確的配置(例如， **開發者**)。

   ![chlimage_1-75](assets/chlimage_1-75.png)

   現在，您可以使用工作流模型將銷售線索過帳到Salesforce，並建立訪問Salesforce資料的元件。

## 將用AEM戶導出為Salesforce Lead {#exporting-aem-users-as-salesforce-leads}

如果要將用戶導出AEM為銷售人員線索，則需要配置工作流以將銷售線索過帳到銷售人員。

要將用戶AEM作為Salesforce銷售線索導出，請執行以下操作：

1. 導航至Salesforce工作流(位於 `http://localhost:4502/workflow` 通過按一下右鍵工作流 **Salesforce.com導出** 按一下 **開始**。

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. 選擇要AEM建立為潛在顧客的用戶 **負載** （首頁 — >用戶）。 請確保選擇用戶的配置檔案節點，因為它包含諸如 **給定名稱**。 **家族名稱**&#x200B;等等，這些映射到Salesforce線索 **名字** 和 **姓氏** 的子菜單。

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >在啟動此工作流之前，在發佈到Salesforce之前，AEM中的潛在客戶節點必須具有某些必需欄位。 這些 **給定名稱**。 **家族名稱**。 **公司**&#x200B;和 **電子郵件**。 要查看用戶和Salesforce潛在客戶之AEM間映射的完整清單，請參閱 [在用戶和Slaesforce潛AEM在用戶之間映射配置。](#mapping-configuration-between-aem-user-and-salesforce-lead)

1. 按一下&#x200B;**「確定」**。用戶資訊將導出到salesforce.com。 您可以在salesforce.com上驗證。

   >[!NOTE]
   >
   >錯誤日誌將顯示是否導入了潛在顧客。 有關詳細資訊，請檢查錯誤日誌。

### 配置Salesforce.com導出工作流 {#configuring-the-salesforce-com-export-workflow}

您可能需要配置Salesforce.com導出工作流，使其與正確的Salesforce.com配置相匹配，或進行其他更改。

要配置Salesforce.com導出工作流，請執行以下操作：

1. 瀏覽到 `http://localhost:4502/cf#/etc/workflow/models/salesforce-com-export.html.`

   ![chlimage_1-16](assets/chlimage_1-16.jpeg)

1. 開啟Salesforce.com導出步驟，選擇 **參數** ，然後選擇正確的配置，然後按一下 **確定**。 此外，如果希望工作流重新建立在Salesforce中刪除的潛在顧客，請選中複選框。

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. 按一下 **保存** 的子菜單。

   ![chlimage_1-79](assets/chlimage_1-79.png)

### 在用戶和Salesforce LeadAEM之間映射配置 {#mapping-configuration-between-aem-user-and-salesforce-lead}

要查看或編輯用戶與Salesforce銷售線AEM索之間的當前映射配置，請開啟Configuration Manager: `https://<hostname>:<port>/system/console/configMgr` 並搜索 **Salesforce Lead映射配置**。

1. 通過按一下 **Web控制台** 或直接 `https://<hostname>:<port>/system/console/configMgr.`
1. 搜索 **Salesforce Lead映射配置**。

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. 根據需要更改映射。 預設映射遵循模式 **aemUserAttribute=sfLeadAttribute**。 按一下 **保存** 的子菜單。

## 配置Salesforce客戶端上下文儲存 {#configuring-salesforce-client-context-store}

salesforce客戶端上下文儲存顯示有關當前登錄用戶的附加資訊，而不是中已提供的信AEM息。 它根據用戶與Salesforce的連接從Salesforce獲取此附加資訊。

為此，您需要配置以下內容：

1. 通過Salesforce AEM Connect元件將用戶與Salesforce ID連結。
1. 將Salesforce配置檔案資料添加到客戶端上下文頁中，以配置要查看的屬性。
1. （可選）生成使用Salesforce客戶端上下文儲存中資料的段。

### 將用AEM戶與Salesforce ID連結 {#linking-an-aem-user-with-a-salesforce-id}

您需要使用Salesforce AEM ID映射用戶，以便將其載入到客戶端上下文中。 在現實場景中，您將基於已知用戶資料與驗證進行連結。 為了演示，在此過程中，您使用 **Salesforce連接** 元件。

1. 導航到網站，AEM登錄，然後拖放 **Salesforce連接** 從側腳中分出。

   >[!NOTE]
   >
   >如果 **Salesforce連接** 元件不可用，請轉到 **設計** 查看並選擇它，使其可用 **編輯** 的子菜單。

   ![chlimage_1-17](assets/chlimage_1-17.jpeg)

   將元件拖到頁面時，將顯示 **連結到Salesforce=Off**。

   ![chlimage_1-81](assets/chlimage_1-81.png)

   >[!NOTE]
   >
   >此元件僅用於演示。 對於真實情況，將有另一個過程將用戶與線索連結/匹配。

1. 在頁面上拖動元件後，開啟該元件進行配置。 選擇配置、聯繫人類型以及Salesforce線索或聯繫人，然後按一下 **確定**。

   ![chlimage_1-82](assets/chlimage_1-82.png)

   將用AEM戶與Salesforce聯繫人或潛在顧客連結。

   ![chlimage_1-83](assets/chlimage_1-83.png)

### 將Salesforce資料添加到客戶端上下文 {#adding-salesforce-data-to-client-context}

您可以從客戶端上下文中的Salesforce載入用戶資料以用於個性化：

1. 通過在客戶端上下文中導航開啟要擴展的客戶端上下文，例如， `http://localhost:4502/etc/clientcontext/default/content.html.`

   ![chlimage_1-18](assets/chlimage_1-18.jpeg)

1. 拖動 **Salesforce配置檔案資料** 到客戶端上下文的元件。

   ![chlimage_1-19](assets/chlimage_1-19.jpeg)

1. 按兩下元件將其開啟。 選擇 **添加項** 並從下拉清單中選擇一個屬性。 添加任意數量的屬性並選擇 **確定**。

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. 現在，您可以看到在客戶端上下文中顯示的Salesforce中特定於Salesforce的屬性。

   ![chlimage_1-85](assets/chlimage_1-85.png)

### 使用Salesforce客戶端上下文儲存中的資料生成段 {#building-a-segment-using-data-from-salesforce-client-context-store}

您可以生成使用Salesforce客戶端上下文儲存中資料的段。 要執行此操作：

1. 通過轉AEM到 **工具** > **分段** 或者 [http://localhost:4502/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation)。
1. 建立或更新段以包括來自Salesforce的資料。 有關詳細資訊，請參見 [分段](/help/sites-administering/campaign-segmentation.md)。

## 搜索線索 {#searching-leads}

隨附AEM一個示例Search元件，該元件根據給定標準在Salesforce中搜索銷售線索。 此元件說明如何使用Salesforce REST API搜索salesforce對象。 您需要將頁面與Salesforce配置連結起來以跟蹤對salesforce.com的呼叫。

>[!NOTE]
>
>這是一個示例元件，它顯示如何使用Salesforce REST API查詢Salesforce對象。 作為示例，根據您的需求建立更複雜的元件。

要使用此元件：

1. 導航到要使用此配置的頁面。 開啟頁面屬性並選擇 **Cloud Services。** 按一下 **添加服務** 選擇 **Salesforce** 並按一下 **確定**。

   ![chlimage_1-20](assets/chlimage_1-20.jpeg)

1. 將Salesforce搜索元件拖到頁面（前提是已啟用它）。 要啟用它，請轉到「設計」模式，並將其添加到相應區域)。

   ![chlimage_1-21](assets/chlimage_1-21.jpeg)

1. 開啟「搜索」元件並指定搜索參數，然後按一下 **好。**

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. 顯AEM示搜索元件中指定的與指定標準匹配的線索。

   ![chlimage_1-87](assets/chlimage_1-87.png)
