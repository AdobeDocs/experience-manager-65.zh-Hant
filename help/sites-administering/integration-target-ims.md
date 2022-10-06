---
title: 使用IMS與Adobe Target整合
description: 了解如何使用IMS整合AEM與Adobe Target
exl-id: 8ddd86d5-a5a9-4907-b07b-b6552d7afdc8
source-git-commit: eb05fb92491932e4c2489c5adb533bbbae1d2870
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 1%

---

# 使用IMS與Adobe Target整合{#integration-with-adobe-target-using-ims}

AEM透過Target Standard API與Adobe Target整合時，需要使用Adobe Developer主控台設定Adobe IMS(Identity Management系統)。

>[!NOTE]
>
>AEM 6.5新增了對Adobe Target Standard API的支援。Target Standard API使用IMS驗證。
>
>在AEM中使用Adobe Target Classic API仍支援回溯相容性。 此 [Target Classic API使用使用者憑證驗證](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).
>
>API選取由用於AEM/Target整合的驗證方法驅動。
>另請參閱 [租用戶ID和用戶端代碼](#tenant-client) 區段。

## 必備條件 {#prerequisites}

開始此過程之前：

* [Adobe支援](https://helpx.adobe.com/tw/contact/enterprise-support.ec.html) 必須為您配置帳戶：

   * Adobe主控台
   * Adobe Developer Console
   * Adobe Target和
   * Adobe IMS(Identity Management系統)

* 您組織的系統管理員應使用Admin Console，將組織中所需的開發人員新增至相關的產品設定檔。

   * 這可為特定開發人員提供在Adobe Developer主控台中啟用整合的權限。
   * 如需詳細資訊，請參閱 [管理開發人員](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## 設定IMS設定 — 產生公開金鑰 {#configuring-an-ims-configuration-generating-a-public-key}

設定的第一階段是在AEM中建立IMS設定並產生公開金鑰。

1. 在AEM中開啟 **工具** 功能表。
1. 在 **安全性** 節選 **Adobe IMS設定**.
1. 選擇 **建立** 開啟 **Adobe IMS技術帳戶設定**.
1. 使用下拉式清單 **雲端設定**，選取 **Adobe Target**.
1. 啟動 **建立新憑證** 並輸入新別名。
1. 確認為 **建立憑證**.

   ![](assets/integrate-target-io-01.png)

1. 選擇 **下載** (或 **下載公開金鑰**)將檔案下載到本機磁碟，以便在 [設定IMS for Adobe Target與AEM整合](#configuring-ims-for-adobe-target-integration-with-aem).

   >[!CAUTION]
   >
   >請保持此設定開啟，當 [在AEM中完成IMS設定](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-02.png)

## 為Adobe Target設定IMS與AEM整合 {#configuring-ims-for-adobe-target-integration-with-aem}

使用Adobe Developer Console時，您需要與AEM將使用的Adobe Target建立專案（整合），然後指派所需的權限。

### 建立專案 {#creating-the-project}

開啟Adobe Developer Console以使用AEM將使用的Adobe Target建立專案：

1. 開啟專案的Adobe Developer Console:

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. 將顯示您擁有的任何專案。 選擇 **建立新專案**  — 位置和使用取決於：

   * 如果您尚未建立任何專案， **建立新專案** 中間，底部。
      ![建立新專案 — 第一個專案](assets/integration-target-io-02.png)
   * 如果您已有現有專案，則會列出 **建立新專案** 右上角。
      ![建立新專案 — 多個專案](assets/integration-target-io-03.png)


1. 選擇 **新增至專案** 後跟 **API**:

   ![](assets/integration-target-io-10.png)

1. 選擇 **Adobe Target**，然後 **下一個**:

   >[!NOTE]
   >
   >如果您已訂閱Adobe Target，但未看到其列出，則應檢查 [先決條件](#prerequisites).

   ![](assets/integration-target-io-12.png)

1. **上傳您的公開金鑰**，完成時，繼續 **下一個**:

   ![](assets/integration-target-io-13.png)

1. 查看憑據，然後繼續 **下一個**:

   ![](assets/integration-target-io-15.png)

1. 選取所需的產品設定檔，然後繼續 **儲存已設定的API**:

   >[!NOTE]
   >
   >顯示的產品設定檔視您是否具備：
   >
   >* Adobe Target Standard — 僅 **預設工作區** 可用
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

1. 導覽至 **產品** （頂端工具列），然後選取 **Adobe Target - &lt;*your-tenant-id*>** （從左側面板）。
1. 選擇 **產品設定檔**，則會從顯示的清單中取得您所需的工作區。 例如，預設工作區。
1. 選擇 **API憑證**，然後是必要的整合設定。
1. 選擇 **編輯器** 作為 **產品角色**;而非 **觀察者**.

## 儲存於Adobe Developer主控台整合專案的詳細資料 {#details-stored-for-the-ims-integration-project}

從Adobe Developer Console - 「專案」中，您可以看到所有整合專案的清單：

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

選擇 **檢視** （位於特定專案項目的右側），以顯示有關設定的詳細資訊。 這些包括：

* 專案概述
* 分析
* 憑證
   * 服務帳戶(JWT)
      * 憑據詳細資訊
      * 產生JWT
* API
   * 例如，Adobe Target

其中部分作業需要根據IMS完成Adobe Target與AEM的整合。

## 在AEM中完成IMS設定 {#completing-the-ims-configuration-in-aem}

返回AEM後，您可以從Target的Adobe Developer主控台整合新增必要值，以完成IMS設定：

1. 返回 [在AEM中開啟IMS設定](#configuring-an-ims-configuration-generating-a-public-key).
1. 選擇 **下一個**.

1. 您可以在此處使用 [Adobe Developer Console中專案設定的詳細資訊](#details-stored-for-the-ims-integration-project):

   * **標題**:你的簡訊。
   * **授權伺服器**:複製/貼上 `aud` 行 **裝載** 一節，例如 `https://ims-na1.adobelogin.com` 在以下範例中
   * **API金鑰**:從 [概述](#details-stored-for-the-ims-integration-project) 節
   * **用戶端密碼**:在 [概述](#details-stored-for-the-ims-integration-project) 節，並複製
   * **裝載**:從 [產生JWT](#details-stored-for-the-ims-integration-project) 節

   ![](assets/integrate-target-io-10.png)

1. 確認為 **建立**.

1. 您的Adobe Target設定會顯示在AEM主控台中。

   ![](assets/integrate-target-io-11.png)

## 確認IMS設定 {#confirming-the-ims-configuration}

若要確認設定如預期般運作：

1. 開啟:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   例如：

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 選取您的設定。
1. 選擇 **檢查運行狀況** ，後面 **檢查**.

   ![](assets/integrate-target-io-12.png)

1. 如果成功，您會看到訊息：

   ![](assets/integrate-target-io-13.png)

## 設定Adobe TargetCloud Service {#configuring-the-adobe-target-cloud-service}

現在可以參考設定，讓Cloud Service使用Target Standard API:

1. 開啟 **工具** 功能表。 然後，在 **Cloud Services** 部分，選擇 **舊版Cloud Services**.
1. 向下捲動至 **Adobe Target** 選取 **立即配置**.

   此 **建立配置** 對話框將開啟。

1. 輸入 **標題** 如果你願意， **名稱** （若保留為空白，則會從標題產生）。

   您也可以選取所需的範本（如果有多個範本可用）。

1. 確認為 **建立**.

   此 **編輯元件** 對話框將開啟。

1. 在 **Adobe Target設定** 標籤：

   * **驗證**:IMS

   * **租用戶ID**:Adobe IMS租用戶ID。 另請參閱 [租用戶ID和用戶端代碼](#tenant-client) 區段。

      >[!NOTE]
      >
      >針對IMS，此值需要取自Target本身。 您可以登入Target並從URL中擷取租用戶ID。
      >
      >例如，如果URL為：
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >那你就用 `yourtenantid`.

   * **用戶端代碼**:請參閱 [租用戶ID和用戶端代碼](#tenant-client) 區段。

   * **IMS設定**:選取IMS設定的名稱

   * **API類型**:REST

   * **A4T Analytics Cloud設定**:選取用於目標活動目標和量度的Analytics雲端設定。 如果您在鎖定目標內容時使用Adobe Analytics作為報表來源，則需要此功能。 如果您沒有看見雲端設定，請參閱 [設定A4T Analytics Cloud設定](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration).

   * **使用精確定位**:依預設，此核取方塊會選取。 如果選取此選項，雲端服務設定會在載入內容之前等待內容載入。 請參閱以下備注。

   * **從Adobe Target同步區段**:選取此選項可下載Target中定義的區段，以便在AEM中使用。 當API類型屬性為REST時，您必須選取此選項，因為不支援內嵌區段，且您一律需要使用Target中的區段。 (請注意，「區段」的AEM詞語等同於Target「對象」。)

   * **用戶端程式庫**:選取您要AT.js用戶端程式庫或mbox.js（已廢止）。

   * **使用Tag Management系統來傳送用戶端程式庫**:使用DTM（已淘汰）、Adobe啟動或任何其他標籤管理系統。

   * **自訂AT.js**:如果您勾選Tag Management方塊或使用預設的AT.js，請保留空白。 或者上傳自訂AT.js。 只有在您已選取AT.js時才會顯示。
   >[!NOTE]
   >
   >[設定Cloud Service以使用Target Classic API](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) 已遭取代(使用「Adobe Recommendations設定」標籤)。

1. 按一下 **連線至Target** 初始化與Adobe Target的連線。

   如果連線成功，則會顯示訊息 **連接成功** 的下界。

1. 選擇 **確定** 在訊息上，之後 **確定** ，以確認設定。

1. 您現在可以繼續 [新增Target架構](/help/sites-administering/target-configuring.md#adding-a-target-framework) 設定要傳送至Target的ContextHub或ClientContext參數。 請注意，將AEM體驗片段匯出至Target可能不需要此功能。

### 租用戶ID和用戶端代碼 {#tenant-client}

使用 [Adobe Experience Manager 6.5.8.0](/help/release-notes/release-notes.md)，則「用戶端代碼」欄位已新增至「目標設定」視窗。

設定「租用戶ID」和「用戶端代碼」欄位時，請注意下列事項：

1. 對於大部分的客戶，租用戶ID和用戶端代碼都相同。 這表示兩個欄位包含相同的資訊，且相同。 請務必在兩個欄位中輸入租用戶ID。
2. 為了傳統用途，您也可以在租用戶ID和用戶端代碼欄位中輸入不同的值。

在這兩種情況下，請注意：

* 依預設，用戶端代碼（若先新增）也會自動複製到租用戶ID欄位中。
* 您可以選擇變更預設的租用戶ID集。
* 因此，對Target的後端呼叫將以租用戶ID為基礎，而對Target的用戶端呼叫將以用戶端代碼為基礎。

如前所述，第一個案例是AEM 6.5最常見的案例。無論如何，請確定 **both** 欄位會根據您的需求包含正確的資訊。

>[!NOTE]
>
> 如果要變更現有的Target設定：
>
> 1. 重新輸入租用戶ID。
> 2. 重新連線至Target。
> 3. 儲存設定。

