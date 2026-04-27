---
title: 設定 [!DNL Workfront for Experience Manager enhanced connector]
description: 設定 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 2660de7c-0281-4884-98d9-e78f20cf571c
hide: true
solution: Experience Manager, Workfront
source-git-commit: bca6156727dca11b2e09be549f3def6130827193
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 1%

---

# 設定 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-configure.html?lang=en) |
| AEM 6.5 | 本文章 |

在[!DNL Adobe Experience Manager]中擁有管理員存取許可權的使用者會在安裝增強型聯結器後進行設定。 如需安裝說明，請參閱[安裝聯結器](/help/assets/workfront-integrations.md)。

>[!IMPORTANT]
>
>* Adobe僅需要透過認證合作夥伴或[!DNL Adobe Professional Services]來部署及設定[!DNL Adobe Workfront for Experience Manager enhanced connector]。 如果未透過認證合作夥伴或[!DNL Adobe Professional Services]進行部署與設定，則Adobe不支援此功能。
>
>* Adobe可能會發行[!DNL Adobe Workfront]和[!DNL Adobe Experience Manager]的更新，使此聯結器成為多餘的；如果發生這種情況，客戶可能需要從使用此聯結器進行轉換。
>
>* Adobe支援增強型聯結器1.7.4版及更新版本。 不支援舊版發行前版本和自訂版本。 若要檢查增強型聯結器版本，請瀏覽至[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant)左側窗格中可用的`digital.hoodoo`群組。
>
>* 請參閱Experience Manager Assets增強型聯結器的[Workfront合作夥伴認證測驗](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)。 如需有關考試的資訊，請參閱[考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)。

## 設定事件訂閱 {#event-subscriptions}

事件訂閱是用來通知AEM [!DNL Adobe Workfront]中發生的事件。 有三個[!DNL Workfront for Experience Manager enhanced connector]功能需要事件訂閱才能運作，分別為：

* 自動建立專案連結資料夾。
* 同步Workfront檔案自訂表單值與AEM資產中繼資料的變更。
* 專案完成時將資產自動發佈到Brand Portal。

若要使用這些功能，請啟用事件訂閱。

* 編輯您在步驟5建立的[!UICONTROL Workfront工具]雲端服務設定，並選取[!UICONTROL 事件訂閱]索引標籤。
* 選取您在第6節中建立的[!UICONTROL Workfront自訂整合]。
* Click [!UICONTROL Enable Workfront Event Subscriptions].

  ![Event subscription](/help/assets/assets/event-subs.png)

## Configure linked folders {#linked-folders}

To subscribe to the events, follow these steps:

1. Navigate to the **[!UICONTROL Event Subscriptions]** tab in the cloud services.
1. Select the custom integration created in [!DNL Workfront].
1. Click **[!UICONTROL Enable Workfront Event Subscriptions]**.

### Linked folder structure configuration {#linked-folder-structure}

1. Go to the Project Linked Folders tab in the cloud services.
1. Linked folder parent path: Select a folder in the DAM where you wish to create the linked folders. If left empty, it will default to /content/dam. Make sure that the Workfront Tools metadata schema and Workfront Linked Folder folder metadata schema have been applied to the selected folder.
1. Linked folder structure: Enter comma-separated values. Each value should be `DE:<some-project-custom-form-field>`, Portfolio, Program, Year, Name, or some &quot;Literal String Value&quot; (this last one with quotation marks). It is currently set to Portfolio,Program,Year,DE:Project Type,Name.
1. Configure permissions: Add `jcr:all permissions` permissions to `/conf/workfront-tools/settings/cloudconfigs` for `wf-workfront-users` group.
1. Build linked folder title in Workfront using the folder structure names checkbox should be checked if the title of the folder in Workfront should include all folders in the structure. Otherwise, it is the title of the last folder.
1. Sub-folders multifield lets you specify a list of folders that should be created as a child folder of the linked folder.
1. Project status: Select the status of the project to create the linked folder.
1. Create a linked folder in projects with portfolio: List of Portfolios to which the project must belong to create the linked folder. Leave this list empty to create the linked folder for all project portfolio.
1. Create a linked folder in projects with custom form field: Custom form field and its corresponding value that the project has to have to create the linked folder. This configuration is ignored if left empty. Select `CUSTOM FORMS: Create DAM Linked Folder` for the field and input `Yes` for the value.
1. Click on Enable automatic creation of linked folders. If you go back to the Event Subscriptions tab, you&#39;ll see there is now one create event.

