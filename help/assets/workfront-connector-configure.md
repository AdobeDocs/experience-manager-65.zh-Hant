---
title: 設定 [!DNL Workfront for Experience Manager enhanced connector]
description: 設定 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 2660de7c-0281-4884-98d9-e78f20cf571c
hide: true
solution: Experience Manager, Workfront
source-git-commit: 5ccac0aadce3971e66da052d393cbd33b61e94f7
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 1%

---

# 設定 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-configure.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

在[!DNL Adobe Experience Manager]中擁有管理員存取許可權的使用者會在安裝增強型聯結器後進行設定。 如需安裝說明，請參閱[安裝聯結器](/help/assets/workfront-integrations.md)。

>[!IMPORTANT]
>
>* Adobe僅需要透過認證合作夥伴或[!DNL Adobe Professional Services]來部署和設定[!DNL Adobe Workfront for Experience Manager enhanced connector]。 如果未使用認證合作夥伴或[!DNL Adobe Professional Services]進行部署與設定，則Adobe不支援此功能。
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

* 編輯您在步驟5建立的[!UICONTROL Workfront工具]Cloud Service設定，並選取[!UICONTROL 事件訂閱]索引標籤。
* 選取您在第6節中建立的[!UICONTROL Workfront自訂整合]。
* 按一下[!UICONTROL 啟用Workfront活動訂閱]。

  ![活動訂閱](/help/assets/assets/event-subs.png)

## 設定連結的資料夾 {#linked-folders}

若要訂閱事件，請遵循下列步驟：

1. 導覽至雲端服務中的&#x200B;**[!UICONTROL 事件訂閱]**&#x200B;索引標籤。
1. 選取在[!DNL Workfront]中建立的自訂整合。
1. 按一下&#x200B;**[!UICONTROL 啟用Workfront活動訂閱]**。

### 連結的資料夾結構設定 {#linked-folder-structure}

1. 前往雲端服務中的專案連結資料夾索引標籤。
1. 連結資料夾父路徑：在DAM中選取您想要建立連結資料夾的資料夾。 如果留空，其將預設為/content/dam。 請確定Workfront工具中繼資料結構和Workfront連結資料夾中繼資料結構已套用至選取的資料夾。
1. 連結的資料夾結構：輸入逗號分隔值。 每個值應該是`DE:<some-project-custom-form-field>`、Portfolio、方案、年份、名稱或某個「常值字串值」（最後一個值加上引號）。 目前設為Portfolio、方案、年、DE：專案型別、名稱。
1. 設定許可權：為`wf-workfront-users`群組新增`jcr:all permissions`許可權至`/conf/workfront-tools/settings/cloudconfigs`。
1. 如果Workfront中的資料夾標題應包含結構中的所有資料夾，則應核取使用資料夾結構名稱在Workfront中建立連結資料夾標題。 否則，這是最後一個資料夾的標題。
1. 子資料夾多欄位可讓您指定應建立為連結資料夾的子資料夾的資料夾清單。
1. 專案狀態：選取專案狀態以建立連結的資料夾。
1. 在具有投資組合的專案中建立連結資料夾：專案必須屬於其中建立連結資料夾的Portfolio清單。 將此清單保留為空白可為所有專案組合建立連結資料夾。
1. 使用自訂表單欄位在專案中建立連結資料夾：自訂表單欄位及其對應的值，專案必須建立連結資料夾。 如果留為空白，則會忽略此設定。 選取`CUSTOM FORMS: Create DAM Linked Folder`作為欄位，並輸入`Yes`作為值。
1. 按一下啟用自動建立連結資料夾。 如果您返回「事件訂閱」標籤，現在會看到有一個建立事件。

![連結的資料夾組態](/help/assets/assets/wf-linked-folder-config.png)

## 中繼資料結構描述對應 {#metadata-schema-mapping}

### 設定資料夾中繼資料對應 {#folder-metadata-mapping}

Workfront專案與AEM資料夾之間的中繼資料對應是在AEM資料夾中繼資料結構中定義。 應照常在AEM中建立和設定資料夾中繼資料結構。 Workfront工具會將自動完成下拉式清單新增至每個資料夾中繼資料結構表單欄位的「設定」設定索引標籤。 此自動完成下拉式功能表可讓您指定每個AEM資料夾屬性應該對應至的Workfront欄位。

若要設定對應，請遵循下列步驟：

