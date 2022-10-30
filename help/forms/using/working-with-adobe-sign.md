---
title: 在最適化表單中使用Adobe Sign
seo-title: Using Adobe Sign in an adaptive form
description: 啟用最適化表單的電子簽名(Adobe Sign)工作流程，以自動化簽署工作流程、簡化單一和多簽名流程，以及從行動裝置以電子方式簽署表單。
seo-description: Enable e-signature (Adobe Sign) workflows for an adaptive form to automate signing workflows, simplify single and multi-signature processes, and to electronically sign forms from mobile devices.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: a8decba9-229d-40a2-992a-3cc8ebefdd6d
source-git-commit: 28d092a7713438c27213766f0bb702b699305b88
workflow-type: tm+mt
source-wordcount: '3826'
ht-degree: 0%

---

# 使用 [!DNL Adobe Sign] 最適化表單{#using-adobe-sign-in-an-adaptive-form}

[!DNL Adobe Sign] 啟用最適化表單的電子簽名工作流程。 電子簽名改進了處理法律、銷售、工資、人力資源管理等領域的文檔的工作流。

在 [!DNL Adobe Sign] 和最適化表單案例，使用者會填入最適化表單以申請服務。 例如，抵押貸款和信用卡申請要求所有借款人和共同申請人簽名。 若要針對類似的情況啟用電子簽名工作流程，您可以整合 [!DNL Adobe Sign] 使用AEM [!DNL Forms]. 您可以使用 [!DNL Adobe Sign] 至：

* 通過完全自動化的計畫書、報價和合同流程從任何設備處理交易。
* 更快完成人力資源流程，並為員工提供數位體驗。
* 縮短合約週期時間，並加快供應商的上線速度。
* 建立可自動化常見流程的數位工作流程。

[!DNL Adobe Sign] 與AEM整合 [!DNL Forms] 支援：

* 單一和多使用者簽署工作流程
* 循序和同時簽署工作流程
* 表單內和表單外簽署體驗
* 以匿名或登入的使用者身分簽署表單
* 動態簽署程式(與AEM整合 [!DNL Forms] 工作流程)
* 通過知識庫、電話和社交配置檔案進行身份驗證

了解 [搭配最適化表單使用Adobe Sign的最佳作法](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684) 以建立更好的簽署體驗。

## 必備條件 {#prerequisites}

使用前 [!DNL Adobe Sign] 在最適化表單中：

