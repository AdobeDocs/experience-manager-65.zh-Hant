---
title: 使用IMS與Adobe Analytics整合
description: 了解如何使用IMS整合AEM與Adobe Analytics
exl-id: 2833a6df-ef32-48ab-8395-0f26816f8443
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 1%

---

# 使用IMS與Adobe Analytics整合 {#integration-with-adobe-analytics-using-ims}

AEM透過Analytics Standard API與Adobe Analytics整合時，需要使用Adobe Developer主控台設定Adobe IMS(Identity Management系統)。

>[!NOTE]
>
>AEM 6.5.12.0中新增了對Adobe Analytics Standard API 2.0的支援。此版本的API支援IMS驗證。
>
>在AEM中使用Adobe Analytics Classic API 1.4仍支援回溯相容性。 此 [Analytics Classic API使用使用者憑證驗證](/help/sites-administering/adobeanalytics-connect.md).
>
>API選取由用於AEM/Analytics整合的驗證方法驅動。
>
>進一步資訊也可在 [移轉至2.0 API](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/).

## 必備條件 {#prerequisites}

開始此過程之前：

* [Adobe支援](https://helpx.adobe.com/tw/contact/enterprise-support.ec.html) 必須為您配置帳戶：

   * Adobe主控台
   * Adobe Developer Console
   * Adobe Analytics和
   * Adobe IMS(Identity Management系統)

* 您組織的系統管理員應使用Admin Console，將組織中所需的開發人員新增至相關的產品設定檔。

   * 這可為特定開發人員提供在Adobe Developer主控台中啟用整合的權限。
   * 如需詳細資訊，請參閱 [管理開發人員](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## 設定IMS設定 — 產生公開金鑰 {#configuring-an-ims-configuration-generating-a-public-key}

設定的第一階段是在AEM中建立IMS設定並產生公開金鑰。

1. 在AEM中開啟 **工具** 功能表。
1. 在 **安全性** 節選 **Adobe IMS設定**.
1. 選擇 **建立** 開啟 **Adobe IMS技術帳戶設定**.
1. 使用下拉式清單 **雲端設定**，選取 **Adobe Analytics**.
1. 啟動 **建立新憑證** 並輸入新別名。
1. 確認為 **建立憑證**.

   ![](assets/integrate-analytics-io-01.png)

1. 選擇 **下載** (或 **下載公開金鑰**)將檔案下載到本機磁碟，以便在 [設定IMS for Adobe Analytics與AEM整合](#configuring-ims-for-adobe-analytics-integration-with-aem).

   >[!CAUTION]
   >
   >請保持此設定開啟，當 [在AEM中完成IMS設定](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-analytics-io-02.png)

## 為Adobe Analytics設定IMS與AEM整合 {#configuring-ims-for-adobe-analytics-integration-with-aem}

使用Adobe Developer Console時，您需要使用Adobe Analytics建立專案（整合）(以供AEM使用)，然後指派所需的權限。

### 建立專案 {#creating-the-project}

開啟Adobe Developer Console以使用AEM將使用的Adobe Analytics建立專案：

1. 開啟專案的Adobe Developer Console:

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. 將顯示您擁有的任何專案。 選擇 **建立新專案**  — 位置和使用取決於：

   * 如果您尚未建立任何專案， **建立新專案** 中間，底部。
      ![建立新專案 — 第一個專案](assets/integration-analytics-io-02.png)
   * 如果您已有現有專案，則會列出 **建立新專案** 右上角。
      ![建立新專案 — 多個專案](assets/integration-analytics-io-03.png)


1. 選擇 **新增至專案** 後跟 **API**:

   ![開始使用您的新專案](assets/integration-analytics-io-10.png)

1. 選擇 **Adobe Analytics**，然後 **下一個**:

   >[!NOTE]
   >
   >如果您已訂閱Adobe Analytics，但未看到其列出，則應檢查 [先決條件](#prerequisites).

   ![新增API](assets/integration-analytics-io-12.png)

1. 選擇 **服務帳戶(JWT)** 作為驗證類型，請繼續 **下一個**:

   ![選擇身份驗證類型](assets/integration-analytics-io-12a.png)

1. **上傳您的公開金鑰**，完成時，繼續 **下一個**:

   ![上傳您的公開金鑰](assets/integration-analytics-io-13.png)

1. 查看憑據，然後繼續 **下一個**:

   ![查看憑據](assets/integration-analytics-io-15.png)

1. 選取所需的產品設定檔，然後繼續 **儲存已設定的API**:

   ![選取所需的產品設定檔](assets/integration-analytics-io-16.png)

1. 將會確認設定。

### 為整合指派權限 {#assigning-privileges-to-the-integration}

您現在必須將必要的權限指派給整合：

1. 開啟Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. 導覽至 **產品** （頂端工具列），然後選取 **Adobe Analytics - &lt;*your-tenant-id*>** （從左側面板）。
1. 選擇 **產品設定檔**，則會從顯示的清單中取得您所需的工作區。 例如，預設工作區。
1. 選擇 **API憑證**，然後是必要的整合設定。
1. 選擇 **編輯器** 作為 **產品角色**;而非 **觀察者**.

## 儲存於Adobe Developer主控台整合專案的詳細資料 {#details-stored-for-the-ims-integration-project}

從Adobe Developer專案主控台，您可以看到所有整合專案的清單：

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

選取特定專案項目，以顯示有關設定的詳細資訊。 這些包括：

* 專案概述
* 分析
* 憑證
   * 服務帳戶(JWT)
      * 憑據詳細資訊
      * 產生JWT
* API
   * 例如，Adobe Analytics

其中部分內容需要完成AEM中Adobe Analytics的整合。

## 在AEM中完成IMS設定 {#completing-the-ims-configuration-in-aem}

返回AEM後，您可以從Analytics的整合專案新增所需值，以完成IMS設定：

1. 返回 [在AEM中開啟IMS設定](#configuring-an-ims-configuration-generating-a-public-key).
1. 選擇 **下一個**.

1. 您可以在此處使用 [儲存於Adobe Developer主控台整合專案的詳細資料](#details-stored-for-the-ims-integration-project):

   * **標題**:你的簡訊。
   * **授權伺服器**:複製/貼上 `aud` 行 **裝載** 一節，例如 `https://ims-na1.adobelogin.com` 在以下範例中
   * **API金鑰**:從 **憑證** 區段 [專案概述](#details-stored-for-the-ims-integration-project)
   * **用戶端密碼**:在 [服務帳戶(JWT)區段的用戶端密碼標籤](#details-stored-for-the-ims-integration-project)，並複製
   * **裝載**:從 [生成服務帳戶(JWT)部分的JWT頁簽](#details-stored-for-the-ims-integration-project)

   ![AEM IMS設定詳細資訊](assets/integrate-analytics-io-10.png)

1. 確認為 **建立**.

1. 您的Adobe Analytics設定會顯示在AEM主控台中。

   ![IMS 設定](assets/integrate-analytics-io-11.png)

## 確認IMS設定 {#confirming-the-ims-configuration}

若要確認設定如預期般運作：

1. 開啟:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   例如：

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 選取您的設定。
1. 選擇 **檢查運行狀況** ，後面 **檢查**.

   ![IMS設定 — 檢查運行狀況](assets/integrate-analytics-io-12.png)

1. 如果成功，您會看到確認訊息。

## 設定Adobe Analytics Cloud服務 {#configuring-the-adobe-analytics-cloud-service}

現在可以參考設定，供Cloud Service使用Analytics Standard API:

1. 開啟 **工具** 功能表。 然後，在 **Cloud Services** 部分，選擇 **舊版Cloud Services**.
1. 向下捲動至 **Adobe Analytics** 選取 **立即配置**.

   此 **建立配置** 對話框將開啟。

1. 輸入 **標題** 如果你願意， **名稱** （若保留為空白，則會從標題產生）。

   您也可以選取所需的範本（如果有多個範本可用）。

1. 確認為 **建立**.

   此 **編輯元件** 對話框將開啟。

1. 在 **Analytics設定** 標籤：

   * **驗證**:IMS

   * **IMS設定**:選取IMS設定的名稱

1. 按一下 **連線至Analytics** 初始化與Adobe Analytics的連線。

   如果連線成功，則會顯示訊息 **連接成功** 的下界。

1. 選擇 **確定** 在消息上。

1. 視需要完成其他參數，然後 **確定** ，以確認設定。

1. 您現在可以繼續 [新增Analytics架構](/help/sites-administering/adobeanalytics-connect.md) 設定要傳送至Adobe Analytics的參數。
