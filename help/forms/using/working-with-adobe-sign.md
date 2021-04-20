---
title: 以最適化形式使用Adobe Sign
seo-title: 以最適化形式使用Adobe Sign
description: 啟用電子簽名(Adobe Sign)工作流程，以自動化簽名工作流程、簡化單一和多重簽名程式，以及從行動裝置電子簽署表格。
seo-description: 啟用電子簽名(Adobe Sign)工作流程，以自動化簽名工作流程、簡化單一和多重簽名程式，以及從行動裝置電子簽署表格。
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
feature: Adaptive Forms, Adobe Sign
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '3863'
ht-degree: 0%

---


# 以最適化形式使用[!DNL Adobe Sign]{#using-adobe-sign-in-an-adaptive-form}

[!DNL Adobe Sign] 可針對最適化表單啟用電子簽名工作流程。電子簽名可改善處理法律、銷售、薪資、人力資源管理等領域檔案的工作流程。

在典型的[!DNL Adobe Sign]和最適化表單場景中，用戶填充自適應表單以申請服務。 例如，房貸和信用卡申請需要所有借款人和共同申請人的合法簽名。 若要針對類似案例啟用電子簽名工作流程，您可將[!DNL Adobe Sign]與AEM[!DNL Forms]整合。 還有一些示例，您可以使用[!DNL Adobe Sign]來：

* 透過完全自動化的提案、報價和合約流程，從任何裝置完成交易。
* 更快完成人力資源流程，為您的員工提供數位體驗。
* 縮短合約週期時間，並加快廠商上線速度。
* 建立可自動化一般程式的數位工作流程。

[!DNL Adobe Sign] 與支援整AEM合： [!DNL Forms] 

* 單一和多使用者簽署工作流程
* 循序和同步簽署工作流程
* 表單內和表單外簽署體驗
* 以匿名或登入使用者身分簽署表格
* 動態簽署程式(與AEM[!DNL Forms]工作流程整合)
* 透過知識庫、電話和社交個人檔案進行驗證

