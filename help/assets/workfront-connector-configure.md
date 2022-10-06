---
title: 設定 [!DNL Workfront for Experience Manager enhanced connector]
description: 設定 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2660de7c-0281-4884-98d9-e78f20cf571c
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1749'
ht-degree: 1%

---

# 設定 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-configure.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-connector-configure.html?lang=en) |

具有管理員存取權的使用者 [!DNL Adobe Experience Manager] 在安裝後配置enhanced connector。 如需安裝指示，請參閱 [安裝連接器](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
>* Adobe需要部署，並配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅透過認證合作夥伴或 [!DNL Adobe Professional Services]. 如果部署和配置時沒有經過認證的合作夥伴或 [!DNL Adobe Professional Services],Adobe不支援。
>
>* Adobe可發行 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使此連接器冗餘；如果發生此情況，客戶可能需要從使用此連接器進行轉變。
>
>* Adobe支援增強的連接器1.7.4版及更新版本。 不支援舊版和自訂版本。 若要檢查增強連接器版本，請導覽至 `digital.hoodoo` 群組(位於 [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant).
>
>* 請參閱 [Workfront for Experience Manager Assets enhanced connector的合作夥伴認證考試](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 有關考試的資訊，請參見 [考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).


## 設定事件訂閱 {#event-subscriptions}

事件訂閱可用來通知AEM發生的事件 [!DNL Adobe Workfront]. 有三個 [!DNL Workfront for Experience Manager enhanced connector] 需要事件訂閱才能運作的功能包括：

* 自動建立項目連結資料夾。
* 同步將Workfront檔案自訂表單值變更為AEM資產中繼資料。
* 專案完成時自動將資產發佈至Brand Portal。

若要使用這些功能，請啟用事件訂閱。

* 編輯 [!UICONTROL Workfront工具] Cloud Services您在步驟5中建立的設定，並選取 [!UICONTROL 事件訂閱] 標籤。
* 選取 [!UICONTROL Workfront自訂整合] 您在第6節中建立。
* 按一下 [!UICONTROL 啟用Workfront事件訂閱].

   ![事件訂閱](/help/assets/assets/event-subs.png)

## 配置連結的資料夾 {#linked-folders}

若要訂閱事件，請依照下列步驟操作：

1. 導覽至 **[!UICONTROL 事件訂閱]** 標籤。
1. 選取中建立的自訂整合 [!DNL Workfront].
1. 按一下 **[!UICONTROL 啟用Workfront事件訂閱]**.

### 連結的資料夾結構配置 {#linked-folder-structure}

1. 前往雲端服務中的「專案連結資料夾」標籤。
1. 連結的資料夾父路徑：在DAM中選取您要建立連結資料夾的資料夾。 如果保留為空白，則預設為/content/dam。 請確定Workfront工具中繼資料結構和Workfront連結資料夾中繼資料結構已套用至選取的資料夾。
1. 連結的資料夾結構：輸入逗號分隔值。 每個值應為 `DE:<some-project-custom-form-field>`、Portfolio、方案、年、名稱或某些「常值字串值」（最後一個帶有引號）。 它當前設定為Portfolio、方案、年、DE：項目類型、名稱。
1. 如果Workfront中資料夾的標題應包含結構中的所有資料夾，則應勾選使用資料夾結構名稱在Workfront中建立連結資料夾標題核取方塊。 否則，會是最後一個資料夾的標題。
1. 子資料夾多欄位可讓您指定應建立為連結資料夾之子資料夾的資料夾清單。
1. 項目狀態：選擇項目必須設定為的狀態以建立連結的資料夾。
1. 在具有產品組合的專案中建立連結資料夾：項目必須屬於的Portfolio清單，才能建立連結的資料夾。 將此清單保留為空白，以便為所有項目組合建立連結的資料夾。
1. 使用自訂表單欄位在專案中建立連結的資料夾：自訂表單欄位及其對應值，專案必須具備才能建立連結的資料夾。 如果保留為空，則會忽略此配置。 選擇 `CUSTOM FORMS: Create DAM Linked Folder` 欄位和輸入 `Yes` （值）。
1. 按一下「啟用自動建立連結的資料夾」。 如果您返回「事件訂閱」標籤，您會看到現在有一個建立事件。

![連結的資料夾組態](/help/assets/assets/wf-linked-folder-config.png)

## 中繼資料結構對應 {#metadata-schema-mapping}

### 配置資料夾元資料映射 {#folder-metadata-mapping}

Workfront專案和AEM資料夾之間的中繼資料對應是在AEM資料夾中繼資料結構中定義。 您應照常在AEM中建立和設定資料夾中繼資料結構。 Workfront工具會將自動完成下拉式清單新增至每個資料夾中繼資料結構表單欄位的「設定設定」設定標籤。 此自動完成下拉式功能表可讓您指定每個AEM資料夾屬性應對應至哪個Workfront欄位。

若要設定對應，請遵循下列步驟：

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 資料夾中繼資料結構]**.
1. 選擇要編輯的資料夾元資料架構表單，然後按一下「編輯」。
1. 選取您要編輯的資料夾中繼資料結構表單欄位，然後在右側面板上選取「設定」標籤。
1. 在 [!UICONTROL 從Workfront欄位對應] 欄位，選取您要對應至所選AEM資料夾屬性的Workfront欄位名稱。 可用選項包括：

   * 專案自訂表單欄位
   * 項目概覽欄位(ID、名稱、說明、參考編號、計畫完成日期、項目責任人、項目贊助商、Portfolio或方案)

![中繼資料對應設定](/help/assets/assets/wf-metadata-mapping-config2.png)

### 設定資產中繼資料對應 {#asset-metadata-mapping}

Adobe Workfront檔案與資產之間的中繼資料對應是在AEM中繼資料結構中定義。 中繼資料結構應照常在AEM中建立和設定。 Workfront工具會將設定選項新增至每個中繼資料結構表單欄位的「設定」設定標籤。 這些選項可讓您指定每個AEM屬性應對應至哪個Workfront欄位。

若要設定對應，請遵循下列步驟：

1. 導覽至 **工具** > **資產** > **中繼資料結構**.
1. 選取您要編輯的中繼資料結構表單，然後按一下 **編輯** 或從頭建立新的中繼資料結構。
1. 選擇要編輯的元資料架構表單欄位並選擇 **設定** 標籤。
1. 在 [!DNL Workfront] 自訂表單欄位選取 [!DNL Workfront] 欄位來對應至選取的AEM屬性。 可用選項包括：

   * 文檔自定義表單欄位
   * 專案自訂表單欄位
   * 發佈自訂表單欄位
   * 任務自定義表單欄位
   * 專案概述欄位（ID、名稱、說明或參考編號）

1. 若 [!DNL Workfront] 在 [!UICONTROL Workfront自訂表單欄位] 是「Workfront使用者」預先輸入欄位，您必須指定您要對應的「Workfront使用者」欄位。 若要這麼做，請核取從Workfront參考的物件欄位取得值，然後指定 [!UICONTROL Workfront使用者自訂表單欄位] 從中擷取要映射的值。

   ![中繼資料對應設定](/help/assets/assets/wf-metadata-mapping-config1.png)

## 映射屬性 {#map-property}

此工作流程步驟可讓使用者將屬性對應至 [!DNL Workfront] 項目、任務、問題或文檔上的自定義表單。 此 [!DNL Workfront] 對象此步驟影響使用來自有效負載的相對路徑查找。 要映射的屬性是從步驟對話框配置中控制的。

**類型**:此欄位可讓您選取屬性應對應的Workfront物件類型。

**ID屬性**:此欄位可讓您指定屬性應對應的Workfront物件ID的路徑。 此欄位中指定的路徑應相對於工作流程裝載。

**屬性分配**:此多欄位可讓您指定AEM屬性與Workfront欄位之間的對應。 多欄位中的每個項目將指定一個對應。 每個對應都應有格式 `<workfront-field>=<aem-mapped-property>`.

* 此 `workfront-field` 可以

   * 由首碼識別的自訂表單欄位 `DE:`.
   * 由其名稱標識的可編輯欄位。 欄位名稱位於 [[!DNL Workfront] API總管](https://experience.workfront.com/s/api-explorer).

* 此 `aem-mapped-property` 可以是：

   * 常值。 這些字元應以引號括住。
   * AEM屬性。 此參考應相對於工作流程裝載。
   * 已命名的值。 這些應由方括弧包住。
   * 上述3個項目的串連。 使用指定 `{+}`.
   * 對以上3項的修改，請以 `{replace(<value>,"old-char","new-char")}`.

* 例如：

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![映射屬性的配置](/help/assets/assets/wf-map-property-config.png)

## 設定狀態 {#set-status}

在工作流程編輯器中，編輯 **[!UICONTROL Workfront — 設定狀態]** 在 **[!UICONTROL 引數]** 標籤。

![編輯工作流以設定狀態](/help/assets/assets/wf-set-status.png)

## 注釋同步 {#comments-sync}

1. 在 [!DNL Experience Manager]，存取 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具設定]**，選取設定，然後選取 **[!UICONTROL 屬性]**.

   ![註解同步](/help/assets/assets/comments-sync1.png)

1. 選擇 **[!UICONTROL 事件訂閱]** 按一下 **[!UICONTROL 啟用注釋同步]** on **[!UICONTROL 將在Workfront中發表的意見傳送至AEM]** 選項。

   ![已啟用同步](/help/assets/assets/wf-comment-sync-enabled.png)

若要測試從Workfront到AEM的註解同步化，請執行下列步驟：

1. 導覽至Workfront中的連結檔案，並在「更新」索引標籤中新增註解。

   ![在Workfront留言](/help/assets/assets/comments-sync2.png)

1. 在AEM中導覽至相同的連結檔案，選取檔案並開啟 [!UICONTROL 時間表] 選項，然後選取 [!UICONTROL 註解]. 左側邊欄顯示已同步的注釋 [!DNL Workfront].

## 資產版本 {#asset-versions}

若要在AEM中維護資產的版本記錄，請在AEM中設定資產版本設定。

1. 在Experience Manager中，存取 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具設定]**，然後開啟 **[!UICONTROL 進階]** 標籤。

1. 選擇選項 **[!UICONTROL 儲存與現有資產版本同名的資產]**. 若勾選此選項，可將以相同名稱上傳的資產儲存至與現有資產版本相同的位置。 如果未勾選，則會以不同名稱建立新資產(例如 `asset-name.pdf` 和 `asset-name-1.pdf`)。

1. 選擇選項 **[!UICONTROL 建立新版本時更新資產中繼資料]**. 若勾選此選項，每當建立新版本的資產時，此選項就會更新資產中繼資料。 如果取消勾選，資產會保留建立新版本之前的中繼資料。

![設定資產版本設定](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>連結的資料夾不支援版本設定。 建立 [!DNL Workfront] 使用連結資料夾內的檔案進行校樣，會移除舊版資產上的註解和註解。

## 附加自訂表單 {#attach-custom-forms}

此工作流程步驟可讓使用者將自訂表單附加至 [!DNL Workfront] 藏物。 此工作流程步驟可新增至任何工作流程模型。 此 [!DNL Workfront] 將使用來自有效負載的相對路徑查找此步驟影響的對象。

在Experience Manager的工作流程編輯器中，編輯 [!UICONTROL Workfront — 附加自訂表單] 工作流程步驟。

![自訂表單](/help/assets/assets/wf-custom-forms.png).

## 自動發佈資產 {#auto-publish-assets}

1. 在Experience Manager中，存取 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具設定]**，然後開啟 **[!UICONTROL 進階]** 標籤。

1. 選擇 **[!UICONTROL 從Workfront傳送時自動發佈資產]**. 此選項可在資產從Workfront傳送至AEM時啟用自動發佈。 您可以指定Workfront自訂表單欄位，並將其設為值，以有條件地啟用此功能。 每當檔案傳送至AEM時，如果檔案滿足條件，資產就會自動發佈。

1. 選擇 **[!UICONTROL 專案完成時將所有專案資產發佈至Brand Portal]**. 此選項可讓資產自動發佈至 [!DNL Brand Portal] 當其所屬Workfront專案的狀態變更為 `Complete`.

![設定自動發佈](/help/assets/assets/wf-auto-publish-config.png)

## Workfront檔案自訂表單更新 {#subscribe-workfront-doc-custom-form-updates}

若要訂閱 [!DNL Workfront] 自訂表單，請選取 **[!UICONTROL 進階]** 標籤。 當您訂閱這些更新時，會更新您對應的 [!DNL Experience Manager] 中對應欄位時的中繼資料欄位 [!DNL Workfront] 文檔自定義表單已更改。

![Workfront檔案自訂表單更新設定 [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