* 確保AEM [!DNL Forms] 雲端服務設定為使用 [!DNL Adobe Sign]. 如需詳細資訊，請參閱 [整合Adobe Sign與AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* 讓簽署者清單保持就緒。 您至少需要每個簽署者的電子郵件地址。

## 設定 [!DNL Adobe Sign] 最適化表單 {#configure-adobe-sign-for-an-adaptive-form}

執行下列步驟以設定 [!DNL Adobe Sign] 適用性表單：

1. [編輯Adobe符號的最適化表單屬性](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [將Adobe Sign欄位新增至最適化表單](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [啟用Adobe Sign以建立最適化表單](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [為最適化表單選取Adobe Sign Cloud Service](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [將Adobe Sign簽署者新增至最適化表單](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [為最適化表單選取「提交動作」](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![簽署者詳細資訊](assets/signer_details_new.png)

### 編輯的最適化表單屬性 [!DNL Adobe Sign] {#enableadobesign}

設定適用性表單屬性 [!DNL Adobe Sign] 適用於現有或新的最適化表單。

[建立適用於Adobe Sign的最適化表單](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) 說明建立基本最適化表單的步驟。 請參閱 [建立最適化表單](../../forms/using/creating-adaptive-form.md) 以取得建立最適化表單時可用的其他選項。

#### 為建立最適化表單 [!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}

執行下列步驟以建立已啟用符號的最適化表單：

1. 導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 點選 **[!UICONTROL 建立]** 選取 **[!UICONTROL 適用性表單]**. 隨即顯示範本清單。 選取範本並點選 **[!UICONTROL 下一個]**.
1. 在 **[!UICONTROL 基本]** 標籤：

   1. 指定 **[!UICONTROL 名稱]** 和 **[!UICONTROL 標題]** （適用於最適化表單）。

   1. 選取 [組態容器](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 配置時建立 [!DNL Adobe Sign] 使用AEM [!DNL Forms].

      >[!NOTE]
      >
      >此 **[!UICONTROL Adobe Sign Cloud Service]** 下拉式清單會顯示您在此欄位中選取之設定容器中所設定的雲端服務。 此 **[!UICONTROL Adobe Sign Cloud Service]** 下拉式清單可在 **[!UICONTROL 電子簽名]** 區段(當您選取 **[!UICONTROL 啟用Adobe Sign]** 選項。

1. 在 **[!UICONTROL 表單模型]** 頁簽，選擇以下選項之一：

   * 選取 **[!UICONTROL 將表單模板與記錄文檔模板關聯]** 選項並選擇「記錄文檔」模板。 如果您使用基於表單模板的最適化表單，則為簽名而發送的文檔將僅顯示基於關聯表單模板的那些欄位。 它不會顯示最適化表單的所有欄位。

   * 選取 **[!UICONTROL 生成記錄文檔]** 選項。 如果您使用已啟用「記錄檔案」選項的適用性表單，則為簽署而傳送的檔案會顯示適用性表單的所有欄位。

1. 點選 **[!UICONTROL 建立。]** 已建立可供新增 [!DNL Adobe Sign] 欄位。

#### 編輯最適化表單 [!DNL Adobe Sign] {#editafsign}

執行下列步驟以使用 [!DNL Adobe Sign] 在現有的最適化表單中：

1. 導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 選取最適化表單並點選 **[!UICONTROL 屬性]**.
1. 在 **[!UICONTROL 基本]** 頁簽，選擇 [組態容器](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 配置時建立 [!DNL Adobe Sign] 使用AEM [!DNL Forms].
1. 在 **[!UICONTROL 表單模型]** 頁簽，選擇以下選項之一：

   * 選取 **[!UICONTROL 將表單模板與記錄文檔模板關聯]** 選項並選擇「記錄文檔」模板。 如果您使用基於表單模板的最適化表單，則為簽名而發送的文檔將僅顯示基於關聯表單模板的那些欄位。 它不會顯示最適化表單的所有欄位。

   * 選取 **[!UICONTROL 生成記錄文檔]** 選項。 如果您使用已啟用「記錄檔案」選項的適用性表單，則為簽署而傳送的檔案會顯示適用性表單的所有欄位。

1. 點選 **[!UICONTROL 儲存並關閉]**. 最適化表單已啟用 [!DNL Adobe Sign].

### 將Adobe Sign欄位新增至最適化表單 {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] 有可放置在最適化表單上的各種欄位。 這些欄位接受各種類型的資料，如簽名、縮寫、公司或標題，並幫助在簽名期間收集額外資訊以及簽名。 您可以使用 [!DNL Adobe Sign] 要放置的塊元件 [!DNL Adobe Sign] 最適化表單中不同位置的欄位。

執行下列步驟，將欄位新增至最適化表單，並自訂與這些欄位相關的各種選項：

1. 拖放 **[!UICONTROL Adobe Sign區塊]** 元件從元件瀏覽器移至最適化表單。 此 [!DNL Adobe Sign] 塊元件支援所有 [!DNL Adobe Sign] 欄位。 依預設，會新增 **簽名** 欄位至最適化表單。

   ![符號區塊](assets/sign_block_new.png)

   依預設， [!DNL Adobe Sign] 已發佈的適用性表單中不會顯示區塊。 它只會顯示在簽署檔案中。 您可以變更 [!DNL Adobe Sign] 從 [!DNL Adobe Sign] 阻止元件。

   >[!NOTE]
   >
   >    * 使用 [!DNL Adobe Sign] 塊不是強制使用 [!DNL Adobe Sign] 在最適化表單中。 如果您未使用 [!DNL Adobe Sign] 阻止並添加簽名者的欄位，然後預設簽名欄位顯示在簽名文檔的底部。
   >    * 使用 [!DNL Adobe Sign] 僅針對自動產生記錄檔案的最適化表單封鎖。 如果您使用自訂XDP來產生記錄檔案或表單範本型最適化表單， [!DNL Adobe Sign] 不支援塊。


1. 選取 **[!UICONTROL Adobe Sign區塊]** 元件並點選 **編輯** ![aem_6_3_edit](assets/aem_6_3_edit.png) 表徵圖。 它顯示添加欄位和格式欄位外觀的選項。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **答：** 選取並新增 [!DNL Adobe Sign] 欄位。 **B.** 展開 [!DNL Adobe Sign] 封鎖至全螢幕檢視

1. 點選 **[!UICONTROL Adobe Sign] 欄位** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) 表徵圖。 它會顯示選取和新增的選項 [!DNL Adobe Sign] 欄位。

   展開 **[!UICONTROL 類型]** 下拉欄位以選取 [!DNL Adobe Sign] 欄位並點選「完成」 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 表徵圖，將所選欄位添加到 [!DNL Adobe Sign] 封鎖。 此 **[!UICONTROL 類型]** 下拉欄位包括簽名、簽名者資訊和資料欄位類型。 [!DNL Adobe Sign] 與AEM整合 [!DNL Forms] 支援欄位中列出 [!UICONTROL 類型] 僅下拉框。 如需 [!DNL Adobe Sign] 欄位，請參閱 [Adobe Sign檔案](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   必須為欄位提供唯一名稱。 您也可以選取必要選項，將欄位標示為必填欄位。 除了 **[!UICONTROL 名稱]** 和 **[!UICONTROL 必填]** 選項，部分 [!DNL Adobe Sign] 欄位有更多選項。 例如，遮色片和多行。 此外，請為每個 [!DNL Adobe Sign] 欄位，欄位是位於相同還是不同 [!DNL Adobe Sign] 區塊。

   如果您選取 **[!UICONTROL 數位簽名]** 從下拉式清單中，您可以將數位簽名套用至最適化表單：

   * 線上使用雲簽名來使用 [數位識別碼](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 由信任服務提供商托管。
   * 使用智慧卡、USB代號或檔案式數位ID下載含Adobe Acrobat或Reader的檔案，即可在本機下載。

### 啟用 [!DNL Adobe Sign] 最適化表單 {#enableadobsignforanadaptiveform}

現成可用， [!DNL Adobe Sign] 未針對適用性表單啟用。 執行下列步驟以啟用：

1. 在內容瀏覽器中，點選 **[!UICONTROL 表單容器]**，然後點選 **[!UICONTROL 設定]** ![設定](assets/configure.png) 表徵圖。 它會開啟屬性瀏覽器並顯示適用性表單容器屬性。
1. 在屬性瀏覽器中，展開 **[!UICONTROL 電子簽名]** 折疊式功能表，然後選取 **[!UICONTROL 啟用Adobe Sign]** 選項。 它可讓 [!DNL Adobe Sign] 的URL區段。

### 選擇 [!DNL Adobe Sign] Cloud Service和簽署順序 {#selectadobesigncloudserviceforanadaptiveform}

您可以設定多個 [!DNL Adobe Sign] AEM例項的服務 [!DNL Forms]. 建議為每個職能（人力資源、財務等）分別提供一套服務。 它讓追蹤和報告已簽署的檔案更輕鬆。 例如，銀行有多個部門。 您可以為每個部門分別設定以更好地跟蹤文檔。

文檔還可以有多個簽名者。 例如，信用卡申請可以有多個申請人。 銀行在開始處理申請前要求所有申請人簽名。 對於多簽署者方案，您可以選擇按順序或同時順序對文檔進行簽名。

執行下列步驟以選取雲端服務和簽署順序：

![雲端服務](assets/cloud-service.png)

1. 在內容瀏覽器中，點選 **[!UICONTROL 表單容器]**，然後點選 **[!UICONTROL 設定]** ![設定](assets/configure.png) 表徵圖。 它會開啟屬性瀏覽器並顯示適用性表單容器屬性。
1. 在屬性瀏覽器中，展開 **[!UICONTROL 電子簽名]** 折疊式功能表，然後選取 **[!UICONTROL 啟用Adobe Sign]** 選項。 它可讓 [!DNL Adobe Sign] 的URL區段。
1. 從已設定的 [!DNL Adobe Sign] Cloud Services。

   若 **[!UICONTROL Adobe Sign Cloud Service]** 清單空白，請遵循 [使用AEM Forms設定Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md) 設定服務的文章。

   下拉式清單列出 `global` 「工具」> **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. 此外，下拉式清單也會列出您在 **[!UICONTROL 組態容器]** 欄位。

1. 從 **[!UICONTROL 簽署者可簽署]** 對話框。 [!DNL Adobe Sign] 歌手可以簽署最適化表格 **[!UICONTROL 循序]**  — 一個接一個的簽署者，或 **[!UICONTROL 同時]**  — 無論如何。

   依序，一個簽署者一次會收到要簽署的表單。 簽署者完成對檔案的簽署後，表單會傳送給下一個簽署者，以此類推。

   同時，多位簽署者一次可簽署表單。

1. [將簽署者新增至最適化表單](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) 並點選「完成」 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 圖示以儲存變更。


### 將簽署者新增至最適化表單 {#addsignerstoanadaptiveform}

最適化表單只能有一名或多名簽署者。 添加簽名者時，還可以配置簽名者的驗證詳細資訊。 您也可以選取表單填寫者和歌手是否為同一人。 執行下列步驟來新增及提供與簽署者相關的各種詳細資訊：

1. 在內容瀏覽器中，點選 **[!UICONTROL 表單容器]**，然後點選 **[!UICONTROL 設定]** ![設定](assets/configure.png) 表徵圖。 它會開啟屬性瀏覽器，其中包含適用性表單容器屬性。
1. 在屬性瀏覽器中，展開 **[!UICONTROL 電子簽名]** 折疊式功能表，然後選取 **[!UICONTROL 啟用Adobe Sign]** 選項。 它可讓 [!DNL Adobe Sign] 的URL區段。
1. 點選 **[!UICONTROL 添加簽名者]** 在 **[!UICONTROL 簽署者配置]**. 它會將簽署者新增至最適化表單。 您可以新增多個 [!DNL Adobe Sign] 最適化表單的簽署者。
   ![電話詳細資訊](assets/phone-details.png)

1. 按一下 **編輯** ![aem_6_3_edit](assets/aem_6_3_edit.png) 表徵圖，以指定與簽署者有關的以下資訊：

   * **[!UICONTROL 標題]:** 指定標題以唯一識別簽署者。

   * **[!UICONTROL 簽署者和人員在填寫相同的表單嗎？]:** 選擇 **是**，如果表單填寫者和第一個簽署者是同一人。 如果選項設為 **不，** 然後，請勿在最適化表單中使用簽名步驟元件。 如果表單包含簽名步驟元件，則欄位將自動設定為是。

   * **[!UICONTROL 簽署者電子郵件地址]:** 指定簽署者的電子郵件地址。 簽署者會在指定的電子郵件地址上收到要簽署的檔案/表單。 您可以選擇使用表單欄位中、登入使用者的AEM使用者設定檔中提供的電子郵件地址，或手動輸入電子郵件地址。 這是必要的步驟。 請確定第一個簽署者或唯一簽署者（若是單一簽署者）的電子郵件地址與 [!DNL Adobe Sign] 用來設定AEM雲端服務的帳戶。

   * **[!UICONTROL 簽署者驗證方法]:** 指定在開啟要簽名的表單之前驗證用戶的方法。 您可以在電話、知識庫和社交身份驗證之間進行選擇。
   >[!NOTE]
   >
   >    * 依預設，社交身分驗證提供使用Facebook、Google和LinkedIn進行驗證的選項。 您可以聯絡 [!DNL Adobe Sign] 支援以啟用其他社交驗證提供者。


   * **[!DNL Adobe Sign]要填寫或簽名的欄位：** 選擇 [!DNL Adobe Sign] 簽署者的欄位。 最適化表單可以有多個 [!DNL Adobe Sign] 欄位。 您可以選擇為簽署者啟用特定欄位。 欄位會顯示所有可用 [!DNL Adobe Sign] 封鎖。 選取區塊時，會選取區塊的所有欄位。 您可以使用X圖示來取消選取欄位。

   ![簽署者詳細資訊](assets/signer-details.png)

   上圖有兩個範例 [!DNL Adobe Sign] 區塊：個人資訊和辦公室詳細資訊

   點選完成 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 表徵圖。 已添加並配置簽名者。

### 為最適化表單選取「提交動作」 {#selectsubmitactionforanadaptiveform}

在您之後，新增 [!DNL Adobe Sign] 欄位至最適化表單，啟用 [!DNL Adobe Sign] 從表單容器中，選擇 [!DNL Adobe Sign] Cloud Service，然後新增 [!DNL Adobe Sign] 簽署者，請為最適化表單選取適當的提交動作。 如需適用性表單提交動作的詳細資訊，請參閱 [設定提交動作](../../forms/using/configuring-submit-actions.md).

此外， [!DNL Adobe Sign] 只有在所有簽署者簽署表單後，才會提交已啟用的最適化表單。 您可以在表單入口網站的「待簽署」區段中找到部分簽署的表單。 [!DNL Adobe Sign] 配置服務保持輪詢 [!DNL Adobe Sign] 伺服器 [規則間隔](../../forms/using/adobe-sign-integration-adaptive-forms.md) 驗證簽名狀態。 如果所有簽署者都完成表單的簽署，則會啟動提交動作服務並提交表單。 如果您使用自訂提交動作，且表單使用 [!DNL Adobe Sign]，請更新您的自訂提交動作，以使用提交動作服務。

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

您的表單簽署體驗已就緒。 您可以預覽表單以驗證簽署體驗。 在已發佈的表格上， [!DNL Adobe Sign] 簽署者收到透過電子郵件簽署的表單時，會顯示區塊欄位。 此體驗也稱為表單外簽署體驗。 您也可以為第一個簽署者設定表單內簽署體驗，詳細步驟請參閱 [建立表單內簽署體驗](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

## 為最適化表單配置雲端簽名 {#configure-cloud-signatures-for-an-adaptive-form}

雲端數位簽名或遠程簽名是新一代的數位簽名，可跨案頭、移動和網路運行，並滿足簽名者驗證的最高級合規性和保證。 您可以使用雲端數位簽名來簽署最適化表單。

之後 [編輯Adobe符號的最適化表單屬性](../../forms/using/working-with-adobe-sign.md#enableadobesign)，請執行下列步驟，將雲端簽名欄位新增至最適化表單：

1. 拖放 **[!UICONTROL Adobe Sign區塊]** 元件從元件瀏覽器移至最適化表單。 此 [!UICONTROL Adobe Sign區塊] 元件包含所有支援的 [!DNL Adobe Sign] 欄位。 依預設，會新增 **[!UICONTROL 簽名]** 欄位至最適化表單。

   ![符號區塊](assets/sign-block-new.png)

1. 選取 **[!UICONTROL Adobe Sign區塊]** 元件並點選 **編輯** ![aem_6_3_edit](assets/aem_6_3_edit.png) 表徵圖。 它顯示添加欄位和格式欄位外觀的選項。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **答：** 選取並新增 [!DNL Adobe Sign] 欄位。 **B.** 展開 [!DNL Adobe Sign] 封鎖至全螢幕檢視

1. 點選 **[!UICONTROL Adobe Sign欄位]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) 表徵圖。 它會顯示選取和新增的選項 [!DNL Adobe Sign] 欄位。

   展開 **[!UICONTROL 類型]** 要選擇的下拉欄位 **[!UICONTROL 數位簽名]** 然後點選 **完成** 表徵圖，將所選欄位添加到 [!DNL Adobe Sign] 封鎖。

   ![數位簽名](assets/digital_signatures_new.png)

   必須為欄位提供唯一名稱。

   使用下列方式將數位簽名套用至最適化表單：

   * 雲簽名：使用 [數位識別碼](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 由信任服務提供商托管。
   * Adobe Acrobat或Reader:下載並開啟包含Adobe Acrobat或Reader的檔案，以使用智慧卡、USB令牌或基於檔案的數字ID進行簽名。

   將雲端簽名欄位新增至最適化表單後，請執行下列步驟以完成設定程式：

   * [啟用Adobe Sign以建立最適化表單](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [為最適化表單選取Adobe Sign Cloud Service](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [將Adobe Sign簽署者新增至最適化表單](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [為最適化表單選取「提交動作」](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## 建立表單內簽署體驗 {#create-in-form-signing-experience}

使用者也可以在填寫表單時簽署最適化表單。 此體驗也稱為表單內簽署體驗。 表單內簽署體驗僅適用於多個簽署者環境中的第一位歌手。 執行下列步驟，為最適化表單建立表單內簽署體驗：

1. [添加和配置簽名步驟元件](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. [新增摘要步驟元件](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component).

![表單內簽署體驗](assets/in_form_signing_experience_new.png)

### 添加和配置簽名步驟元件 {#add-and-configure-the-signature-step-component}

使用「簽名步驟」元件提供一個區域，以電子方式對填寫的表單進行簽名。 呈現包含簽名步驟元件的部分時，它顯示可簽名的填充表單的PDF版本。 簽名步驟元件佔用表單可用的全寬。 建議在包含簽名步驟元件的區段上不要有任何其他元件。

執行以下步驟配置簽名步驟元件：

1. 拖放 **[!UICONTROL 簽名步驟]** 元件（從元件瀏覽器到表單）。
1. 選取新新增的簽章步驟元件，然後點選 **設定** ![設定](assets/configure.png) 表徵圖。 它會開啟屬性瀏覽器並顯示簽名步驟屬性。 設定下列屬性：

   * **[!UICONTROL 名稱]**:指定元件的名稱。

   * **[!UICONTROL 標題]:** 指定元件的唯一標題。
   * **[!UICONTROL 範本訊息]:** 指定在載入簽名PDF時要顯示的消息。 [!DNL Adobe Sign] 服務需要一些時間來準備和載入簽名PDF。
   * **[!UICONTROL 簽名服務]:** 選取 **[!DNL Adobe Sign]** 選項。

   * **[!UICONTROL 使用舊版電子簽名元件]**:如果您在 [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), AEM [!DNL Forms] 或基礎適用性表單具有舊版電子簽名元件，請選取 **使用舊版電子簽名元件** 選項。

   * **[!UICONTROL 設定]**:選取設定([!DNL Adobe Sign] Cloud Service)。 下拉式方塊僅在 **使用舊版電子簽名元件** 選項。

   * **[!UICONTROL CSS類]**:指定元件的CSS類別。

   點選完成 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 圖示以儲存變更。

   ![簽名步驟](assets/signature_step_new.png)

   >[!NOTE]
   >
   > * 拖放 **[!UICONTROL 簽名步驟]** 元件， **[!UICONTROL 簽署者和填寫表單的人是否相同？]** 選項自動設為 **是**. 必須讓表單持續運作。
   >
   > * 使用簽章步驟元件後的摘要步驟元件以獲得最佳體驗。 在您完成在簽名步驟元件中籤名表單後，「摘要」步驟會自動立即提交表單。 若您未使用摘要步驟，系統只會在使用 [Adobe Sign設定服務](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).
      > 以下是幾項最佳實務：
   > * 包含「簽名」步驟的適用性表單面板一律位於適用性表單的最後一個或第二個最後一個面板。 只有在最後一個面板包含「摘要」步驟時，才能是第二個面板。
   > * 包含「簽名」或「摘要」步驟元件的面板不能包含任何其他元件。
   > * 包含簽名步驟的適用性表單不能有提交按鈕。
   > * 包含簽名步驟的適用性表單的提交是透過背景服務或摘要步驟處理。 如果有一個已配置的簽名者也在填寫表單，則使用「摘要」步驟處理最適化表單提交的好處是，它會立即評估簽名者已簽名表單並調用提交操作。 背景服務需要更多時間來評估所有已設定的簽署者是否已簽署表單，並延遲提交最適化表單。
   > * 設計表單，使用者無法從包含「簽名」或「摘要」步驟的面板導覽回。



### 設定感謝頁面或摘要步驟元件 {#configure-the-thank-you-page-or-summary-step-component}

此 **摘要步驟** 元件會自動提交表單、填入自訂「摘要」頁面中的資訊，並顯示已提交表單的摘要。 它也會在傳回地圖中取得所需資訊。 摘要步驟元件會取用表單可用的全寬度。 建議在包含摘要步驟元件的區段上不要有任何其他元件。

現在，表單中的簽署體驗已就緒。 您可以預覽表單以驗證簽署體驗。

## 常見問題 {#frequently-asked-questions}

**問：** 您可以將適用性表單嵌入另一個適用性表單。 內嵌的最適化表單是否 [!DNL Adobe Sign] 已啟用？
**答：** 否，AEM [!DNL Forms] 不支援使用內嵌 [!DNL Adobe Sign] 已啟用最適化表單以簽署

**問：** 當我使用進階範本建立最適化表單並將其開啟以進行編輯時，會出現「電子簽名或簽署者未正確設定」錯誤訊息。 框。 如何解決錯誤訊息？
**答：** 使用進階範本建立的最適化表單已設定為使用 [!DNL Adobe Sign]. 若要解決錯誤，請建立並選取 [!DNL Adobe Sign] 雲端設定和設定 [!DNL Adobe Sign] 最適化表單的簽署者。

**問：** 我可以使用 [!DNL Adobe Sign] 最適化表單的靜態文字元件中的文字標籤？
**答：** 是，您可以在文字元件中使用文字標籤來新增 [!DNL Adobe Sign] 欄位 [記錄檔案](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) （僅限自動生成記錄文檔選項）啟用的最適化表單。 若要了解建立文字標籤的程式和規則，請參閱 [Adobe Sign檔案](https://helpx.adobe.com/sign/using/text-tag.html). 另請注意，適用性表單對文字標籤的支援有限。 您可以使用文字標籤來僅建立那些 [Adobe Sign區塊](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) 支援。

**問：** AEM [!DNL Forms] 兩者 [!UICONTROL Adobe Sign區塊] 和簽名步驟元件。 可在最適化表單中同時使用嗎？
**答：** 您可以在表單中同時使用這兩個元件。 以下是使用這些元件的幾項建議：

**Adobe Sign區塊：** 您可以使用 [!UICONTROL Adobe Sign區塊] 新增 [!UICONTROL Adobe Sign] 適用性表單上任何位置的欄位。 也會有助於為簽署者指派特定欄位。 預覽或發佈最適化表單時 [!UICONTROL Adobe Sign] 預設情況下，區塊不可見。 這些區塊僅在簽署檔案中啟用。 在簽名文檔中，僅啟用分配給簽名者的欄位。 [!UICONTROL Adobe Sign] 區塊可與第一個和後續簽署者搭配使用。

**簽名步驟元件：** 您可以使用簽名步驟元件來建立表單內簽名體驗。 填入表單時，僅允許第一個簽署者簽署。 呈現包含簽名步驟元件的部分時，它顯示表單的可簽名PDF版本。 通常是表單的最後一個或倒數第二個區段，後面接著摘要元件。

## 疑難排解 {#troubleshoot}

### [!DNL Adobe Sign] 協定失敗 {#adobe-sign-agreement-failures}

**問題**
當 [!DNL Adobe Sign] 為適用性表單配置服務，服務將無法建立 [!DNL Adobe Sign] 基礎適用性表單的合約。

**解析度**

* 檢查 [Adobe Sign雲端服務設定](../../forms/using/adobe-sign-integration-adaptive-forms.md) 用於最適化表單。
* 確認API應用程式位於 [!DNL Adobe Sign] 用於配置的伺服器 [!DNL Adobe Sign] 雲端服務具有必要的權限。
* 如果您使用多個 [!DNL Adobe Sign] 雲端服務，指向 **[!UICONTROL oAuth URL]** 所有服務都一樣 **[!UICONTROL Adobe Sign·沙德]**.

* 使用個別電子郵件地址進行設定 [!DNL Adobe Sign] 第一個簽名者和單一簽名者。 第一個簽署者或唯一簽署者（若是單一簽署者）的電子郵件地址不能與 [!DNL Adobe Sign] 用來設定AEM雲端服務的帳戶。

### AEM [!DNL Forms] 為 [!DNL Adobe Sign] 啟用適用性表單未開始 {#adobe-sign-aem-form-workflow-failures}

**問題**
當 [!DNL Adobe Sign] 針對適用性表單進行設定，則使用叫用來設定的工作流程 [!DNL Forms] 工作流程選項未啟動。

**解析度**

* 使用 [!DNL Adobe Sign] 若沒有「簽名」步驟或表單，則需要多人簽名，AEM [!DNL Forms] 伺服器會等待排程器確認所有人員已簽署表單。 排程器只會在所有人員完成簽署後提交最適化表單，而工作流程只會在成功提交最適化表單後開始。 您可以縮短 [排程器](adobe-sign-integration-adaptive-forms.md) 快速檢查表單簽名狀態並加快表單提交。


## 相關文章 {#related-articles}

* [整合Adobe Sign與AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [搭配最適化表單使用Adobe Sign的最佳作法](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [搭配使用Adobe Sign與AEM Forms（影片）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
