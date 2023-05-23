---
title: 以自適應形式使用Adobe Sign
seo-title: Using Adobe Sign in an adaptive form
description: 啟用電子簽名(Adobe Sign)工作流，以便自動執行簽名工作流，簡化單個和多簽名過程，以及從移動設備以電子方式簽名表單。
seo-description: Enable e-signature (Adobe Sign) workflows for an adaptive form to automate signing workflows, simplify single and multi-signature processes, and to electronically sign forms from mobile devices.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: a8decba9-229d-40a2-992a-3cc8ebefdd6d
source-git-commit: 4714554609a10e58b1c7141696d694fac46887a6
workflow-type: tm+mt
source-wordcount: '3826'
ht-degree: 0%

---

# 使用 [!DNL Adobe Sign] 自適應格式{#using-adobe-sign-in-an-adaptive-form}

[!DNL Adobe Sign] 啟用適應表單的電子簽名工作流。 E-Signatures改進工作流以處理法律、銷售、工資、人力資源管理等領域的文檔。

典型 [!DNL Adobe Sign] 和自適應表單方案，用戶填充自適應表單以申請服務。 例如，申請抵押和信用卡需要所有借款人和共同申請人的合法簽名。 要為類似情形啟用電子簽名工作流，您可以整合 [!DNL Adobe Sign] AEM [!DNL Forms]。 還有幾個示例， [!DNL Adobe Sign] 至：

* 通過完全自動化的計畫書、報價和合同流程從任何設備處成交。
* 更快地完成人力資源流程並為您的員工提供數字型驗。
* 縮短合同週期，加快供應商的上架速度。
* 建立自動化常見流程的數字工作流。

[!DNL Adobe Sign] 集AEM成 [!DNL Forms] 支援：

* 單用戶和多用戶簽名工作流
* 連續和同時簽名工作流
* 格式和格式外簽名體驗
* 以匿名用戶或登錄用戶身份簽名表單
* 動態簽名進程(與整合AEM) [!DNL Forms] 工作流)
* 通過知識庫、電話和社交配置檔案進行身份驗證

瞭解 [使用具有自適應形式的Adobe Sign的最佳做法](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684) 以創造更好的簽名體驗。

## 必備條件 {#prerequisites}

使用前 [!DNL Adobe Sign] 格式：

* 確AEM保 [!DNL Forms] 雲服務配置為使用 [!DNL Adobe Sign]。 有關詳細資訊，請參閱 [整合Adobe Sign與AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)。
* 讓簽名者清單準備好。 您至少需要每個簽名者的電子郵件地址。

## 配置 [!DNL Adobe Sign] 自適應窗體 {#configure-adobe-sign-for-an-adaptive-form}

執行以下步驟以配置 [!DNL Adobe Sign] 對於自適應窗體：

