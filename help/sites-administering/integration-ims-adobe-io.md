---
title: 與Adobe Target整合，使用Adobe I/O
seo-title: Integration with Adobe Target using Adobe I/O
description: 了解如何使用Adobe I/O將AEM與Adobe Target整合
seo-description: Learn about integrating AEM with Adobe Target using Adobe I/O
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
exl-id: ba7abc53-7db8-41b1-a0fa-4e4dbbeca402
source-git-commit: baf68f43decec6631516442c3f9e319ce879696f
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 0%

---

# 與Adobe Target整合，使用Adobe I/O{#integration-with-adobe-target-using-adobe-i-o}

AEM透過Target Standard API與Adobe Target整合時，需要設定Adobe IMS(Identity Management系統)和Adobe I/O。

>[!NOTE]
>
>AEM 6.5新增了對Adobe Target Standard API的支援。Target Standard API使用IMS驗證。
>
>在AEM中使用Adobe Target Classic API仍支援回溯相容性。 [Target Classic API使用使用者憑證驗證](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)。
>
>API選取由用於AEM/Target整合的驗證方法驅動。
>另請參閱[租用戶ID和用戶端代碼](#tenant-client)區段。

## 必備條件 {#prerequisites}

開始此過程之前：

* [Adobe](https://helpx.adobe.com/tw/contact/enterprise-support.ec.html) 支援必須為以下項目配置您的帳戶：

   * Adobe主控台
   * Adobe I/O
   * Adobe Target和
   * Adobe IMS(Identity Management系統)

* 您組織的系統管理員應使用Admin Console，將組織中所需的開發人員新增至相關的產品設定檔。

   * 這可為特定開發人員提供權限，以在Adobe I/O內啟用整合。
   * 如需詳細資訊，請參閱[管理開發人員](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)。


## 設定IMS設定 — 產生公開金鑰 {#configuring-an-ims-configuration-generating-a-public-key}

設定的第一階段是在AEM中建立IMS設定並產生公開金鑰。

1. 在AEM中開啟&#x200B;**工具**&#x200B;功能表。
1. 在&#x200B;**Security**&#x200B;區段中，選取&#x200B;**Adobe IMS設定**。
1. 選擇&#x200B;**Create**&#x200B;以開啟&#x200B;**Adobe IMS Technical Account Configuration**。
1. 使用&#x200B;**雲配置**&#x200B;下拉式清單，選擇&#x200B;**Adobe Target**。
1. 激活&#x200B;**建立新證書**&#x200B;並輸入新別名。
1. 使用&#x200B;**建立憑證**&#x200B;確認。

   ![](assets/integrate-target-io-01.png)

1. 選取&#x200B;**下載**（或&#x200B;**下載公開金鑰**）將檔案下載至本機磁碟，以便在[設定Adobe Target整合的Adobe I/O與AEM](#configuring-adobe-i-o-for-adobe-target-integration-with-aem)時使用。

   >[!CAUTION]
   >
   >保持此設定開啟，當[在AEM](#completing-the-ims-configuration-in-aem)中完成IMS設定時，將會再次需要此設定。

   ![](assets/integrate-target-io-02.png)

## 設定Adobe Target與AEM整合的Adobe I/O {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}

您需要使用AEM將使用的Adobe Target建立Adobe I/O專案（整合），然後指派所需的權限。

### 建立專案 {#creating-the-project}

開啟Adobe I/O主控台，使用AEM將使用的Adobe Target建立I/O專案：

>[!NOTE]
>
>另請參閱[Adobe I/O教學課程](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html)。

1. 開啟專案的Adobe I/O主控台：

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. 將顯示您擁有的任何專案。 選擇&#x200B;**建立新項目** — 位置和使用情況將取決於：

   * 如果您尚未有任何專案，**建立新專案**將位於中央底部。
      ![建立新專案 — 第一個專案](assets/integration-target-io-02.png)
   * 如果您已有現有專案，則會列出這些專案，而右上角會是&#x200B;**建立新專案**。
      ![建立新專案 — 多個專案](assets/integration-target-io-03.png)


1. 選擇&#x200B;**添加到項目**，後跟&#x200B;**API**:

   ![](assets/integration-target-io-10.png)

1. 選擇&#x200B;**Adobe Target**，然後選擇&#x200B;**Next**:

   >[!NOTE]
   >
   >如果您已訂閱Adobe Target，但未看到其列出，則應檢查[Prerequestes](#prerequisites)。

   ![](assets/integration-target-io-12.png)

1. **上傳您的公開金鑰**，並在完成時繼續進行下 **一步**:

   ![](assets/integration-target-io-13.png)

1. 查看憑據，然後繼續&#x200B;**Next**:

   ![](assets/integration-target-io-15.png)

1. 選取所需的產品設定檔，然後繼續&#x200B;**儲存已設定的API**:

   >[!NOTE]
   >
   >顯示的產品設定檔視您是否具備：
   >
   >* Adobe Target Standard — 僅&#x200B;**預設工作區**&#x200B;可用
   >* Adobe Target Premium — 會列出所有可用的工作區，如下所示


   ![](assets/integration-target-io-16.png)

1. 建立將得到確認。

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### 為整合指派權限 {#assigning-privileges-to-the-integration}

您現在必須將必要的權限指派給整合：

1. 開啟Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. 導覽至&#x200B;**Products**（頂端工具列），然後選取&#x200B;**Adobe Target - &lt;*your-tenant-id*>**（從左側面板）。
1. 從顯示的清單中選擇&#x200B;**產品設定檔**，然後選擇所需的工作區。 例如，預設工作區。
1. 選取&#x200B;**整合**，然後是必要的整合設定。
1. 選擇&#x200B;**Editor**&#x200B;作為&#x200B;**Product Role**;而不是&#x200B;**觀察者**。

## 儲存的Adobe I/O整合專案詳細資訊 {#details-stored-for-the-adobe-io-integration-project}

從「Adobe I/O專案」主控台，您可以看到所有整合專案的清單：

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

選擇&#x200B;**View**（特定項目項的右側）以顯示有關配置的詳細資訊。 這些包括：

* 專案概述
* 分析
* 憑證
   * 服務帳戶(JWT)
      * 憑據詳細資訊
      * 產生JWT
* API
   * 例如，Adobe Target

您需要完成AEM中Target的Adobe I/O整合，才能執行其中部分操作。

## 在AEM中完成IMS設定 {#completing-the-ims-configuration-in-aem}

返回AEM後，您就可以從Target的Adobe I/O整合新增必要值，以完成IMS設定：

1. 返回在AEM](#configuring-an-ims-configuration-generating-a-public-key)中開啟的[IMS設定。
1. 選擇&#x200B;**Next**。

1. 您可以在此處使用Adobe I/O](#details-stored-for-the-adobe-io-integration-project)中的[詳細資訊：

   * **標題**:你的簡訊。
   * **授權伺服器**:從下方的Payloads區段 `"aud"` 的行 **** 複製/貼上，例如 `"https://ims-na1.adobelogin.com"` 在以下範例中
   * **API索引鍵**:從TargetAdobe I/O整 [](#details-stored-for-the-adobe-io-integration-project) 合的「概觀」區段複製
   * **用戶端密碼**:在TargetAdobe I/O整 [](#details-stored-for-the-adobe-io-integration-project) 合的「概觀」區段中產生，並複製
   * **裝載**:從TargetAdobe I/O整 [合](#details-stored-for-the-adobe-io-integration-project) 的「產生JWT」區段複製

   ![](assets/integrate-target-io-10.png)

1. 使用&#x200B;**Create**&#x200B;確認。

1. 您的Adobe Target設定會顯示在AEM主控台中。

   ![](assets/integrate-target-io-11.png)

## 確認IMS設定 {#confirming-the-ims-configuration}

若要確認設定如預期般運作：

1. 開啟:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   例如：

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 選取您的設定。
1. 從工具欄中選擇&#x200B;**檢查健康狀態**，然後選擇&#x200B;**檢查**。

   ![](assets/integrate-target-io-12.png)

1. 如果成功，您會看到訊息：

   ![](assets/integrate-target-io-13.png)

## 設定Adobe TargetCloud Service {#configuring-the-adobe-target-cloud-service}

現在可以參考設定，讓Cloud Service使用Target Standard API:

1. 開啟&#x200B;**工具**&#x200B;菜單。 然後，在&#x200B;**Cloud Services**&#x200B;區段內，選取&#x200B;**舊版Cloud Services**。
1. 向下捲動至&#x200B;**Adobe Target**&#x200B;並選取&#x200B;**立即設定**。

   將會開啟&#x200B;**建立配置**&#x200B;對話框。

1. 輸入&#x200B;**Title**，如果需要，輸入&#x200B;**Name**（如果保留為空白，則從標題生成）。

   您也可以選取所需的範本（如果有多個範本可用）。

1. 使用&#x200B;**Create**&#x200B;確認。

   將開啟「**編輯元件**」對話框。

1. 在&#x200B;**Adobe Target設定**&#x200B;標籤中輸入詳細資訊：

   * **驗證**:IMS
   * **租用戶ID**:Adobe IMS租用戶ID。另請參閱[租用戶ID和用戶端代碼](#tenant-client)區段。

      >[!NOTE]
      >
      >針對IMS，此值需要取自Target本身。 您可以登入Target並從URL中擷取租用戶ID。
      >
      >例如，如果URL為：
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >然後，您將使用`yourtenantid`。
   * **用戶端代碼**:請參閱租 [用戶ID和用戶端](#tenant-client) 代碼區段。
   * **IMS設定**:選取IMS設定的名稱
   * **API類型**:REST
   * **A4T Analytics Cloud設定**:選取用於目標活動目標和量度的Analytics雲端設定。如果您在鎖定目標內容時使用Adobe Analytics作為報表來源，則需要此功能。 如果您沒有看見雲端設定，請參閱[設定A4T Analytics Cloud設定](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration)中的附註。

   >[!NOTE]
   >使用者憑證驗證（舊版）無法用於A4T（適用於Target和Analytics）。 因此，客戶應使用     IMS驗證而非使用者憑證驗證。
   * **使用精確鎖定目標**:依預設，此核取方塊會選取。如果選取此選項，雲端服務設定會在載入內容之前等待內容載入。 請參閱以下備注。
   * **從Adobe Target同步區段**:選取此選項可下載Target中定義的區段，以便在AEM中使用。當API類型屬性為REST時，您必須選取此選項，因為不支援內嵌區段，且您一律需要使用Target中的區段。 (請注意，「區段」的AEM詞語等同於Target「對象」。)
   * **用戶端程式庫**:選取您要AT.js用戶端程式庫或mbox.js（已廢止）。
   * **使用標籤管理系統來傳送用戶端程式庫**:使用DTM（已淘汰）、Adobe啟動或任何其他標籤管理系統。
   * **自訂AT.js**:如果您勾選「標籤管理」方塊或使用預設的AT.js，請保留空白。或者上傳自訂AT.js。 只有在您已選取AT.js時才會顯示。

   >[!NOTE]
   >
   >[已棄用配置Cloud Service以使](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) 用Target Classic API(使用Adobe Recommendations設定標籤)。
1. 按一下&#x200B;**連線至Target**&#x200B;以初始化與Adobe Target的連線。

   如果連接成功，則顯示消息&#x200B;**Connection successful**。

1. 在消息上選擇&#x200B;**OK**，然後在對話框上選擇&#x200B;**OK**&#x200B;以確認配置。
1. 您現在可以繼續[新增Target架構](/help/sites-administering/target-configuring.md#adding-a-target-framework)以設定將傳送至Target的ContextHub或ClientContext參數。 請注意，將AEM體驗片段匯出至Target可能不需要此功能。

### 租用戶ID和用戶端代碼 {#tenant-client}

透過[Adobe Experience Manager 6.5.8.0](/help/release-notes/sp-release-notes.md)，「用戶端代碼」欄位已新增至Target設定視窗。

設定「租用戶ID」和「用戶端代碼」欄位時，請注意下列事項：

1. 對於大部分的客戶，租用戶ID和用戶端代碼都相同。 這表示兩個欄位包含相同的資訊，且相同。 請務必在兩個欄位中輸入租用戶ID。
2. 為了傳統用途，您也可以在租用戶ID和用戶端代碼欄位中輸入不同的值。

在這兩種情況下，請注意：

* 依預設，用戶端代碼（若先新增）也會自動複製到租用戶ID欄位中。
* 您可以選擇變更預設的租用戶ID集。
* 因此，對Target的後端呼叫將以租用戶ID為基礎，而對Target的用戶端呼叫將以用戶端代碼為基礎。

如前所述，AEM 6.5中最常見的第一個案例。無論如何，請根據您的需求確保&#x200B;**兩個**&#x200B;欄位都包含正確的資訊。

>[!NOTE]
>
> 如果要變更現有的Target設定：
>
> 1. 重新輸入租用戶ID。
> 2. 重新連線至Target。
> 3. 儲存設定。