1. 為`wf-workfront-users`群組新增`jcr:read`許可權至`/conf/global/settings/dam/adminui-extension/foldermetadataschema`。
1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 資料夾中繼資料結構]**。
1. 選取您要編輯的資料夾中繼資料結構表單，然後按一下編輯。
1. 選取您要編輯的資料夾中繼資料結構表單欄位，然後在右側面板上選取設定索引標籤。
1. 在[!UICONTROL 從Workfront欄位對應]欄位中，選取您要對應到所選AEM資料夾屬性的Workfront欄位名稱。 可用的選項包括：

   * 專案自訂表單欄位
   * 專案概述欄位(識別碼、名稱、說明、參考編號、計畫完成日期、專案所有者、專案贊助者、Portfolio或方案)

![中繼資料對應設定](/help/assets/assets/wf-metadata-mapping-config2.png)

### 設定資產中繼資料對應 {#asset-metadata-mapping}

Adobe Workfront檔案與Assets之間的中繼資料對應是在AEM中繼資料結構中定義。 中繼資料結構描述應照常在AEM中建立和設定。 Workfront工具會將設定選項新增至每個中繼資料結構表單欄位的「設定」設定索引標籤。 這些選項可讓您指定每個AEM屬性應該對應至的Workfront欄位。

若要設定對應，請遵循下列步驟：

1. 導覽至&#x200B;**工具** > **Assets** > **中繼資料結構描述**。
1. 選取您要編輯的中繼資料結構描述表單，然後按一下&#x200B;**編輯**&#x200B;或從頭開始建立中繼資料結構描述。
1. 選取您要編輯的中繼資料結構表單欄位，然後選取右側面板上的&#x200B;**設定**&#x200B;索引標籤。
1. 在[!DNL Workfront]自訂表單欄位中，選取您要對應至所選AEM屬性的[!DNL Workfront]欄位名稱。 可用的選項包括：

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

* `aem-mapped-property`可以是：

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

在工作流程編輯器中，編輯&#x200B;**[!UICONTROL Workfront — 在**&#x200B;[!UICONTROL &#x200B;引數&#x200B;]&#x200B;**索引標籤中設定狀態]**&#x200B;的屬性。

![編輯工作流程以設定狀態](/help/assets/assets/wf-set-status.png)

## 註解同步 {#comments-sync}

1. 在[!DNL Experience Manager]中，存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具組態]**，選取組態並選取&#x200B;**[!UICONTROL 屬性]**。

   ![個註解同步](/help/assets/assets/comments-sync1.png)

1. 選取&#x200B;**[!UICONTROL 事件訂閱]**&#x200B;索引標籤，按一下&#x200B;**[!UICONTROL 將Workfront中的評論傳送至AEM]**&#x200B;選項上的&#x200B;**[!UICONTROL 啟用評論同步處理]**。

   ![同步處理已啟用](/help/assets/assets/wf-comment-sync-enabled.png)

若要測試從Workfront到AEM的評論同步化，請遵循下列步驟：

1. 導覽至Workfront中的連結檔案，並在更新索引標籤中新增註解。

   ![在Workfront中留下註解](/help/assets/assets/comments-sync2.png)

1. 導覽至AEM中的相同連結檔案，選取檔案並開啟左側導覽中的[!UICONTROL 時間表]選項，然後選取[!UICONTROL 註解]。 左側邊欄顯示從[!DNL Workfront]同步處理的註解。

## 資產版本 {#asset-versions}

若要維護AEM中的資產版本記錄，請在AEM中設定資產版本設定。

1. 在Experience Manager中，存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具組態]**，然後開啟&#x200B;**[!UICONTROL 進階]**&#x200B;標籤。

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

1. 在Experience Manager中，存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具組態]**，然後開啟&#x200B;**[!UICONTROL 進階]**&#x200B;標籤。

1. 選取&#x200B;**[!UICONTROL 從Workfront]**&#x200B;傳送時自動發佈資產。 此選項可在資產從Workfront傳送至AEM時自動發佈資產。 此功能可透過指定Workfront自訂表單欄位及其應設定的值有條件地啟用。 每當檔案傳送至AEM時，如果符合條件，則會自動發佈資產。

1. 選取&#x200B;**[!UICONTROL 在專案完成時，將所有專案資產Publish到Brand Portal]**。 此選項可讓您在資產所屬的Workfront專案狀態變更為`Complete`時，將資產自動發佈至[!DNL Brand Portal]。

![設定自動發佈](/help/assets/assets/wf-auto-publish-config.png)

## Workfront檔案自訂表單更新 {#subscribe-workfront-doc-custom-form-updates}

若要訂閱[!DNL Workfront]檔案自訂表單中的變更，請在&#x200B;**[!UICONTROL 進階]**&#x200B;索引標籤中選取相關選項。 當您訂閱這些更新時，它會在[!DNL Workfront]檔案自訂表單中的對應欄位變更時更新您對應的[!DNL Experience Manager]中繼資料欄位。

![在[!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)中的Workfront檔案自訂表單更新設定