1. [編輯Adobe符號的自適應窗體屬性](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [將Adobe Sign欄位添加到自適應窗體](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [為Adobe Sign啟用自適應窗體](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [為自適應表單選擇Adobe Sign Cloud Service](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [將Adobe Sign簽名者添加到自適應窗體](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [為自適應表單選擇提交操作](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![簽署者詳細資訊](assets/signer_details_new.png)

### 編輯的自適應表單屬性 [!DNL Adobe Sign] {#enableadobesign}

配置自適應表單屬性 [!DNL Adobe Sign] 的子菜單。

[為Adobe Sign建立自適應窗體](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) 介紹了建立基本自適應窗體的步驟。 請參閱 [建立自適應窗體](../../forms/using/creating-adaptive-form.md) 選項。

#### 建立適應窗體 [!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}

執行以下步驟以建立啟用符號的自適應表單：

1. 導航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 點擊 **[!UICONTROL 建立]** 選擇 **[!UICONTROL 自適應窗體]**。 此時將顯示模板清單。 選擇模板並點擊 **[!UICONTROL 下一個]**。
1. 在 **[!UICONTROL 基本]** 頁籤：

   1. 指定 **[!UICONTROL 名稱]** 和 **[!UICONTROL 標題]** 的上界。

   1. 選擇 [配置容器](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 配置時建立 [!DNL Adobe Sign] AEM [!DNL Forms]。

      >[!NOTE]
      >
      >的 **[!UICONTROL Adobe Sign Cloud Service]** 下拉清單顯示在此欄位中選擇的配置容器中配置的雲服務。 的 **[!UICONTROL Adobe Sign Cloud Service]** 下拉清單在 **[!UICONTROL 電子簽名]** 的子菜單。 **[!UICONTROL 啟用Adobe Sign]** 的雙曲餘切值。

1. 在 **[!UICONTROL 窗體模型]** 頁籤中，選擇以下選項之一：

   * 選擇 **[!UICONTROL 將表單模板與記錄文檔模板關聯]** 的子菜單。 如果使用基於表單模板的自適應表單，則發送用於簽名的文檔只顯示那些基於關聯表單模板的欄位。 它不顯示自適應表單的所有欄位。

   * 選擇 **[!UICONTROL 生成記錄文檔]** 的雙曲餘切值。 如果使用啟用了「記錄文檔」選項的自適應表單，則為簽名而發送的文檔將顯示自適應表單的所有欄位。

1. 點擊 **[!UICONTROL 建立。]** 建立啟用符號的自適應表單，該表單可用於添加 [!DNL Adobe Sign] 的子菜單。

#### 編輯適應窗體 [!DNL Adobe Sign] {#editafsign}

執行以下步驟以使用 [!DNL Adobe Sign] 在現有的自適應格式中：

1. 導航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 選擇自適應窗體並點擊 **[!UICONTROL 屬性]**。
1. 在 **[!UICONTROL 基本]** 頁籤 [配置容器](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 配置時建立 [!DNL Adobe Sign] AEM [!DNL Forms]。
1. 在 **[!UICONTROL 窗體模型]** 頁籤中，選擇以下選項之一：

   * 選擇 **[!UICONTROL 將表單模板與記錄文檔模板關聯]** 的子菜單。 如果使用基於表單模板的自適應表單，則發送用於簽名的文檔只顯示那些基於關聯表單模板的欄位。 它不顯示自適應表單的所有欄位。

   * 選擇 **[!UICONTROL 生成記錄文檔]** 的雙曲餘切值。 如果使用啟用了「記錄文檔」選項的自適應表單，則為簽名而發送的文檔將顯示自適應表單的所有欄位。

1. 點擊 **[!UICONTROL 保存並關閉]**。 自適應窗體已啟用 [!DNL Adobe Sign]。

### 將Adobe Sign欄位添加到自適應窗體 {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] 具有可放置在自適應窗體上的多個欄位。 這些欄位接受各種類型的資料，如簽名、縮寫、公司或標題，並幫助在簽名期間收集額外資訊以及簽名。 您可以使用 [!DNL Adobe Sign] 阻止要放置的元件 [!DNL Adobe Sign] 以自適應形式顯示各個位置的欄位。

執行以下步驟，將欄位添加到自適應表單並定制與這些欄位相關的各種選項：

1. 拖放 **[!UICONTROL Adobe Sign街]** 從元件瀏覽器到自適應窗體的元件。 的 [!DNL Adobe Sign] 塊元件支援所有 [!DNL Adobe Sign] 的子菜單。 預設情況下，它會添加 **簽名** 的子菜單。

   ![標籤塊](assets/sign_block_new.png)

   預設情況下， [!DNL Adobe Sign] 塊在已發佈的自適應窗體中不可見。 僅在簽名文檔中可見。 可以更改 [!DNL Adobe Sign] 阻止 [!DNL Adobe Sign] 阻止元件。

   >[!NOTE]
   >
   >    * 使用 [!DNL Adobe Sign] 塊不是強制使用的 [!DNL Adobe Sign] 的形式。 如果你不用 [!DNL Adobe Sign] 阻止和添加簽名者的欄位，然後在簽名文檔底部顯示預設簽名欄位。
   >    * 使用 [!DNL Adobe Sign] 僅用於自動生成「記錄文檔」的那些自適應表單。 如果使用自定義XDP生成記錄文檔或基於表單模板的自適應表單， [!DNL Adobe Sign] 不支援塊。


1. 選擇 **[!UICONTROL Adobe Sign街]** 並點擊 **編輯** ![aem_6_3_edit](assets/aem_6_3_edit.png) 表徵圖 它顯示用於添加欄位和設定欄位外觀格式的選項。

   ![adobe符號塊選擇欄位](assets/adobe-sign-block-select-fields.png)

   **答：** 選擇並添加 [!DNL Adobe Sign] 的子菜單。 **B** 展開 [!DNL Adobe Sign] 阻止進入全屏視圖

1. 點擊 **[!UICONTROL Adobe Sign] 欄位** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) 表徵圖 它顯示要選擇和添加的選項 [!DNL Adobe Sign] 的子菜單。

   展開 **[!UICONTROL 類型]** 下拉欄位以選擇 [!DNL Adobe Sign] 欄位並點擊「完成」 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 表徵圖，將選定欄位添加到 [!DNL Adobe Sign] 框。 的 **[!UICONTROL 類型]** 下拉欄位包括「簽名」、「簽名者資訊」和「資料」欄位類型。 [!DNL Adobe Sign] 集AEM成 [!DNL Forms] 中列出的支援欄位 [!UICONTROL 類型] 僅下拉框。 有關 [!DNL Adobe Sign] 欄位，請參閱 [Adobe Sign文檔](https://helpx.adobe.com/sign/help/field-types.html)。

   ![adobe符號塊欄位選項](assets/adobe-sign-block-fields-options.png)

   必須為欄位提供唯一名稱。 您也可以選擇必需選項來標籤必填欄位。 除 **[!UICONTROL 名稱]** 和 **[!UICONTROL 必需]** 選項，某些 [!DNL Adobe Sign] 選項。 例如，蒙版和多行。 此外，為每個名稱指定唯一名稱 [!DNL Adobe Sign] 欄位是否位於相同或不同 [!DNL Adobe Sign] 塊。

   如果選擇 **[!UICONTROL 數字簽名]** 從下拉清單中，可將數字簽名應用到自適應表單：

   * 使用雲簽名線上登錄 [數字身份證](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 由信任服務提供商托管。
   * 通過使用智慧卡、USB令牌或基於檔案的數字ID下載帶Adobe Acrobat或Reader的文檔進行本地下載。

### 啟用 [!DNL Adobe Sign] 自適應窗體 {#enableadobsignforanadaptiveform}

出局了， [!DNL Adobe Sign] 未為自適應窗體啟用。 執行以下步驟以啟用它：

1. 在內容瀏覽器中，點擊 **[!UICONTROL 窗體容器]**，然後按一下 **[!UICONTROL 配置]** ![配置](assets/configure.png) 表徵圖 它開啟屬性瀏覽器並顯示「自適應表單」容器屬性。
1. 在屬性瀏覽器中，展開 **[!UICONTROL 電子簽名]** 折疊式，然後 **[!UICONTROL 啟用Adobe Sign]** 的雙曲餘切值。 它啟用 [!DNL Adobe Sign] 的雙曲余弦值。

### 選擇 [!DNL Adobe Sign] Cloud Service和簽名訂單 {#selectadobesigncloudserviceforanadaptiveform}

可以配置多個 [!DNL Adobe Sign] 實例的服AEM務 [!DNL Forms]。 建議為每個職能（人力資源、財務等）單獨提供一套服務。 它使跟蹤和報告已簽署的文檔變得更容易。 例如，銀行有多個部門。 您可以為每個部門單獨配置以更好地跟蹤文檔。

文檔也可以具有多個簽名器。 例如，信用卡申請可以具有多個申請人。 銀行在開始處理申請前需要所有申請人的簽名。 對於多簽名者方案，您可以選擇按順序或同時順序對文檔進行簽名。

執行以下步驟以選擇雲服務和簽名順序：

![雲服務](assets/cloud-service.png)

1. 在內容瀏覽器中，點擊 **[!UICONTROL 窗體容器]**，然後按一下 **[!UICONTROL 配置]** ![配置](assets/configure.png) 表徵圖 它開啟屬性瀏覽器並顯示「自適應表單」容器屬性。
1. 在屬性瀏覽器中，展開 **[!UICONTROL 電子簽名]** 折疊式，然後 **[!UICONTROL 啟用Adobe Sign]** 的雙曲餘切值。 它啟用 [!DNL Adobe Sign] 的雙曲余弦值。
1. 從已配置的 [!DNL Adobe Sign] Cloud Services。

   如果 **[!UICONTROL Adobe Sign Cloud Service]** 清單為空，請遵循 [將Adobe Sign配置為AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) 配置服務的文章。

   下拉清單列出了中存在的雲服務 `global` 「工具」>中的資料夾 **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**。 此外，下拉清單還列出了您在中選擇的資料夾中存在的雲服務 **[!UICONTROL 配置容器]** 的子菜單。

1. 從 **[!UICONTROL 簽名者可以簽名]** 對話框。 [!DNL Adobe Sign] 歌手可以簽署適應性表格 **[!UICONTROL 順序]**  — 一個接一個的簽名人，或 **[!UICONTROL 同時]**  — 按任意順序排列。

   按順序，一個簽名者一次接收用於簽名的表單。 簽名人完成對文檔的簽名後，表單會發送給下一個簽名人等。

   同時，多個簽名者可以一次簽署表單。

1. [將簽名者添加到自適應窗體](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) 點擊「完成」 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 表徵圖。


### 將簽名者添加到自適應窗體 {#addsignerstoanadaptiveform}

對於自適應表單，只能有一個簽名者或多個簽名者。 添加簽名者時，還可以配置簽名者的驗證詳細資訊。 您還可以選擇表單填寫者和歌手是否是同一人。 執行以下步驟以添加並提供有關簽名者的各種詳細資訊：

1. 在內容瀏覽器中，點擊 **[!UICONTROL 窗體容器]**，然後按一下 **[!UICONTROL 配置]** ![配置](assets/configure.png) 表徵圖 它開啟帶有Adaptive Form容器屬性的屬性瀏覽器。
1. 在屬性瀏覽器中，展開 **[!UICONTROL 電子簽名]** 折疊式，然後 **[!UICONTROL 啟用Adobe Sign]** 的雙曲餘切值。 它啟用 [!DNL Adobe Sign] 的雙曲余弦值。
1. 點擊 **[!UICONTROL 添加簽名者]** 在 **[!UICONTROL 簽名者配置]**。 它會向自適應表單中添加簽名者。 可以添加多個 [!DNL Adobe Sign] 自適應格式的簽名者。
   ![電話詳細資訊](assets/phone-details.png)

1. 按一下 **編輯** ![aem_6_3_edit](assets/aem_6_3_edit.png) 表徵圖以指定有關簽名者的以下資訊：

   * **[!UICONTROL 標題]:** 指定唯一標識簽名者的標題。

   * **[!UICONTROL 簽署者和人員在填寫相同的表單嗎？]:** 選擇 **是**，如果表單填寫者和第一簽名者是同一人。 如果選項設定為 **不，** 然後，不要在自適應表單中使用簽名步驟元件。 如果表單包含「簽名步驟」元件，則欄位將自動設定為「是」。

   * **[!UICONTROL 簽名者電子郵件地址]:** 指定簽名者的電子郵件地址。 簽名人將收到指定電子郵件地址上的要簽名的文檔/表單。 您可以選擇使用表單域、登錄用戶的用戶配置AEM檔案中提供的電子郵件地址，或手動輸入電子郵件地址。 這是強制性的一步。 確保第一個簽名者或唯一簽名者（如果是單個簽名者）的電子郵件地址與 [!DNL Adobe Sign] 用於配置AEM雲服務的帳戶。

   * **[!UICONTROL 簽名者認證方法]:** 指定在開啟用於簽名的表單之前驗證用戶的方法。 您可以在電話、知識庫和基於社會身份的身份驗證之間進行選擇。
   >[!NOTE]
   >
   >    * 預設情況下，基於社會身份的身份驗證提供了使用Facebook、Google和LinkedIn進行身份驗證的選項。 您可以聯繫 [!DNL Adobe Sign] 支援以啟用其他社會身份驗證提供程式。


   * **[!DNL Adobe Sign]要填寫或簽名的欄位：** 選擇 [!DNL Adobe Sign] 欄位。 自適應形式可具有多個 [!DNL Adobe Sign] 的子菜單。 您可以選擇為簽名者啟用特定欄位。 該欄位顯示所有可用 [!DNL Adobe Sign] 阻止。 選擇塊時，塊的所有欄位都被選中。 可以使用X表徵圖取消選擇欄位。

   ![簽名者詳細資訊](assets/signer-details.png)

   上圖有兩個示例 [!DNL Adobe Sign] 塊：個人資訊和辦公室詳細資訊

   點擊完成 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 表徵圖 簽名者已添加並配置。

### 為自適應表單選擇提交操作 {#selectsubmitactionforanadaptiveform}

添加 [!DNL Adobe Sign] 欄位到自適應窗體，啟用 [!DNL Adobe Sign] 從窗體容器中選擇 [!DNL Adobe Sign] Cloud Service，並添加 [!DNL Adobe Sign] 簽名者，為自適應表單選擇適當的提交操作。 有關自適應表單提交操作的詳細資訊，請參見 [配置提交操作](../../forms/using/configuring-submit-actions.md)。

另外， [!DNL Adobe Sign] 只有在所有簽名者簽署表單後，才提交啟用的自適應表單。 您可以在表單門戶的「掛起簽名」部分中找到部分簽名的表單。 [!DNL Adobe Sign] 配置服務保持輪詢 [!DNL Adobe Sign] 伺服器 [正則區間](../../forms/using/adobe-sign-integration-adaptive-forms.md) 驗證簽名的狀態。 如果所有簽名者都完成了表單的簽名，則啟動提交操作服務並提交表單。 如果您使用自定義提交操作，而表單使用 [!DNL Adobe Sign]，更新自定義提交操作以使用提交操作服務。

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

您的表單簽名體驗已就緒。 您可以預覽表單以驗證簽名體驗。 在出版的表格上， [!DNL Adobe Sign] 當簽名者收到通過電子郵件簽名的表單時，將顯示阻止欄位。 此體驗也稱為格式外簽名體驗。 您也可以為第一個簽名者配置格式內簽名體驗，有關詳細步驟，請參閱 [建立表單簽名體驗](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience)。

## 為自適應表單配置雲簽名 {#configure-cloud-signatures-for-an-adaptive-form}

基於雲的數字簽名或遠程簽名是新一代的數字簽名，可跨案頭、移動和Web工作，並滿足簽名者身份驗證的最高級別合規性和保證。 您可以使用基於雲的數字簽名簽署自適應表單。

之後 [編輯用於Adobe符號的自適應表單屬性](../../forms/using/working-with-adobe-sign.md#enableadobesign)，請執行以下步驟，將雲簽名欄位添加到自適應表單中：

1. 拖放 **[!UICONTROL Adobe Sign街]** 從元件瀏覽器到自適應窗體的元件。 的 [!UICONTROL Adobe Sign街] 元件具有所有受支援的 [!DNL Adobe Sign] 的子菜單。 預設情況下，它會添加 **[!UICONTROL 簽名]** 的子菜單。

   ![標籤塊](assets/sign-block-new.png)

1. 選擇 **[!UICONTROL Adobe Sign街]** 並點擊 **編輯** ![aem_6_3_edit](assets/aem_6_3_edit.png) 表徵圖 它顯示用於添加欄位和設定欄位外觀格式的選項。

   ![adobe符號塊選擇欄位](assets/adobe-sign-block-select-fields.png)

   **答：** 選擇並添加 [!DNL Adobe Sign] 的子菜單。 **B** 展開 [!DNL Adobe Sign] 阻止進入全屏視圖

1. 點擊 **[!UICONTROL Adobe Sign]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) 表徵圖 它顯示要選擇和添加的選項 [!DNL Adobe Sign] 的子菜單。

   展開 **[!UICONTROL 類型]** 要選擇的下拉欄位 **[!UICONTROL 數字簽名]** 點擊 **完成** 表徵圖，將選定欄位添加到 [!DNL Adobe Sign] 框。

   ![數字簽名](assets/digital_signatures_new.png)

   必須為欄位提供唯一名稱。

   將數字簽名應用到自適應表單：

   * 雲簽名：使用 [數字身份證](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 由信任服務提供商托管。
   * Adobe Acrobat或Reader:下載並開啟帶有Adobe Acrobat或Reader的文檔，以使用智慧卡、USB令牌或基於檔案的數字ID進行簽名。

   將雲簽名欄位添加到自適應表單後，請執行以下步驟以完成配置過程：

   * [為Adobe Sign啟用自適應窗體](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [為自適應表單選擇Adobe Sign Cloud Service](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [將Adobe Sign簽名者添加到自適應窗體](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [為自適應表單選擇提交操作](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## 建立表單簽名體驗 {#create-in-form-signing-experience}

用戶還可以在填寫表單時簽署自適應表單。 此體驗也稱為格式簽名體驗。 格式簽名體驗僅對多個簽名者環境中的第一歌手可用。 執行以下步驟為自適應表單建立表單簽名體驗：

1. [添加和配置簽名步驟元件](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)。
1. [添加摘要步驟元件](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component)。

![格式簽名體驗](assets/in_form_signing_experience_new.png)

### 添加和配置簽名步驟元件 {#add-and-configure-the-signature-step-component}

使用「簽名步驟」元件提供一個區域以電子方式對填充的表單簽名。 當呈現包含簽名步驟元件的節時，它將顯示填充表單的可簽名PDF版本。 「簽名步驟」元件佔用表單的全寬。 建議在包含簽名步驟元件的部分上不使用任何其他元件。

執行以下步驟來配置簽名步驟元件：

1. 拖放 **[!UICONTROL 簽名步驟]** 元件。
1. 選擇新添加的簽名步驟元件並點擊 **配置** ![配置](assets/configure.png) 表徵圖 它開啟屬性瀏覽器並顯示簽名步驟屬性。 配置以下屬性：

   * **[!UICONTROL 名稱]**:指定元件的名稱。

   * **[!UICONTROL 標題]:** 指定元件的唯一標題。
   * **[!UICONTROL 模板消息]:** 指定在載入簽名PDF時要顯示的消息。 [!DNL Adobe Sign] 服務需要一些時間來準備和載入簽名PDF。
   * **[!UICONTROL 簽名服務]:** 選擇 **[!DNL Adobe Sign]** 的雙曲餘切值。

   * **[!UICONTROL 使用舊式電子簽名元件]**:如果您在 [AEM Forms工作區](../../forms/using/introduction-html-workspace.md),AEM [!DNL Forms] 應用程式，或底層自適應表單具有舊式電子簽名元件，選擇 **使用舊式電子簽名元件** 的雙曲餘切值。

   * **[!UICONTROL 配置]**:選擇配置([!DNL Adobe Sign] Cloud Service)。 僅當 **使用舊式電子簽名元件** 選項。

   * **[!UICONTROL CSS類]**:指定元件的CSS類。

   點擊完成 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 表徵圖。

   ![簽名步驟](assets/signature_step_new.png)

   >[!NOTE]
   >
   >* 拖放 **[!UICONTROL 簽名步驟]** 元件， **[!UICONTROL 簽名人和填寫表格的人是否相同？]** 選項自動設定為 **是**。 需要使表格保持工作狀態。
   >* 使用「簽名步驟後的摘要步驟」元件獲取最佳體驗。 在簽名步驟元件中完成表單簽名後，「摘要」步驟會自動立即提交表單。 如果不使用摘要步驟，則只有在使用 [Adobe Sign配置服務](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status)。

   >
   >以下幾個最佳做法是：
   >
   >* 包含簽名步驟的自適應表單面板始終位於自適應表單的最後一個或第二個最後一個面板中。 只有在最後一個面板包含「摘要」步驟時，它才能是第二個最後一個面板。
   >* 包含「簽名」或「摘要」步驟元件的面板不能包含任何其他元件。
   >* 包含簽名步驟的自適應表單不能具有提交按鈕。
   >* 包含簽名步驟的自適應表單的提交通過後台服務或摘要步驟處理。 如果有一個配置的簽名者也在填寫表單，則使用「摘要」步驟處理自適應表單提交的好處是，它會立即評估簽名者是否已簽署表單並調用提交操作。 後台服務需要更多時間來評估是否所有配置的簽名者都已簽署表單，並延遲提交自適應表單。
   >* 設計表單，使用戶不能從包含「簽名」或「摘要」步驟的面板中導航回來。



### 配置「感謝」頁或「摘要」步驟元件 {#configure-the-thank-you-page-or-summary-step-component}

的 **摘要步驟** 元件自動提交表單，填充自定義「摘要」頁面中的資訊，並顯示已提交表單的摘要。 它還在返回圖中獲取所需資訊。 「摘要步驟」(Summary Step)元件佔用窗體可用的全形。 建議在包含「摘要步驟」元件的部分上不使用任何其他元件。

現在，表單簽名體驗已就緒。 您可以預覽表單以驗證簽名體驗。

## 常見問題 {#frequently-asked-questions}

**問：** 可以在另一個自適應表單中嵌入自適應表單。 嵌入的自適應形式 [!DNL Adobe Sign] 已啟用？
**答：** 不，AEM [!DNL Forms] 不支援使用嵌入 [!DNL Adobe Sign] 啟用的自適應表單

**問：** 當我使用高級模板建立自適應表單並將其開啟進行編輯時，將出現一條錯誤消息「電子簽名或簽名者配置不正確」。 的子菜單。 如何解決錯誤消息？
**答：** 使用高級模板建立的自適應表單配置為使用 [!DNL Adobe Sign]。 要解決錯誤，請建立並選擇 [!DNL Adobe Sign] 雲配置和配置 [!DNL Adobe Sign] 自適應窗體的簽名者。

**問：** 我能用 [!DNL Adobe Sign] 是否在自適應表單的靜態文本元件中使用文本標籤？
**答：** 是，可以在文本元件中使用文本標籤來添加 [!DNL Adobe Sign] 到 [記錄文檔](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) （僅「自動生成的記錄文檔」選項）啟用自適應表單。 要瞭解建立文本標籤的過程和規則，請參見 [Adobe Sign文檔](https://helpx.adobe.com/sign/using/text-tag.html)。 另請注意，自適應表單對文本標籤的支援有限。 可以使用文本標籤僅建立那些 [Adobe Sign街](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) 支援。

**問：** AEM [!DNL Forms] 提供 [!UICONTROL Adobe Sign] 和簽名步驟元件。 這些功能能否同時以自適應形式使用？
**答：** 可以在窗體中同時使用這兩個元件。 以下是使用這些元件的幾項建議：

**Adobe Sign街：** 您可以使用 [!UICONTROL Adobe Sign街] 添加 [!UICONTROL Adobe Sign] 欄位。 它還有助於為簽名者指定特定欄位。 當預覽或發佈自適應表單時 [!UICONTROL Adobe Sign] 預設情況下，塊不可見。 這些塊僅在簽名文檔中啟用。 在簽名文檔中，僅啟用分配給簽名者的欄位。 [!UICONTROL Adobe Sign] 塊可以與第一和後續簽名器一起使用。

**簽名步驟元件：** 您可以使用簽名步驟元件建立表單簽名體驗。 它只允許第一簽名者在填寫表單時簽名。 當呈現包含簽名步驟元件的節時，它將顯示表單的可簽名PDF版本。 它通常是窗體的最後一個或倒數第二個部分，後面是摘要元件。

## 疑難排解 {#troubleshoot}

### [!DNL Adobe Sign] 協定失敗 {#adobe-sign-agreement-failures}

**問題**
當 [!DNL Adobe Sign] 為自適應表單配置服務，服務無法建立 [!DNL Adobe Sign] 協定。

**解析度**

* 檢查 [Adobe Sign雲服務配置](../../forms/using/adobe-sign-integration-adaptive-forms.md) 在自適應窗體中使用。
* 確保API應用程式 [!DNL Adobe Sign] 用於配置的伺服器 [!DNL Adobe Sign] 雲服務具有所需權限。
* 如果使用多個 [!DNL Adobe Sign] 雲服務，指向 **[!UICONTROL 身份驗證URL]** 所有服務都一樣 **[!UICONTROL Adobe Sign·沙德]**。

* 使用單獨的電子郵件地址來配置 [!DNL Adobe Sign] 帳戶和第一個簽名者和單個簽名者。 第一個簽名者或唯一簽名者（如果是單個簽名者）的電子郵件地址不能與 [!DNL Adobe Sign] 用於配置AEM雲服務的帳戶。

### AEM [!DNL Forms] 為 [!DNL Adobe Sign] 已啟用自適應窗體未啟動 {#adobe-sign-aem-form-workflow-failures}

**問題**
當 [!DNL Adobe Sign] 為自適應表單配置，使用Invoke配置的工作流 [!DNL Forms] 工作流選項未啟動。

**解析度**

* 使用 [!DNL Adobe Sign] 沒有簽字步驟或表格需要多人簽字AEM, [!DNL Forms] 伺服器等待調度程式確認所有人員都已簽署表單。 只有在所有人員完成簽名後，調度程式才提交自適應表單，並且工作流僅在成功提交自適應表單後啟動。 可以縮短 [調度](adobe-sign-integration-adaptive-forms.md) 以快速間隔檢查表單簽名狀態，並加快表單提交。


## 相關文章 {#related-articles}

* [整合Adobe Sign與AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [使用具有自適應形式的Adobe Sign的最佳做法](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [使用Adobe Sign與AEM Forms（視頻）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