瞭解使用Adobe Sign與最適化表單](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)建立更佳簽署體驗的最佳範例。[

## 必備條件 {#prerequisites}

在最適化格式中使用[!DNL Adobe Sign]之前：

* 確AEM定[!DNL Forms]雲端服務已設定為使用[!DNL Adobe Sign]。 如需詳細資訊，請參閱[將Adobe Sign與AEM Forms整合。](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* 讓簽署者的清單準備好。 您至少需要每個簽署者的電子郵件地址。

## 為最適化表單{#configure-adobe-sign-for-an-adaptive-form}配置[!DNL Adobe Sign]

執行以下步驟，為自適應表單配置[!DNL Adobe Sign] :

1. [編輯Adobe符號的最適化表單屬性](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [將Adobe Sign欄位新增至最適化表單](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [啟用Adobe Sign的最適化表單](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [選擇Adobe SignCloud Service以適應形式](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [將Adobe Sign簽署者加入最適化表單](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [為最適化表單選擇提交動作](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![簽署者詳細資訊](assets/signer_details_new.png)

### 編輯[!DNL Adobe Sign] {#enableadobesign}的最適化表單屬性

為現有或新的自適應表單配置[!DNL Adobe Sign]的自適應表單屬性。

[建立Adobe的最適化表](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) 單說明建立基本最適化表單的步驟。有關建立自適應表單時可用的其它選項，請參見[建立自適應表單](../../forms/using/creating-adaptive-form.md)。

#### 為[!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}建立自適應表單

執行下列步驟以建立可簽署的最適化表單：

1. 導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。
1. 點選「**[!UICONTROL 建立]**」並選取「最適化表單」。 ****&#x200B;此時會顯示範本清單。 選擇模板並點選&#x200B;**[!UICONTROL Next]**。
1. 在&#x200B;**[!UICONTROL Basic]**&#x200B;標籤中：

   1. 指定最適化表單的&#x200B;**[!UICONTROL 名稱]**&#x200B;和&#x200B;**[!UICONTROL 標題]**。

   1. 選擇在配置[!DNL Adobe Sign]為[!DNL Forms]時建立的[配置容AEM器](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)。

      >[!NOTE]
      >
      >**[!UICONTROL Adobe SignCloud Service]**&#x200B;下拉式清單會顯示您在此欄位中選取之組態容器中設定的雲端服務。 當您選擇「啟用Adobe Sign」選項時，**[!UICONTROL Adobe SignCloud Service]**&#x200B;下拉清單可在自適應表單屬性的&#x200B;**[!UICONTROL 電子簽名]**&#x200B;部分中找到。****

1. 在&#x200B;**[!UICONTROL 表單模型]**&#x200B;標籤中，選擇以下選項之一：

   * 選擇&#x200B;**[!UICONTROL 將表單模板關聯為記錄文檔模板]**&#x200B;選項，然後選擇記錄文檔模板。 如果您使用以表單範本為基礎的最適化表單，則傳送以進行簽署的檔案只會顯示以關聯表單範本為基礎的欄位。 它不會顯示最適化表單的所有欄位。

   * 選擇&#x200B;**[!UICONTROL 生成記錄文檔]**&#x200B;選項。 如果您使用啟用「記錄檔案」選項的最適化表單，則傳送供簽署的檔案會顯示最適化表單的所有欄位。

1. 點選&#x200B;**[!UICONTROL 建立。]** 會建立可簽署的最適化表單，可用來新增欄 [!DNL Adobe Sign] 位。

#### 編輯[!DNL Adobe Sign] {#editafsign}的最適化表單

執行以下步驟，在現有的自適應格式中使用[!DNL Adobe Sign] :

1. 導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。
1. 選擇最適化表單，然後點選&#x200B;**[!UICONTROL 屬性]**。
1. 在&#x200B;**[!UICONTROL Basic]**&#x200B;標籤中，選擇在配置[!DNL Adobe Sign]為[!DNL Forms]時建立的[配置容器AEM](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)。
1. 在&#x200B;**[!UICONTROL 表單模型]**&#x200B;標籤中，選擇以下選項之一：

   * 選擇&#x200B;**[!UICONTROL 將表單模板關聯為記錄文檔模板]**&#x200B;選項，然後選擇記錄文檔模板。 如果您使用以表單範本為基礎的最適化表單，則傳送以進行簽署的檔案只會顯示以關聯表單範本為基礎的欄位。 它不會顯示最適化表單的所有欄位。

   * 選擇&#x200B;**[!UICONTROL 生成記錄文檔]**&#x200B;選項。 如果您使用啟用「記錄檔案」選項的最適化表單，則傳送供簽署的檔案會顯示最適化表單的所有欄位。

1. 點選&#x200B;**[!UICONTROL 儲存並關閉]**。 [!DNL Adobe Sign]已啟用最適化表單。

### 將Adobe Sign欄位添加到最適化表單{#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] 具有可放置在自適應表單上的各種欄位。這些欄位接受各種資料類型，例如簽名、縮寫簽名、公司或標題，並協助在簽署時收集額外資訊以及簽名。 您可以使用[!DNL Adobe Sign]塊元件將[!DNL Adobe Sign]欄位放置在自適應形式的不同位置。

執行以下步驟，將欄位添加到自適應表單中並自定義與這些欄位相關的各種選項：

1. 將&#x200B;**[!UICONTROL Adobe Sign塊]**&#x200B;元件從元件瀏覽器拖放到自適應表單。 [!DNL Adobe Sign]塊元件具有所有支援的[!DNL Adobe Sign]欄位。 預設情況下，它將&#x200B;**Signature**&#x200B;欄位添加到最適化表單中。

   ![簽署區塊](assets/sign_block_new.png)

   預設情況下，[!DNL Adobe Sign]塊在已發佈的最適化表單中不可見。 只有簽署檔案才會顯示。 可以從[!DNL Adobe Sign]塊元件的屬性中更改[!DNL Adobe Sign]塊的可見性。

   >[!NOTE]
   >
   >    * 使用[!DNL Adobe Sign]塊不是要求以自適應形式使用[!DNL Adobe Sign]的。 如果您不使用[!DNL Adobe Sign]區塊並新增簽署者的欄位，則會在簽署檔案底部顯示預設簽名欄位。
   >    * 僅針對自動產生記錄檔案的最適化表單使用[!DNL Adobe Sign]區塊。 如果您使用自訂XDP來產生記錄檔案或以表單範本為基礎的最適化表單，則不支援[!DNL Adobe Sign]區塊。


1. 選擇&#x200B;**[!UICONTROL Adobe Sign塊]**&#x200B;元件並按一下&#x200B;**編輯** ![ aem_6_3_edit](assets/aem_6_3_edit.png)表徵圖。 它顯示添加欄位和欄位格式外觀的選項。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.選** 擇並添加字 [!DNL Adobe Sign] 段。**B.將** 區塊展 [!DNL Adobe Sign] 開為全螢幕檢視

1. 點選「**[!UICONTROL Adobe Sign]欄位** ![ aem_6_3_adobesign](assets/aem_6_3_adobesign.png)」圖示。 它顯示選擇和添加[!DNL Adobe Sign]欄位的選項。

   展開&#x200B;**[!UICONTROL Type]**&#x200B;下拉式欄位以選取[!DNL Adobe Sign]欄位，並點選「完成![ aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」圖示，將選取的欄位新增至[!DNL Adobe Sign]區塊。 **[!UICONTROL Type]**&#x200B;下拉式欄位包含「簽名」、「簽署者資訊」和「資料」欄位類型。 [!DNL Adobe Sign] 與「AEMType」下拉式方塊中列 [!DNL Forms]   出的支援欄位整合。有關[!DNL Adobe Sign]欄位的詳細資訊，請參閱[Adobe Sign文檔](https://helpx.adobe.com/sign/help/field-types.html)。

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   必須為欄位提供唯一名稱。 您也可以選取必要選項，將欄位標示為必填欄位。 除了&#x200B;**[!UICONTROL Name]**&#x200B;和&#x200B;**[!UICONTROL Required]**&#x200B;選項外，有些[!DNL Adobe Sign]欄位還有更多選項。 例如，遮色片和多行。 此外，請為每個[!DNL Adobe Sign]欄位指定唯一名稱，不論欄位位於相同或不同的[!DNL Adobe Sign]區塊。

   如果您從下拉式清單中選取「數位簽章」****，則可將數位簽章套用至最適化表單：

   * 使用雲端簽名線上簽署，並使用信任服務提供者代管的[數位ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html)。
   * 使用智慧卡、USB Token或檔案式數位ID，以Adobe Acrobat或Reader下載檔案至本機。

### 為最適化表單{#enableadobsignforanadaptiveform}啟用[!DNL Adobe Sign]

現成可用的[!DNL Adobe Sign]不會為最適化表單啟用。 執行下列步驟以啟用它：

1. 在「內容」瀏覽器中，點選「表單容器」**[!UICONTROL ，然後點選「設定****![設定](assets/configure.png)」圖示。]**&#x200B;它會開啟屬性瀏覽器並顯示最適化表單容器屬性。
1. 在屬性瀏覽器中，展開&#x200B;**[!UICONTROL 電子簽名]** accordion，然後選擇&#x200B;**[!UICONTROL 啟用Adobe Sign]**&#x200B;選項。 它為自適應表單啟用[!DNL Adobe Sign]。

### 選擇[!DNL Adobe Sign]Cloud Service和簽署順序{#selectadobesigncloudserviceforanadaptiveform}

您可以為[!DNL Forms]實例配置多個AEM[!DNL Adobe Sign]服務。 建議為每個職能（人力資源、財務等）分別提供一套服務。 它讓追蹤和報告已簽署的檔案變得更輕鬆。 例如，銀行有多個部門。 您可以為每個部門分別設定一個設定，以便更好地追蹤檔案。

檔案也可以有多個簽署者。 例如，信用卡申請可以有多個申請人。 銀行在開始處理申請之前要求所有申請人的簽名。 對於多重簽署者案例，您可以選擇依循序或同時順序簽署檔案。

執行下列步驟以選擇雲端服務和簽署順序：

![雲端服務](assets/cloud-service.png)

1. 在「內容」瀏覽器中，點選「表單容器」**[!UICONTROL ，然後點選「設定****![設定](assets/configure.png)」圖示。]**&#x200B;它會開啟屬性瀏覽器並顯示最適化表單容器屬性。
1. 在屬性瀏覽器中，展開&#x200B;**[!UICONTROL 電子簽名]** accordion，然後選擇&#x200B;**[!UICONTROL 啟用Adobe Sign]**&#x200B;選項。 它為自適應表單啟用[!DNL Adobe Sign]。
1. 從已配置的[!DNL Adobe Sign]Cloud Services清單中選擇雲服務。

   如果&#x200B;**[!UICONTROL Adobe SignCloud Service]**&#x200B;清單為空，請遵循[使用AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)配置Adobe Sign文章配置服務。

   此下拉式清單列出「工具> **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**」中`global`資料夾中存在的雲端服務。 此外，下拉式清單也會列出您在建立最適化表單時，在&#x200B;**[!UICONTROL 設定容器]**&#x200B;欄位中選取之資料夾中存在的雲端服務。

1. 從&#x200B;**[!UICONTROL 「簽署者可以簽署]**」對話方塊中選取簽署順序。 [!DNL Adobe Sign] 歌手可依序簽署 **[!UICONTROL 最適化表]** 單——依序簽署另一個簽署者，或 **[!UICONTROL 同時]** -依任何順序簽署。

   依循序序列，一次會有一個簽署者收到要簽署的表格。 簽署者完成簽署檔案後，表格會傳送給下一個簽署者，依此類推。

   同時，多位簽署者一次可以簽署表格。

1. [將簽署者新增至最適](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) 化格式，並點選「 ![Done_6_3_forms_](assets/aem_6_3_forms_save.png) save」圖示以儲存變更。


### 將簽署者新增至最適化表單{#addsignerstoanadaptiveform}

最適化表單只能有一位或多位簽署者。 當您新增簽署者時，您也可以設定簽署者的驗證詳細資訊。 您也可以選取填表人和歌手是否是同一個人。 執行下列步驟以新增及提供簽署者的各種詳細資訊：

1. 在「內容」瀏覽器中，點選「表單容器」**[!UICONTROL ，然後點選「設定****![設定](assets/configure.png)」圖示。]**&#x200B;它會開啟具有最適化表單容器屬性的屬性瀏覽器。
1. 在屬性瀏覽器中，展開&#x200B;**[!UICONTROL 電子簽名]** accordion，然後選擇&#x200B;**[!UICONTROL 啟用Adobe Sign]**&#x200B;選項。 它為自適應表單啟用[!DNL Adobe Sign]。
1. 點選「**[!UICONTROL 簽署者設定]**」下方的「新增簽署者&#x200B;]**」。**[!UICONTROL &#x200B;它會將簽署者新增至最適化表單。 您可以新增多個[!DNL Adobe Sign]簽署者至最適化表單。
   ![電話詳細資訊](assets/phone-details.png)

1. 按一下&#x200B;**Edit** ![ aem_6_3_edit](assets/aem_6_3_edit.png)圖示，以指定與簽署者相關的下列資訊：

   * **[!UICONTROL 標題]:** 指定標題以唯一識別簽署者。

   * **[!UICONTROL 簽署者和人員在填寫相同的表單嗎？]:** 如果表 ****&#x200B;單填寫者和第一個簽署者是同一人，請選取「是」。如果選項設定為&#x200B;**No，則**&#x200B;請勿在最適化表單中使用簽名步驟元件。 如果表單包含「簽名步驟」元件，則欄位會自動設為「是」。

   * **[!UICONTROL 簽署者電子郵件地址]：指** 定簽署者的電子郵件地址。簽署者會收到指定電子郵件地址上的已簽署檔案／表格。 您可以選擇使用表單欄位、登入使用者的使用AEM者設定檔中提供的電子郵件地址，或手動輸入電子郵件地址。 這是必要的步驟。 請確定第一個簽署者或唯一簽署者（如果是單一簽署者）的電子郵件地址與用於設定AEM雲端服務的[!DNL Adobe Sign]帳戶不相同。

   * **[!UICONTROL 簽署者驗證方法]:** 指定在開啟表單進行簽署之前，先驗證使用者的方法。您可以選擇電話、知識庫和社交身分驗證。
   >[!NOTE]
   >
   >    * 依預設，社交身分驗證提供使用Facebook、Google和LinkedIn進行驗證的選項。 您可以聯絡[!DNL Adobe Sign]支援以啟用其他社交驗證提供者。


   * **[!DNL Adobe Sign]填寫或簽署的欄位：** 選 [!DNL Adobe Sign] 取簽署者的欄位。最適化表單可包含多個[!DNL Adobe Sign]欄位。 您可以選擇為簽署者啟用特定欄位。 該欄位顯示所有可用的[!DNL Adobe Sign]塊。 選擇塊時，將選擇塊的所有欄位。 您可以使用X圖示來取消選取欄位。

   ![簽署者——詳細資訊](assets/signer-details.png)

   上面的影像有兩個示例[!DNL Adobe Sign]塊：個人資訊和辦公室詳細資訊

   點選「完成![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」圖示。 簽章者已新增並設定。

### 選擇最適化表單{#selectsubmitactionforanadaptiveform}的提交操作

在您新增[!DNL Adobe Sign]欄位至最適化表單、從表單容器啟用[!DNL Adobe Sign]、選取[!DNL Adobe Sign]Cloud Service，並新增[!DNL Adobe Sign]簽署者，為最適化表單選擇適當的提交動作。 有關自適應表單提交操作的詳細資訊，請參閱[配置提交操作](../../forms/using/configuring-submit-actions.md)。

此外，[!DNL Adobe Sign]啟用的最適化表單只有在所有簽署者簽署表單後才會送出。 您可以在表單入口網站的「待簽」區段中找到部分簽署的表單。 [!DNL Adobe Sign] Configuration Service會定期將 [!DNL Adobe Sign] 輪詢服 [務器](../../forms/using/adobe-sign-integration-adaptive-forms.md) 保留為驗證簽名狀態。如果所有簽署者都完成表單簽署，則會啟動提交動作服務並提交表單。 如果您使用自訂提交動作，而表單使用[!DNL Adobe Sign]，請更新自訂提交動作以使用提交動作服務。

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

您的表單簽署體驗已就緒。 您可以預覽表單以驗證簽署體驗。 在發佈的表格上，當簽署者收到透過電子郵件進行簽署的表格時，會顯示[!DNL Adobe Sign] 「封鎖」欄位。 這種體驗也稱為表單外簽署體驗。 您也可以為第一個簽署者設定表單內簽署體驗，如需詳細步驟，請參閱[建立表單內簽署體驗](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience)。

## 為最適化表單{#configure-cloud-signatures-for-an-adaptive-form}設定雲端簽名

雲端數位簽名或遠端簽名是新一代的數位簽名，可跨桌上型電腦、行動裝置和網路運作。 並符合簽署者驗證的最高等級合規性與保證。 您可以使用雲端數位簽名來簽署調適性表格。

在[編輯Adobe符號的最適化表單屬性](../../forms/using/working-with-adobe-sign.md#enableadobesign)後，請執行下列步驟，將雲端簽名欄位新增至最適化表單：

1. 將&#x200B;**[!UICONTROL Adobe Sign塊]**&#x200B;元件從元件瀏覽器拖放到自適應表單。 [!UICONTROL Adobe Sign塊]元件具有所有支援的[!DNL Adobe Sign]欄位。 預設情況下，它將&#x200B;**[!UICONTROL Signature]**&#x200B;欄位添加到最適化表單中。

   ![簽署區塊](assets/sign-block-new.png)

1. 選擇&#x200B;**[!UICONTROL Adobe Sign塊]**&#x200B;元件並按一下&#x200B;**編輯** ![ aem_6_3_edit](assets/aem_6_3_edit.png)表徵圖。 它顯示添加欄位和欄位格式外觀的選項。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.選** 擇並添加字 [!DNL Adobe Sign] 段。**B.將** 區塊展 [!DNL Adobe Sign] 開為全螢幕檢視

1. 點選「**[!UICONTROL Adobe Sign欄位]** ![ aem_6_3_adobesign](assets/aem_6_3_adobesign.png)」圖示。 它顯示選擇和添加[!DNL Adobe Sign]欄位的選項。

   展開&#x200B;**[!UICONTROL Type]**&#x200B;下拉式欄位以選擇&#x200B;**[!UICONTROL 數位簽章]**&#x200B;並點選&#x200B;**Done**&#x200B;圖示，將選取的欄位新增至[!DNL Adobe Sign]區塊。

   ![數位簽名](assets/digital_signatures_new.png)

   必須為欄位提供唯一名稱。

   使用下列功能，將數位簽名套用至最適化表單：

   * 雲端簽名：使用信任服務提供者托管的[數位ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html)進行簽署。
   * Adobe Acrobat或Reader:下載並開啟含Adobe Acrobat或Reader的檔案，以使用智慧卡、USB Token或以檔案為基礎的數位ID進行簽署。

   將雲端簽名欄位新增至最適化表單後，請執行下列步驟以完成設定程式：

   * [啟用Adobe Sign的最適化表單](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [選擇Adobe SignCloud Service以適應形式](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [將Adobe Sign簽署者加入最適化表單](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [為最適化表單選擇提交動作](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## 建立表單內簽署體驗{#create-in-form-signing-experience}

使用者也可以在填寫表單時簽署最適化表單。 此體驗也稱為表單簽署體驗。 表單簽署體驗僅適用於多重簽署者環境中的第一位歌手。 執行下列步驟，為最適化表單建立表單內簽署體驗：

1. [新增及設定「簽名步驟」元件](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)。
1. [添加摘要步驟元件](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component)。

![表單簽署體驗](assets/in_form_signing_experience_new.png)

### 添加和配置「簽名步驟」元件{#add-and-configure-the-signature-step-component}

使用「簽名步驟」元件提供電子簽署填寫表單的區域。 當轉譯包含「簽名步驟」元件的區段時，會顯示可簽名的PDF版本填寫表單。 「簽名步驟」元件會佔用表單的全寬。 建議在包含「簽名步驟」元件的部分上不使用任何其他元件。

執行以下步驟以配置「簽名步驟」元件：

1. 將&#x200B;**[!UICONTROL 簽名步驟]**&#x200B;元件從元件瀏覽器拖放到表單中。
1. 選擇新添加的「簽名」步驟元件，並點選「配置&#x200B;**** ![配置](assets/configure.png)」表徵圖。 它會開啟屬性瀏覽器並顯示「簽名」步驟屬性。 設定下列屬性：

   * **[!UICONTROL 名稱]**:指定元件的名稱。

   * **[!UICONTROL Title]:** 指定元件的唯一標題。
   * **[!UICONTROL 範本訊息]:** 指定在載入簽名PDF時要顯示的訊息。[!DNL Adobe Sign] 服務需要一些時間來準備和載入簽名PDF。
   * **[!UICONTROL 簽署服務]:** 選取 **[!DNL Adobe Sign]** 選項。

   * **[!UICONTROL 使用舊版電子簽名元件]**:如果您在 [AEM Forms工作區、應用AEM程式中使用個別的最適化表單，或是基礎的最適化表單有舊版電子簽名元件，請選取「](../../forms/using/introduction-html-workspace.md)使用舊版電子簽名元 [!DNL Forms]  **** 件」。

   * **[!UICONTROL 配置]**:選擇配置([!DNL Adobe Sign] Cloud Service)。只有啟用了&#x200B;**使用舊版電子簽名元件**&#x200B;選項時，下拉框才可用。

   * **[!UICONTROL CSS類別]**:指定元件的CSS類別。

   點選「完成![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」圖示以儲存變更。

   ![簽名步驟](assets/signature_step_new.png)

   >[!NOTE]
   >
   > * 當您將&#x200B;**[!UICONTROL 簽名步驟]**&#x200B;元件拖放至表單時，**[!UICONTROL 簽署者與填寫表單的人員是否相同？]** 選項自動設定為「 **是」**。必須讓表單繼續運作。
      >
      > 
   * 在「簽名步驟」元件後使用「摘要步驟」元件，以獲得最佳體驗。 在您完成簽名步驟元件中的表單簽署後，「摘要」步驟會自動並立即提交表單。 如果不使用摘要步驟，則只有在使用[Adobe Sign配置服務](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status)設定間隔後才觸發自動提交。
      > 以下是一些最佳實務：
   > * 包含簽名步驟的最適化表單面板永遠位於最適化表單的最後一個或第二個最後一個面板。 只有在最後一個面板包含「摘要」步驟時，它才能是第二個最後一個面板。
   > * 包含「簽名」或「摘要」步驟元件的面板不能包含任何其他元件。
   > * 包含「簽名步驟」的最適化表單不能有「提交」按鈕。
   > * 包含簽名步驟的最適化表單的提交是透過背景服務或摘要步驟處理。 如果有一個已設定的簽署者也在填寫表單，則使用「摘要」步驟處理最適化表單提交的優點是，它會立即評估簽署者已簽署表單並叫用提交動作。 背景服務需要更多時間來評估所有已設定的簽署者是否已簽署表單，並延遲提交最適化表單。
   > * 設計表單，讓使用者不能從包含「簽名」或「摘要」步驟的面板導覽回來。



### 設定感謝頁面或摘要步驟元件{#configure-the-thank-you-page-or-summary-step-component}

**摘要步驟**&#x200B;元件會自動提交表單，在自定義的「摘要」頁中填入資訊，並顯示提交表單的摘要。 它也會在回訪地圖中取得所需資訊。 「摘要步驟」元件佔用表單的全寬。 建議在包含「摘要步驟」元件的部分上不使用任何其他元件。

現在，表單簽署體驗已就緒。 您可以預覽表單以驗證簽署體驗。

## 常見問題 {#frequently-asked-questions}

**問：您可** 以將最適化表單嵌入另一個最適化表單。嵌入式自適應表單是否可啟用？
[!DNL Adobe Sign]**Ans:** 否AEM，不 [!DNL Forms] 支援使用可內嵌可調式表單以進行 [!DNL Adobe Sign] 簽署的可調式表單

**問：當** 我使用進階範本建立最適化表單並開啟它進行編輯時，會出現錯誤訊息「電子簽名或簽署者未正確設定」。的雙曲餘切值。 如何解決錯誤訊息？
**Ans：使用** 進階範本建立的最適化表單已設定為使用 [!DNL Adobe Sign]。若要解決錯誤，請建立並選取[!DNL Adobe Sign]雲端組態，並為最適化表單設定[!DNL Adobe Sign]簽署者。

**問：我** 可以在最適 [!DNL Adobe Sign] 化表單的靜態文字元件中使用文字標籤嗎？**Ans:** 是的，您可以在文字元件中使用文字標籤，將欄 [!DNL Adobe Sign] 位新增至 [Document of Record](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) （僅限自動產生的記錄檔案選項）啟用的最適化表單。要瞭解建立文本標籤的過程和規則，請參閱[Adobe Sign文檔](https://helpx.adobe.com/sign/using/text-tag.html)。 另請注意，最適化表單對文字標籤的支援有限。 您只能使用文字標籤來建立[Adobe Sign區塊](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form)支援的欄位。

**問：提** 供 [!DNL Forms] 了 [!UICONTROL Adobe Sign] 區塊和簽名步驟元件。這些功能是否可同時以最適化形式使用？
**Ans:** 您可以在表單中同時使用這兩個元件。以下是使用這些元件的一些建議：

**Adobe Sign塊：** 您可以使用 [!UICONTROL Adobe Sign] 塊，在最適化表 [!UICONTROL 單的任] 意位置添加Adobe信號欄位。此外，也有助於為簽署者指派特定欄位。 預覽最適化表單或發佈[!UICONTROL Adobe Sign]區塊時，預設不會顯示。 這些區塊僅在簽署檔案中啟用。 在簽署檔案中，只會啟用指派給簽署者的欄位。 [!UICONTROL Adobe] 簽署區塊可與第一個和後續簽署者搭配使用。

**簽章步驟元件：** 您可以使用簽章步驟元件來建立表單簽署體驗。它只允許第一個簽署者在填寫表單時簽名。 當轉譯包含「簽名步驟」元件的區段時，會顯示可簽名的表單PDF版本。 通常是表單的最後一個或倒數第二個部分，後面接著是摘要元件。

## 疑難排解 {#troubleshoot}

### [!DNL Adobe Sign] 協定失效  {#adobe-sign-agreement-failures}

**問**
題當 [!DNL Adobe Sign] 為自適應表單配置服務時，服務無法為基礎自適應 [!DNL Adobe Sign] 表單建立協定。

**解析度**

* 檢查最適化表單中使用的Adobe Sign雲服務[組態。](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* 請確定用於設定[!DNL Adobe Sign]雲端服務之[!DNL Adobe Sign]伺服器上的API應用程式具有必要的權限。
* 如果您使用多個[!DNL Adobe Sign]雲端服務，請將所有服務的&#x200B;**[!UICONTROL oAuth URL]**&#x200B;指向相同的&#x200B;**[!UICONTROL Adobe Sign·沙德]**。

* 請使用個別的電子郵件地址來設定[!DNL Adobe Sign]帳戶，以及第一個簽署者和單一簽署者的帳戶。 第一個簽署者或唯一簽署者（如果是單一簽署者）的電子郵件地址不能與用於設定AEM雲端服務的[!DNL Adobe Sign]帳戶相同。

### 為[!DNL Adobe Sign]啟用的AEM適應性表單配置的[!DNL Forms]工作流不會啟動{#adobe-sign-aem-form-workflow-failures}

**問**
題為 [!DNL Adobe Sign] 最適化表單設定時，使用「叫用工作流程」選項設定的 [!DNL Forms] 工作流程不會啟動。

**解析度**

* 當您使用[!DNL Adobe Sign]而不使用「簽名」步驟或表格需要多人簽名時，AEM [!DNL Forms]伺服器會等待排程器確認所有人已簽署表格。 調度器只有在所有人完成簽名後才提交自適應表單，而工作流只在成功提交自適應表單後才啟動。 您可以縮短[排程器](adobe-sign-integration-adaptive-forms.md)的間隔，以快速間隔檢查表單簽署狀態並加速表單提交。


## 相關文章{#related-articles}

* [將Adobe Sign與AEM Forms整合](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [使用具有最適化表單的Adobe Sign的最佳範例](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [使用Adobe Sign與AEM Forms（影片）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
