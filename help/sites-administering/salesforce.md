---
title: 與Salesforce整合
description: 瞭解如何整合Adobe Experience Manager (AEM)與Salesforce。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 0f3aaa0a-ccfb-4162-97a6-ee5485595d28
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 3%

---


# 與Salesforce整合 {#integrating-with-salesforce}

將Salesforce與Adobe Experience Manager (AEM)整合提供銷售機會管理功能，並使用Salesforce立即提供的現有功能。 您可以設定AEM將銷售機會發佈至Salesforce，並建立可直接從Salesforce存取資料的元件。

AEM與Salesforce之間的雙向及可擴充整合可啟用：

* 組織可充分使用和修改資料，以提升客戶體驗。
* 從行銷到銷售活動的參與。
* 自動從Salesforce資料存放區傳輸及接收資料的組織。

本檔案說明下列各項：

* 如何設定SalesforceCloud Service(設定AEM以與Salesforce整合)。
* 如何在Client Context中使用Salesforce銷售機會/聯絡資訊進行個人化。
* 如何使用Salesforce工作流程模型將AEM使用者發佈到銷售機會中。
* 如何建立可顯示來自Salesforce之資料的元件。

## 設定AEM以與Salesforce整合 {#configuring-aem-to-integrate-with-salesforce}

若要設定AEM以與Salesforce整合，您必須先在Salesforce中設定遠端存取應用程式。 然後您將Salesforce雲端服務設定為指向此遠端存取應用程式。

>[!NOTE]
>
>您可以在Salesforce中建立免費的開發人員帳戶。

若要設定AEM以與Salesforce整合：

