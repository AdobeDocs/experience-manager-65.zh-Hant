---
title: 設定 [!DNL Workfront for Experience Manager enhanced connector]
description: 設定 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2660de7c-0281-4884-98d9-e78f20cf571c
hide: true
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1723'
ht-degree: 1%

---

# 設定 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-configure.html?lang=en) |
| AEM 6.5 | 本文章 |

在中具有管理員存取許可權的使用者 [!DNL Adobe Experience Manager] 在安裝增強型聯結器後進行設定。 如需安裝指示，請參閱 [安裝聯結器](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
>* Adobe需要部署和設定 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅透過認證合作夥伴或 [!DNL Adobe Professional Services]. 如果部署與設定沒有認證合作夥伴或 [!DNL Adobe Professional Services]，Adobe不支援。
>
>* Adobe可能會將更新發行至 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 讓此聯結器成為多餘的；如果發生這種情況，客戶可能需要從使用此聯結器進行轉換。
>
>* Adobe支援增強型聯結器1.7.4版及更新版本。 不支援舊版發行前版本和自訂版本。 若要檢查增強型聯結器版本，請導覽至 `digital.hoodoo` 群組可在左側窗格取得，位置為 [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant).
>
>* 另請參閱 [適用於Experience Manager Assets增強型聯結器的Workfront合作夥伴認證考試](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 有關考試的資訊，請參閱 [考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## 設定事件訂閱 {#event-subscriptions}

事件訂閱是用來通知AEM中發生的事件 [!DNL Adobe Workfront]. 共有三種 [!DNL Workfront for Experience Manager enhanced connector] 需要事件訂閱才能運作的功能，包括：

* 自動建立專案連結資料夾。
* 同步Workfront檔案自訂表單值與AEM資產中繼資料的變更。
* 專案完成時將資產自動發佈到Brand Portal。

若要使用這些功能，請啟用事件訂閱。

* 編輯 [!UICONTROL Workfront工具] 您在步驟5建立的Cloud Service設定，並選取 [!UICONTROL 活動訂閱] 標籤。
* 選取 [!UICONTROL Workfront自訂整合] 您已在第6節中建立。
* 按一下 [!UICONTROL 啟用Workfront事件訂閱].

  ![活動訂閱](/help/assets/assets/event-subs.png)

## 設定連結的資料夾 {#linked-folders}

若要訂閱事件，請遵循下列步驟：

1. 導覽至 **[!UICONTROL 活動訂閱]** 索引標籤來識別。
1. 選取在中建立的自訂整合 [!DNL Workfront].
1. 按一下 **[!UICONTROL 啟用Workfront事件訂閱]**.

### 連結的資料夾結構設定 {#linked-folder-structure}

1. 前往雲端服務中的專案連結資料夾索引標籤。
1. 連結資料夾父路徑：在DAM中選取您想要建立連結資料夾的資料夾。 如果留空，其將預設為/content/dam。 請確定Workfront工具中繼資料結構和Workfront連結資料夾中繼資料結構已套用至選取的資料夾。
1. 連結的資料夾結構：輸入逗號分隔值。 每個值都應 `DE:<some-project-custom-form-field>`、Portfolio、方案、年份、名稱或某些「常值字串值」（最後一項帶有引號）。 目前設為Portfolio、方案、年、DE：專案型別、名稱。
1. 如果Workfront中的資料夾標題應包含結構中的所有資料夾，則應核取使用資料夾結構名稱在Workfront中建立連結資料夾標題。 否則，這是最後一個資料夾的標題。
1. 子資料夾多欄位可讓您指定應建立為連結資料夾的子資料夾的資料夾清單。
1. 專案狀態：選取專案狀態以建立連結的資料夾。
1. 在具有投資組合的專案中建立連結資料夾：專案必須屬於其中建立連結資料夾的Portfolio清單。 將此清單保留為空白可為所有專案組合建立連結資料夾。
1. 使用自訂表單欄位在專案中建立連結資料夾：自訂表單欄位及其對應的值，專案必須建立連結資料夾。 如果留為空白，則會忽略此設定。 選取 `CUSTOM FORMS: Create DAM Linked Folder` 欄位和輸入 `Yes` ，以取得值。
1. 按一下啟用自動建立連結資料夾。 如果您返回「事件訂閱」標籤，現在會看到有一個建立事件。

![連結的資料夾組態](/help/assets/assets/wf-linked-folder-config.png)

## 中繼資料結構描述對應 {#metadata-schema-mapping}

### 設定資料夾中繼資料對應 {#folder-metadata-mapping}

Workfront專案與AEM資料夾之間的中繼資料對應是在AEM資料夾中繼資料結構中定義。 應照常在AEM中建立和設定資料夾中繼資料結構。 Workfront工具會將自動完成下拉式清單新增至每個資料夾中繼資料結構表單欄位的「設定」設定索引標籤。 此自動完成下拉式功能表可讓您指定每個AEM資料夾屬性應該對應至的Workfront欄位。

若要設定對應，請遵循下列步驟：

1. 新增 `jcr:read` 許可權： `/conf/global/settings/dam/adminui-extension/foldermetadataschema` 的 `wf-workfront-users` 群組。
1. 瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 資料夾中繼資料結構]**.
1. 選取您要編輯的資料夾中繼資料結構表單，然後按一下編輯。
1. 選取您要編輯的資料夾中繼資料結構表單欄位，然後在右側面板上選取設定索引標籤。
1. 在 [!UICONTROL 從Workfront欄位對應] 欄位中，選取您要對應至所選AEM資料夾屬性的Workfront欄位名稱。 可用的選項包括：

   * 專案自訂表單欄位
   * 專案概述欄位(識別碼、名稱、說明、參考編號、計畫完成日期、專案所有者、專案贊助者、Portfolio或方案)

![中繼資料對應設定](/help/assets/assets/wf-metadata-mapping-config2.png)

### 設定資產中繼資料對應 {#asset-metadata-mapping}

Adobe Workfront檔案與資產之間的中繼資料對應是在AEM中繼資料結構中定義。 中繼資料結構描述應照常在AEM中建立和設定。 Workfront工具會將設定選項新增至每個中繼資料結構表單欄位的「設定」設定索引標籤。 這些選項可讓您指定每個AEM屬性應該對應至的Workfront欄位。

若要設定對應，請遵循下列步驟：

1. 瀏覽至 **工具** > **資產** > **中繼資料結構**.
1. 選取您要編輯的中繼資料結構表單，然後按一下 **編輯** 或從頭開始建立中繼資料結構。
1. 選取您要編輯的中繼資料結構表單欄位，然後選取 **設定** 標籤。
1. 在 [!DNL Workfront] 自訂表單欄位選取 [!DNL Workfront] 您希望對應到所選AEM屬性的欄位。 可用的選項包括：

   * 記錄自訂表單欄位
   * 專案自訂表單欄位
   * 問題自訂表單欄位
   * 任務自訂表單欄位
   * 專案概述欄位（ID、名稱、說明或參考編號）

1. 在 [!DNL Workfront] 欄位選取於 [!UICONTROL Workfront自訂表單欄位] 是Workfront使用者預先輸入欄位，您必須指定您要對應的Workfront使用者欄位。 若要這麼做，請勾選「從Workfront參考物件欄位取得值」 ，然後指定 [!UICONTROL Workfront使用者自訂表單欄位] 以從中擷取要對映的值。

   ![中繼資料對應設定](/help/assets/assets/wf-metadata-mapping-config1.png)

## 對應屬性 {#map-property}

此工作流程步驟可讓使用者將屬性對應至 [!DNL Workfront] 專案、任務、問題或檔案上的自訂表單。 此 [!DNL Workfront] 此步驟影響的成品會使用裝載中的相對路徑來查詢。 要對應的屬性是從步驟對話方塊設定內控制。

**型別**：此欄位可讓您選取屬性應對應到的Workfront物件型別。

**ID屬性**：此欄位可讓您指定屬性應對應到的Workfront物件ID路徑。 此欄位中指定的路徑應該相對於工作流程裝載。

**屬性指派**：此多欄位可讓您指定AEM屬性與Workfront欄位之間的對應。 多欄位中的每個專案都會指定一個對應。 每個對應都應該有格式 `<workfront-field>=<aem-mapped-property>`.

* 此 `workfront-field` 可以是

   * 前置詞所識別的自訂表單欄位 `DE:`.
   * 由其名稱識別的可編輯欄位。 欄位名稱可在以下位置找到： [[!DNL Workfront] API總管](https://experience.workfront.com/s/api-explorer).

* 此 `aem-mapped-property` 可以是：

   * 常值。 這些應該以引號括住。
   * AEM屬性。 此參考應相對於工作流程裝載。
   * 具名值。 這些應該以方括弧括住。
   * 上述3個專案的串連。 指定，使用 `{+}`.
   * 藉由將值周圍加上，對上述3個專案進行變更 `{replace(<value>,"old-char","new-char")}`.

* 部分範例包括：

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![對應屬性的設定](/help/assets/assets/wf-map-property-config.png)

## 設定狀態 {#set-status}

在工作流程編輯器中，編輯 **[!UICONTROL Workfront — 設定狀態]** 在 **[!UICONTROL 引數]** 標籤。

![編輯工作流程以設定狀態](/help/assets/assets/wf-set-status.png)

## 註解同步 {#comments-sync}

1. 在 [!DNL Experience Manager]，存取 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具設定]**，選取設定，然後選取 **[!UICONTROL 屬性]**.

   ![評論同步](/help/assets/assets/comments-sync1.png)

1. 選取 **[!UICONTROL 活動訂閱]** 標籤，按一下 **[!UICONTROL 啟用評論同步]** 於 **[!UICONTROL 將Workfront中的評論傳送至AEM]** 選項。

   ![已啟用同步](/help/assets/assets/wf-comment-sync-enabled.png)

若要測試從Workfront到AEM的評論同步化，請遵循下列步驟：

1. 導覽至Workfront中的連結檔案，並在更新索引標籤中新增註解。

   ![在Workfront中留下評論](/help/assets/assets/comments-sync2.png)

1. 導覽至AEM中的相同連結檔案，選取檔案並開啟 [!UICONTROL 時間表] 選項，然後選取 [!UICONTROL 註解]. 左側邊欄會顯示從中進行同步處理的評論 [!DNL Workfront].

## 資產版本 {#asset-versions}

若要維護AEM中的資產版本記錄，請在AEM中設定資產版本設定。

1. 在Experience Manager中，存取 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具設定]**，然後開啟 **[!UICONTROL 進階]** 標籤。

1. 選取選項 **[!UICONTROL 以與現有資產版本相同的名稱儲存資產]**. 選取後，此選項可讓您將以相同名稱上傳的資產儲存到與現有資產版本相同的位置。 如果取消勾選，將會以不同名稱建立新資產(例如 `asset-name.pdf` 和 `asset-name-1.pdf`)。

1. 選取選項 **[!UICONTROL 建立版本時更新資產中繼資料]**. 如果勾選，此選項會在建立新版本的資產時更新資產中繼資料。 如果取消勾選，資產將保留建立新版本之前的中繼資料。

![設定資產版本設定](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>連結資料夾中不支援版本設定。 建立 [!DNL Workfront] 檔案在連結資料夾中的校訂，資產先前版本的評論和註解會被移除。

## 附加自訂表單 {#attach-custom-forms}

此工作流程步驟可讓使用者將自訂表單附加至 [!DNL Workfront] 成品。 此工作流程步驟可新增至任何工作流程模型。 此 [!DNL Workfront] 此步驟影響的成品，將會使用裝載中的相對路徑來查閱。

在Experience Manager的工作流程編輯器中，編輯 [!UICONTROL Workfront — 附加自訂表單] 工作流程步驟。

![自訂表格](/help/assets/assets/wf-custom-forms.png).

## 自動發佈資產 {#auto-publish-assets}

1. 在Experience Manager中，存取 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具設定]**，然後開啟 **[!UICONTROL 進階]** 標籤。

1. 選取 **[!UICONTROL 從Workfront傳送時自動發佈資產]**. 此選項可在資產從Workfront傳送至AEM時自動發佈資產。 此功能可透過指定Workfront自訂表單欄位及其應設定的值有條件地啟用。 每當檔案傳送至AEM時，如果符合條件，則會自動發佈資產。

1. 選取 **[!UICONTROL 專案完成時將所有專案資產發佈到Brand Portal]**. 此選項可讓您將資產自動發佈至 [!DNL Brand Portal] 當他們所屬的Workfront專案狀態變更為時 `Complete`.

![設定自動發佈](/help/assets/assets/wf-auto-publish-config.png)

## Workfront檔案自訂表單更新 {#subscribe-workfront-doc-custom-form-updates}

若要訂閱中的變更 [!DNL Workfront] 為自訂表單製作檔案，選取 **[!UICONTROL 進階]** 標籤。 當您訂閱這些更新時，它會更新您對應的更新 [!DNL Experience Manager] 當中的對應欄位時為中繼資料欄位 [!DNL Workfront] 檔案自訂表單已變更。

![Workfront檔案自訂表單更新中的設定 [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
