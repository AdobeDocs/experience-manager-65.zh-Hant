---
title: 與Salesforce整合
seo-title: Integrating with Salesforce
description: 了解如何整合AEM與Salesforce。
seo-description: Learn about integrating AEM with Salesforce.
uuid: 3d6a249d-082f-4a10-b255-96482ccd2c65
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bee7144e-4276-4e81-a3a0-5b7273af34fe
docset: aem65
exl-id: 0f3aaa0a-ccfb-4162-97a6-ee5485595d28
source-git-commit: 6f509ad2ae488d8baec790b7719305a5af49887c
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 0%

---


# 與Salesforce整合 {#integrating-with-salesforce}

將Salesforce與AEM整合提供銷售機會管理功能，並運用Salesforce現成提供的功能。 您可以設定AEM以將銷售機會張貼至Salesforce，並建立可直接從Salesforce存取資料的元件。

AEM與Salesforce之間雙向且可擴充的整合可讓：

* 組織可充分使用和更新資料以增強客戶體驗。
* 從行銷到銷售活動的參與。
* 從Salesforce資料存放區自動傳送和接收資料的組織。

本檔案說明下列項目：

* 如何配置SalesforceCloud Services(配置AEM以與Salesforce整合)。
* 如何在「客戶內容」和「個人化」中使用Salesforce銷售機會/聯絡資訊。
* 如何使用Salesforce工作流程模型將AEM使用者作為銷售人員。
* 如何建立顯示來自Salesforce資料的元件。

## 配置AEM以與Salesforce整合 {#configuring-aem-to-integrate-with-salesforce}

要配置AEM以與Salesforce整合，您需要先在Salesforce中配置遠程訪問應用程式。 然後，您將salesforce雲服務配置為指向此遠程訪問應用程式。

>[!NOTE]
>
>您可以在Salesforce中建立免費的開發人員帳戶。

要配置AEM以與Salesforce整合，請執行以下操作：