>[!CAUTION]
>
>安裝 [Salesforce Api](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=salesforce*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=2&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcom.adobe.cq.mcm.salesforce.content-1.0.4.zip) 在繼續進行程式之前，請先整合套件。 如需有關如何使用套件的詳細資訊，請參閱 [如何使用套件](/help/sites-administering/package-manager.md#package-share) 頁面。

1. 在AEM中導覽至 **Cloud Service**. 在第三方服務中，按一下 **立即設定** 在 **Salesforce**.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. 建立設定，例如， **開發人員**.

   >[!NOTE]
   >
   >新的組態會重新導向至新頁面： **http://localhost:4502/etc/cloudservices/salesforce/developer.html**. 這個值與您在Salesforce中建立遠端存取應用程式時必須在回呼URL中指定的值完全相同。 這些值必須相符。

1. 登入您的Salesforce帳戶(或如果您沒有帳戶，請在 [https://developer.salesforce.com](https://developer.salesforce.com).)
1. 在Salesforce中導覽至 **建立** > **應用程式** 以取得 **連線的應用程式** (在舊版Salesforce中，工作流程為 **部署** > **遠端存取**)。
1. 按一下 **新增** 以便您可以將AEM與Salesforce連線。

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. 輸入 **連線的應用程式名稱**， **API名稱**、和 **連絡人電子郵件**. 選取 **啟用OAuth設定** 核取方塊，並輸入 **回呼URL** 並新增OAuth範圍（例如，完整存取權）。 回呼URL看起來類似這樣： `http://localhost:4502/etc/cloudservices/salesforce/developer.html`

   變更伺服器名稱/連線埠號碼和頁面名稱，以符合您的設定。

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. 按一下 **儲存** 以儲存Salesforce組態。 Salesforce建立 **使用者金鑰** 和 **使用者密碼**，以進行AEM設定。

   ![chlimage_1-73](assets/chlimage_1-73.png)

   >[!NOTE]
   >
   >請等候數分鐘（最多15分鐘），讓Salesforce中的遠端存取應用程式啟動。

1. 在AEM中導覽至 **Cloud Service** 並導覽至您先前建立的Salesforce組態(例如， **開發人員**)。 按一下 **編輯** 並從salesforce.com輸入客戶金鑰和客戶機密。

   ![chlimage_1-15](assets/chlimage_1-15.jpeg)

   | 登入 URL | 這是Salesforce授權端點。 其值會預先填入，並適用於大多數情況。 |
   |---|---|
   | 客戶金鑰 | 輸入從salesforce.com的[遠端存取應用程式註冊]頁面取得的值 |
   | 客戶機密 | 輸入從salesforce.com的[遠端存取應用程式註冊]頁面取得的值 |

1. 按一下 **連線到Salesforce** 以連線。 Salesforce會要求您允許設定連線至Salesforce。

   ![chlimage_1-74](assets/chlimage_1-74.png)

   在AEM中，會開啟確認對話方塊，告訴您已成功連線。

1. 導覽至網站的根頁面，然後按一下 **頁面屬性**. 然後選取 **Cloud Service** 並新增 **Salesforce** 並選取正確的設定(例如， **開發人員**)。

   ![chlimage_1-75](assets/chlimage_1-75.png)

   現在您可以使用工作流程模型將銷售機會發佈至Salesforce，並建立可從Salesforce存取資料的元件。

## 將AEM使用者匯出為Salesforce銷售機會 {#exporting-aem-users-as-salesforce-leads}

如果您想要將AEM使用者匯出為Salesforce銷售機會，請設定將銷售機會發佈至Salesforce的工作流程。

若要將AEM使用者匯出為Salesforce銷售機會：

1. 導覽至Salesforce工作流程，位於 `http://localhost:4502/workflow` 在工作流程上按一下右鍵 **Salesforce.com匯出** 並按一下 **開始**.

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. 選取您要建立為潛在客戶的AEM使用者，作為 **裝載** 此工作流程的相關資訊（首頁>使用者）。 請務必選取使用者的設定檔節點，因為它包含如下資訊 **givenName**、和  **familyName**，對應至Salesforce潛在客戶的 **名字** 和 **姓氏** 欄位。

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >在開始此工作流程之前，AEM中的潛在客戶節點在發佈至Salesforce之前必須具備某些必填欄位。 這些是 **givenName**， **familyName**， **公司**、和 **電子郵件**. 若要檢視AEM使用者與Salesforce潛在客戶之間的完整對應清單，請參閱 [在AEM使用者和Salesforce潛在客戶之間對應設定。](#mapping-configuration-between-aem-user-and-salesforce-lead)

1. 按一下 **確定**. 使用者資訊會匯出至salesforce.com。 您可透過salesforce.com驗證。

   >[!NOTE]
   >
   >錯誤記錄會顯示銷售機會是否已匯入。 如需詳細資訊，請檢視錯誤記錄。

### 設定Salesforce.com匯出工作流程 {#configuring-the-salesforce-com-export-workflow}

如有必要，請設定Salesforce.com匯出工作流程以符合正確的Salesforce.com設定，或進行其他變更。

若要設定Salesforce.com匯出工作流程：

1. 瀏覽至 `http://localhost:4502/cf#/etc/workflow/models/salesforce-com-export.html.`

   ![chlimage_1-16](assets/chlimage_1-16.jpeg)

1. 開啟Salesforce.com匯出步驟，選取 **引數** 標籤，並選取正確的組態，然後按一下 **確定**. 此外，如果您希望工作流程重新建立Salesforce中刪除的銷售機會，請選取核取方塊。

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. 按一下 **儲存** 以儲存變更。

   ![chlimage_1-79](assets/chlimage_1-79.png)

### AEM使用者與Salesforce潛在客戶之間的對應設定 {#mapping-configuration-between-aem-user-and-salesforce-lead}

若要檢視或編輯AEM使用者與Salesforce潛在客戶之間目前的對應組態，請開啟Configuration Manager： `https://<hostname>:<port>/system/console/configMgr` 並搜尋 **Salesforce銷售機會對應設定**.

1. 開啟Configuration Manager，方法是按一下 **網頁主控台** 或直接前往 `https://<hostname>:<port>/system/console/configMgr.`
1. 搜尋 **Salesforce銷售機會對應設定**.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. 視需要變更對應。 預設的對映會遵循該模式 **aemUserAttribute=sfLeadAttribute**. 按一下 **儲存** 以儲存變更。

## 設定Salesforce使用者端內容存放區 {#configuring-salesforce-client-context-store}

Salesforce使用者端內容存放區會顯示目前登入使用者的其他資訊，比AEM中已提供的資訊還多。 它會根據使用者與Salesforce的連線從Salesforce提取此額外資訊。

要執行此操作，請設定下列專案：

1. 透過Salesforce連線元件將AEM使用者與Salesforce ID連結。
1. 將「Salesforce設定檔資料」新增至使用者端內容頁面，讓您設定要檢視的屬性。
1. （選用）建立使用Salesforce Client Context Store資料的區段。

### 將AEM使用者與Salesforce ID連結 {#linking-an-aem-user-with-a-salesforce-id}

使用Salesforce ID對應AEM使用者，以便將其載入使用者端內容。 在真實世界的案例中，您會根據已知的使用者資料連結並進行驗證。 為了示範，在此程式中，您使用 **Salesforce連線** 元件。

1. 導覽至AEM中的網站，登入，然後拖放 **Salesforce連線** sidekick中的元件。

   >[!NOTE]
   >
   >如果 **Salesforce連線** 元件無法使用，請前往 **設計** 檢視並選取它，使其可在 **編輯** 檢視。

   ![chlimage_1-17](assets/chlimage_1-17.jpeg)

   將元件拖曳至頁面時，其顯示 **連結至Salesforce=Off**.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   >[!NOTE]
   >
   >此元件僅供示範之用。 在真實情境中，會有另一個程式可將使用者與潛在客戶連結或比對。

1. 在頁面上拖曳元件後，請開啟元件以對其進行設定。 選取組態、連絡人型別以及Salesforce潛在客戶或連絡人，然後按一下 **確定**.

   ![chlimage_1-82](assets/chlimage_1-82.png)

   AEM會將使用者與Salesforce聯絡人或銷售機會連結在一起。

   ![chlimage_1-83](assets/chlimage_1-83.png)

### 新增Salesforce資料至Client Context {#adding-salesforce-data-to-client-context}

您可以在Client Context中從Salesforce載入使用者資料，以用於個人化：

1. 透過導覽至您要擴充的使用者端內容，例如 `http://localhost:4502/etc/clientcontext/default/content.html.`

   ![chlimage_1-18](assets/chlimage_1-18.jpeg)

1. 拖曳 **Salesforce設定檔資料** 元件至使用者端內容。

   ![chlimage_1-19](assets/chlimage_1-19.jpeg)

1. 按兩下元件以開啟該元件。 選取 **新增專案** 並從下拉式清單中選取屬性。 新增任意數量的屬性並選取 **確定**.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. 現在，您會在使用者端內容中看到Salesforce的Salesforce特定屬性。

   ![chlimage_1-85](assets/chlimage_1-85.png)

### 使用Salesforce使用者端內容存放區的資料建立區段 {#building-a-segment-using-data-from-salesforce-client-context-store}

您可以建立使用Salesforce Client Context Store資料的區段。 若要這麼做：

1. 前往以下位置，導覽至AEM中的分段： **工具** > **細分** 或即將移至 [http://localhost:4502/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation).
1. 建立或更新區段以包含來自Salesforce的資料。 如需詳細資訊，請參閱 [細分](/help/sites-administering/campaign-segmentation.md).

## 搜尋銷售機會 {#searching-leads}

AEM隨附搜尋元件範例，可依據指定條件在Salesforce中搜尋銷售機會。 此元件會示範如何使用Salesforce REST API來搜尋Salesforce物件。 若要觸發對salesforce.com的呼叫，請連結具有Salesforce設定的頁面。

>[!NOTE]
>
>此元件範例說明如何使用Salesforce REST API查詢Salesforce物件。 以為例，根據您的需求建立更複雜的元件。

若要使用此元件：

1. 導覽至您要使用此設定的頁面。 開啟頁面屬性並選取 **Cloud Service。** 按一下 **新增服務** 並選取 **Salesforce** 以及適當的設定，然後按一下 **確定**.

   ![chlimage_1-20](assets/chlimage_1-20.jpeg)

1. 將Salesforce搜尋元件拖曳至頁面（假設該元件已啟用）。 若要啟用它，請移至[設計]模式並將它新增至適當的區域)。

   ![chlimage_1-21](assets/chlimage_1-21.jpeg)

1. 開啟「搜尋」元件並指定搜尋引數，然後按一下 **確定。**

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. AEM會顯示搜尋元件中指定的、符合指定條件的潛在客戶。

   ![chlimage_1-87](assets/chlimage_1-87.png)