![linked folder configuration](/help/assets/assets/wf-linked-folder-config.png)

## Metadata schema mapping {#metadata-schema-mapping}

### Configure folder metadata mapping {#folder-metadata-mapping}

Metadata mapping between Workfront Projects and AEM Folders is defined within AEM Folder Metadata Schemas. Folder Metadata Schemas should be created and configured as usual in AEM. Workfront Tools adds an autocomplete dropdown to the Settings configuration tab of each folder metadata schema form field. This autocomplete drop- down menu will let you specify to which Workfront field each AEM folder property should be mapped to.

To configure the mappings, follow these steps:

1. Add `jcr:read` permissions to `/conf/global/settings/dam/adminui-extension/foldermetadataschema` for `wf-workfront-users` group.
1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Folder Metadata Schemas]**.
1. Select the folder metadata schema form you wish to edit and click Edit.
1. Select the folder metadata schema form field you wish to edit and select Settings tab on the right panel.
1. In [!UICONTROL Mapped from Workfront Field] field, select the name of the Workfront field that you wish to map to the selected AEM folder property. Available options are:

   * Project custom form fields
   * Project Overview fields (ID, Name, Description, Reference Number, Planned Completion Date, Project Owner, Project Sponsor, Portfolio or Program)

![metadata mapping config](/help/assets/assets/wf-metadata-mapping-config2.png)

### 設定資產中繼資料對應 {#asset-metadata-mapping}

Metadata mapping between Adobe Workfront Documents and Assets is defined within AEM Metadata Schemas. Metadata Schemas should be created and configured as usual in AEM. Workfront Tools adds configuration options to the Settings configuration tab of each metadata schema form field. These options will let you specify to which Workfront field each AEM property should be mapped to.

To configure the mappings, follow these steps:

1. Navigate to **Tools** > **Assets** > **Metadata Schemas**.
1. 選取您要編輯的中繼資料結構描述表單，然後按一下&#x200B;**編輯**&#x200B;或從頭開始建立中繼資料結構描述。
1. 選取您要編輯的中繼資料結構表單欄位，然後選取右側面板上的&#x200B;**設定**&#x200B;索引標籤。
1. 在「[!DNL Workfront]自訂表單欄位」中，選取您要對應至所選AEM屬性的[!DNL Workfront]欄位名稱。 可用的選項包括：

   * 記錄自訂表單欄位
   * 專案自訂表單欄位
   * 問題自訂表單欄位
   * 任務自訂表單欄位
   * 專案概述欄位（ID、名稱、說明或參考編號）

1. 如果在[!UICONTROL Workfront自訂表單欄位]中選取的[!DNL Workfront]欄位是Workfront使用者預先輸入欄位，則需要指定您要對應哪個Workfront使用者欄位。 若要這麼做，請核取從Workfront參考物件欄位取得值，然後指定要從中擷取對應值的[!UICONTROL Workfront使用者自訂表單欄位]的名稱。

   ![中繼資料對應設定](/help/assets/assets/wf-metadata-mapping-config1.png)

## 對應屬性 {#map-property}

此工作流程步驟可讓使用者將屬性對應至專案、任務、問題或檔案上的[!DNL Workfront]自訂表單。 此步驟影響的[!DNL Workfront]成品會使用承載中的相對路徑來查詢。 要對應的屬性是從步驟對話方塊設定內控制。

**型別**：此欄位可讓您選取屬性應對應到的Workfront物件型別。

**ID屬性**：此欄位可讓您指定屬性應對應到的Workfront物件識別碼路徑。 此欄位中指定的路徑應該相對於工作流程裝載。

**屬性指派**：此多欄位可讓您指定AEM屬性與Workfront欄位之間的對應。 多欄位中的每個專案都會指定一個對應。 每個對應的格式應該是`<workfront-field>=<aem-mapped-property>`。