>[!CAUTION]
>
>您必須安裝 [Salesforce Force API](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/com.adobe.cq.mcm.salesforce.content) 整合套件，再繼續進行程式。 如需如何使用套件的詳細資訊，請參閱 [如何使用套件](/help/sites-administering/package-manager.md#package-share) 頁面。

1. 在AEM中，導覽至 **Cloud Services**. 在第三方服務中，按一下 **立即配置** in **Salesforce**.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. 建立新設定，例如 **開發人員**.

   >[!NOTE]
   >
   >新設定會重新導向至新頁面： **http://localhost:4502/etc/cloudservices/salesforce/developer.html**. 這與您在Salesforce中建立遠端存取應用程式時需要在回撥URL中指定的值完全相同。 這些值必須符合。

1. 登入您的salesforce帳戶(或者，如果您沒有帳戶，請在建立帳戶 [https://developer.force.com](https://developer.force.com).)
1. 在Salesforce中，導覽至 **建立** > **應用程式** 到 **連接的應用** (在舊版salesforce中，工作流程為 **部署** > **遠程訪問**)。
1. 按一下 **新增** 將AEM與Salesforce連線。

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. 輸入 **連線的應用程式名稱**, **API名稱**，和 **聯絡電子郵件**. 選取 **啟用OAuth設定** 核取方塊並輸入 **回呼URL** 並新增OAuth範圍（例如完整存取）。 回呼URL看起來類似以下： `http://localhost:4502/etc/cloudservices/salesforce/developer.html`

   更改伺服器名稱/埠號和頁名以匹配您的配置。

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. 按一下 **儲存** 以儲存salesforce設定。 Salesforce會建立 **使用者金鑰** 和 **使用者密碼**，而您需要AEM設定。

   ![chlimage_1-73](assets/chlimage_1-73.png)

   >[!NOTE]
   >
   >您可能需要等待幾分鐘（最多15分鐘），才能激活Salesforce中的遠程訪問應用程式。

1. 在AEM中，導覽至 **Cloud Services** 並導覽至您先前建立的salesforce設定(例如， **開發人員**)。 按一下 **編輯** 並從salesforce.com輸入客戶密鑰和客戶密碼。

   ![chlimage_1-15](assets/chlimage_1-15.jpeg)

   | 登入 URL | 這是Salesforce授權端點。 其值會預先填入，且適用於大部分的情況。 |
   |---|---|
   | 客戶金鑰 | 輸入從salesforce.com的「遠程訪問應用程式註冊」頁獲取的值 |
   | 客戶密碼 | 輸入從salesforce.com的「遠程訪問應用程式註冊」頁獲取的值 |

1. 按一下 **連接到Salesforce** 來連接。 Salesforce請求允許配置連接到salesforce。

   ![chlimage_1-74](assets/chlimage_1-74.png)

   在AEM中，會開啟確認對話方塊，告訴您連線成功。

1. 導覽至您網站的根頁面，然後按一下 **頁面屬性**. 然後選取 **Cloud Services** 新增 **Salesforce** 並選取正確的設定(例如 **開發人員**)。

   ![chlimage_1-75](assets/chlimage_1-75.png)

   現在，您可以使用工作流模型將銷售機會張貼到Salesforce，並建立可從Salesforce存取資料的元件。

## 將AEM使用者匯出為Salesforce銷售機會 {#exporting-aem-users-as-salesforce-leads}

如果要將AEM使用者匯出為salesforce銷售機會，您需要設定工作流程以將銷售機會張貼至salesforce。

要將AEM用戶導出為Salesforce銷售線索，請執行以下操作：

1. 在導覽至Salesforce工作流程 `http://localhost:4502/workflow` 以滑鼠右鍵按一下工作流程 **Salesforce.com導出** 按一下 **開始**.

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. 選取您要建立作為銷售機會的AEM使用者作為 **裝載** （首頁 — >使用者）。 請務必選取使用者的設定檔節點，因為節點包含下列資訊 **givenName**, **familyName**&#x200B;等，這些會對應至Salesforce銷售機會的 **名字** 和 **LastName** 欄位。

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >開始此工作流程之前，AEM中的銷售機會節點在發佈至Salesforce之前必須具備某些必要欄位。 這些是 **givenName**, **familyName**, **公司**&#x200B;和 **電子郵件**. 要查看AEM用戶與Salesforce銷售線索之間的映射的完整清單，請參閱 [AEM使用者與Slaesforce銷售機會之間的對應設定。](#mapping-configuration-between-aem-user-and-salesforce-lead)

1. 按一下&#x200B;**「確定」**。用戶資訊將導出到salesforce.com。 您可以在salesforce.com驗證。

   >[!NOTE]
   >
   >錯誤記錄會顯示是否已匯入銷售機會。 查看錯誤日誌以了解詳細資訊。

### 配置Salesforce.com導出工作流 {#configuring-the-salesforce-com-export-workflow}

您可能需要配置Salesforce.com導出工作流，使其與正確的Salesforce.com配置相匹配，或進行其他更改。

要配置Salesforce.com導出工作流，請執行以下操作：

1. 導航到 `http://localhost:4502/cf#/etc/workflow/models/salesforce-com-export.html.`

   ![chlimage_1-16](assets/chlimage_1-16.jpeg)

1. 開啟「Salesforce.com匯出」步驟，選取 **引數** 頁簽，然後選擇正確的配置，然後按一下 **確定**. 此外，如果希望工作流重新建立已在Salesforce中刪除的銷售機會，請選中複選框。

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. 按一下 **儲存** 來儲存變更。

   ![chlimage_1-79](assets/chlimage_1-79.png)

### 在AEM使用者和Salesforce Lead之間對應設定 {#mapping-configuration-between-aem-user-and-salesforce-lead}

要查看或編輯AEM用戶和Salesforce銷售線索之間的當前映射配置，請開啟Configuration Manager: `https://<hostname>:<port>/system/console/configMgr` 和搜索 **Salesforce銷售機會映射配置**.

1. 按一下「 」，開啟「設定管理器」 **Web主控台** 或直接前往 `https://<hostname>:<port>/system/console/configMgr.`
1. 搜尋 **Salesforce銷售機會映射配置**.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. 視需要變更對應。 預設對應遵循模式 **aemUserAttribute=sfLeadAttribute**. 按一下 **儲存** 來儲存變更。

## 配置Salesforce客戶端上下文儲存 {#configuring-salesforce-client-context-store}

salesforce用戶端內容存放區會顯示目前登入使用者的其他資訊，而非AEM中已有的資訊。 它會根據使用者與Salesforce的連線，從Salesforce提取此額外資訊。

若要這麼做，您必須設定下列項目：

1. 透過Salesforce Connect元件將AEM使用者與Salesforce ID連結。
1. 將Salesforce設定檔資料新增至用戶端內容頁面，以設定您要查看的屬性。
1. （選用）建立使用Salesforce用戶端內容存放區資料的區段。

### 將AEM使用者與Salesforce ID連結 {#linking-an-aem-user-with-a-salesforce-id}

您需要將AEM使用者對應為Salesforce ID，才能在用戶端內容中載入。 在實際案例中，您會根據已知使用者資料與驗證進行連結。 為了示範，在此程式中，您會使用 **Salesforce Connect** 元件。

1. 導覽至AEM中的網站、登入，並拖放 **Salesforce Connect** 元件。

   >[!NOTE]
   >
   >若 **Salesforce Connect** 元件無法使用，請移至 **設計** 檢視並選取它，以便在 **編輯** 檢視。

   ![chlimage_1-17](assets/chlimage_1-17.jpeg)

   將元件拖曳至頁面時，元件會隨即顯示 **連結到Salesforce=Off**.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   >[!NOTE]
   >
   >此元件僅供示範之用。 對於實際情況，會有另一個程式來連結/比對使用者與銷售機會。

1. 在頁面上拖曳元件後，請開啟它以進行設定。 選擇配置、聯繫人類型和Salesforce銷售線索或聯繫人，然後按一下 **確定**.

   ![chlimage_1-82](assets/chlimage_1-82.png)

   AEM會將使用者與Salesforce連絡人或銷售機會連結。

   ![chlimage_1-83](assets/chlimage_1-83.png)

### 將Salesforce資料添加到客戶端上下文 {#adding-salesforce-data-to-client-context}

您可以在用戶端內容中從Salesforce載入使用者資料，以用於個人化：

1. 在該處導覽以開啟您要延伸的用戶端內容，例如 `http://localhost:4502/etc/clientcontext/default/content.html.`

   ![chlimage_1-18](assets/chlimage_1-18.jpeg)

1. 拖曳 **Salesforce設定檔資料** 元件。

   ![chlimage_1-19](assets/chlimage_1-19.jpeg)

1. 連按兩下元件以開啟它。 選擇 **新增項目** 並從下拉式清單中選取屬性。 新增您想要的屬性並選取 **確定**.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. 現在，您會在用戶端內容中看到Salesforce中的Salesforce特定屬性。

   ![chlimage_1-85](assets/chlimage_1-85.png)

### 使用Salesforce用戶端內容存放區的資料建立區段 {#building-a-segment-using-data-from-salesforce-client-context-store}

您可以建立使用Salesforce客戶端上下文儲存資料的區段。 要執行此操作：

1. 導覽至AEM中的區段，方法是前往 **工具** > **區段** 或 [http://localhost:4502/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation).
1. 建立或更新區段以包含來自Salesforce的資料。 如需詳細資訊，請參閱 [區段](/help/sites-administering/campaign-segmentation.md).

## 搜索銷售線索 {#searching-leads}

AEM隨附範例Search元件，可根據指定條件在Salesforce中搜尋銷售機會。 此元件顯示如何使用Salesforce REST API來搜索salesforce對象。 您需要將頁面與Salesforce設定連結，以觸發對salesforce.com的呼叫。

>[!NOTE]
>
>此元件示例說明如何使用Salesforce REST API來查詢Salesforce對象。 以為例，根據您的需求建立更複雜的元件。

若要使用此元件：

1. 導覽至您要使用此設定的頁面。 開啟頁面屬性並選取 **Cloud Services。** 按一下 **新增服務** 選取 **Salesforce** 並按一下適當的設定 **確定**.

   ![chlimage_1-20](assets/chlimage_1-20.jpeg)

1. 將Salesforce搜尋元件拖曳至頁面（前提是該元件已啟用）。 要啟用它，請轉至「設計」模式，並將其添加到相應區域)。

   ![chlimage_1-21](assets/chlimage_1-21.jpeg)

1. 開啟「搜索」元件並指定搜索參數，然後按一下 **好。**

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. AEM會顯示搜尋元件中指定的與指定准則相符的銷售機會。

   ![chlimage_1-87](assets/chlimage_1-87.png)