* `workfront-field`可以是

   * 前置詞`DE:`所識別的自訂表單欄位。
   * 由其名稱識別的可編輯欄位。 在[[!DNL Workfront] API總管](https://experience.workfront.com/s/api-explorer)中找到欄位名稱。

* `aem-mapped-property` 可能是：

   * 常值。 這些應該以引號括住。
   * AEM屬性。 此參考應相對於工作流程裝載。
   * 具名值。 這些應該以方括弧括住。
   * 上述3個專案的串連。 使用`{+}`指定它。
   * 以`{replace(<value>,"old-char","new-char")}`包圍值來變更上述3個專案。

* 部分範例包括：

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![對應屬性的組態](/help/assets/assets/wf-map-property-config.png)

## 設定狀態 {#set-status}

在工作流程編輯器中，編輯&#x200B;**[!UICONTROL Workfront — 在**[!UICONTROL &#x200B;引數&#x200B;]**索引標籤中設定狀態]**&#x200B;的屬性。

![編輯工作流程以設定狀態](/help/assets/assets/wf-set-status.png)

## 註解同步 {#comments-sync}

1. 在[!DNL Experience Manager]中，存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL Workfront工具組態]**，選取組態並選取&#x200B;**[!UICONTROL 屬性]**。

   ![個註解同步](/help/assets/assets/comments-sync1.png)

1. 選取&#x200B;**[!UICONTROL 事件訂閱]**&#x200B;索引標籤，按一下&#x200B;**[!UICONTROL 將Workfront中的評論傳送至AEM]**&#x200B;選項上的&#x200B;**[!UICONTROL 啟用評論同步]**。

   ![同步處理已啟用](/help/assets/assets/wf-comment-sync-enabled.png)

若要測試從Workfront到AEM的評論同步化，請遵循下列步驟：

1. 導覽至Workfront中的連結檔案，並在更新索引標籤中新增註解。

   ![在Workfront中留下註解](/help/assets/assets/comments-sync2.png)

1. 導覽至AEM中的相同連結檔案，選取檔案並開啟左側導覽中的[!UICONTROL 時間表]選項，然後選取[!UICONTROL 註解]。 左側邊欄顯示從[!DNL Workfront]同步處理的註解。

## 資產版本 {#asset-versions}

若要維護AEM中的資產版本記錄，請在AEM中設定資產版本設定。

1. 在Experience Manager中，存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL Workfront工具設定]**，然後開啟&#x200B;**[!UICONTROL 進階]**&#x200B;標籤。

1. 選取選項&#x200B;**[!UICONTROL 儲存與現有資產版本同名的資產]**。 選取後，此選項可讓您將以相同名稱上傳的資產儲存到與現有資產版本相同的位置。 如果未勾選，則會以不同的名稱（例如`asset-name.pdf`和`asset-name-1.pdf`）建立新資產。

1. 選取選項&#x200B;**[!UICONTROL 建立版本]**&#x200B;時更新資產中繼資料。 如果勾選，此選項會在建立新版本的資產時更新資產中繼資料。 如果取消勾選，資產將保留建立新版本之前的中繼資料。

![設定資產版本設定](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>連結資料夾中不支援版本設定。 當在連結的資料夾內建立具有檔案的[!DNL Workfront]校訂時，將移除資產先前版本上的註解與註解。

## 附加自訂表單 {#attach-custom-forms}

此工作流程步驟可讓使用者將自訂表單附加至[!DNL Workfront]成品。 此工作流程步驟可新增至任何工作流程模型。 此步驟影響的[!DNL Workfront]成品將使用承載中的相對路徑來查閱。

在Experience Manager的工作流程編輯器中，編輯[!UICONTROL Workfront — 附加自訂表單]工作流程步驟的屬性。

![自訂表單](/help/assets/assets/wf-custom-forms.png)。

## 自動發佈資產 {#auto-publish-assets}

1. 在Experience Manager中，存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL Workfront工具設定]**，然後開啟&#x200B;**[!UICONTROL 進階]**&#x200B;標籤。

1. 選取&#x200B;**[!UICONTROL 從Workfront]**&#x200B;傳送時自動發佈資產。 此選項可在資產從Workfront傳送至AEM時自動發佈資產。 此功能可透過指定Workfront自訂表單欄位及其應設定的值有條件地啟用。 每當檔案傳送至AEM時，如果符合條件，則會自動發佈資產。

1. 選取&#x200B;**[!UICONTROL 在專案完成時將所有專案資產發佈到Brand Portal]**。 This option enables automatic publishing of assets to [!DNL Brand Portal] when the status of the Workfront project they belong to is changed to `Complete`.

![configure auto-publish](/help/assets/assets/wf-auto-publish-config.png)

## Workfront document custom form updates {#subscribe-workfront-doc-custom-form-updates}

To subscribe to the changes in [!DNL Workfront] document custom forms, select the relevant option in the **[!UICONTROL Advanced]** tab. When you subscribe to these updates, it updates your mapped [!DNL Experience Manager] metadata fields when the corresponding field in [!DNL Workfront] document custom form is changed.

![Workfront document custom form updates configuration in [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
