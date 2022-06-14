---
title: 設定 [!DNL Workfront for Experience Manager enhanced connector]
description: 設定 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2660de7c-0281-4884-98d9-e78f20cf571c
source-git-commit: 00713ea7fe06d4e180232e48a9e3f11b53f4326f
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 0%

---

# 設定 [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

具有管理員訪問權限的用戶 [!DNL Adobe Experience Manager] 在安裝增強的連接器後配置它。 有關安裝的說明，請參見 [安裝連接器](/help/assets/workfront-integrations.md)。

>[!IMPORTANT]
>
>* Adobe需要部署和配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 僅通過認證合作夥伴或 [!DNL Adobe Professional Services]。 如果部署和配置時沒有經過認證的合作夥伴或 [!DNL Adobe Professional Services]，它不受Adobe支援。
>
>* Adobe可以發佈更新 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使這個連接器冗餘；如果發生這種情況，可能需要客戶從使用此連接器進行過渡。
>
>* Adobe支援增強的連接器1.7.4版和更高版本。 不支援以前的預發行版和自定義版本。 要檢查增強的連接器版本，請導航至 `digital.hoodoo` 組在的左窗格中可用 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant)。
>
>* 請參閱 [Workfront的Experience Manager Assets增強型連接器合作夥伴認證考試](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)。 有關考試的資訊，請參見 [考試指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)。


## 配置事件訂閱 {#event-subscriptions}

事件預訂用於通AEM知發生在 [!DNL Adobe Workfront]。 有三個 [!DNL Workfront for Experience Manager enhanced connector] 需要事件預訂才能工作的功能包括：

* 自動建立項目連結資料夾。
* 將Workfront文檔自定義表單值中的更改同AEM步到資產元資料。
* 在項目完成後自動向Brand Portal公佈資產。

要使用這些功能，請啟用事件訂閱。

* 編輯 [!UICONTROL Workfront工具] Cloud Services在步驟5中建立的配置，並選擇 [!UICONTROL 事件訂閱] 頁籤。
* 選擇 [!UICONTROL Workfront定制整合] 在第6節中建立。
* 按一下 [!UICONTROL 啟用Workfront事件訂閱]。

   ![事件訂閱](/help/assets/assets/event-subs.png)

## 配置連結資料夾 {#linked-folders}

要訂閱事件，請執行以下步驟：

1. 導航到 **[!UICONTROL 事件訂閱]** 頁籤。
1. 選擇在中建立的自定義整合 [!DNL Workfront]。
1. 按一下 **[!UICONTROL 啟用Workfront事件訂閱]**。

### 連結資料夾結構配置 {#linked-folder-structure}

1. 轉到雲服務中的「項目連結資料夾」頁籤。
1. 連結的資料夾父路徑：在DAM中選擇要建立連結資料夾的資料夾。 如果為空，則預設為/content/dam。 確保已將Workfront工具元資料架構和Workfront連結資料夾元資料架構應用到所選資料夾。
1. 連結資料夾結構：輸入逗號分隔的值。 每個值應為 `DE:<some-project-custom-form-field>`、Portfolio、程式、年份、名稱或某些「文字字串值」（最後一個帶有引號）。 它當前設定為Portfolio、程式、年、DE：項目類型、名稱。
1. 如果Workfront中資料夾的標題應包含結構中的所有資料夾，則應選中使用資料夾結構名稱在Workfront中生成連結資料夾標題複選框。 否則，它將是最後一個資料夾的標題。
1. 子資料夾多欄位允許您指定應作為連結資料夾的子資料夾建立的資料夾清單。
1. 項目狀態：選擇項目必須設定為以建立連結資料夾的狀態。
1. 在項目中建立連結的資料夾，包括：項目必須屬於以建立連結資料夾的Portfolio清單。 將此清單留空，以為所有項目組合建立連結資料夾。
1. 在具有自定義表單域的項目中建立連結資料夾：為建立連結資料夾，項目必須具有的自定義表單域及其相應值。 如果此配置為空，則將忽略此配置。 選擇 `CUSTOM FORMS: Create DAM Linked Folder` 欄位和輸入 `Yes` 值。
1. 按一下「Enable automatic creation of linked folders（啟用自動建立連結資料夾）」。 如果返回「事件訂閱」頁籤，您將看到現在有一個建立事件。

![連結資料夾配置](/help/assets/assets/wf-linked-folder-config.png)

## 元資料架構映射 {#metadata-schema-mapping}

### 配置資料夾元資料映射 {#folder-metadata-mapping}

Workfront項目和資料夾之間的元AEM資料映射是在資料夾元資料AEM架構中定義的。 資料夾元資料架構應按照中的常規建立和配AEM置。 Workfront工具將自動完成下拉清單添加到每個資料夾元資料架構表單域的「設定」配置頁籤。 此自動完成下拉菜單將允許您指定每個資料夾屬AEM性應映射到的Workfront欄位。

要配置映射，請執行以下步驟：

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 資料夾元資料架構]**。
1. 選擇要編輯的資料夾元資料架構表單，然後按一下編輯。
1. 選擇要編輯的資料夾元資料架構表單域，然後在右面板上選擇「設定」頁籤。
1. 在 [!UICONTROL 從Workfront欄位映射] 欄位，選擇要映射到選定資料夾屬性的Workfront字AEM段的名稱。 可用選項包括：

   * 項目自定義表單域
   * 項目概覽欄位(ID、名稱、說明、參考編號、計畫完成日期、項目責任人、項目發起人、Portfolio或項目群)

![元資料映射配置](/help/assets/assets/wf-metadata-mapping-config2.png)

### 配置資產元資料映射 {#asset-metadata-mapping}

Adobe Workfront文檔和資產之間的元資料映射是在元資料架構AEM中定義的。 元資料架構應按照中的常規建立和配AEM置。 Workfront工具將配置選項添加到每個元資料架構表單域的「設定」配置頁籤。 這些選項將允許您指定每個屬性應映射到AEM哪個Workfront欄位。

要配置映射，請執行以下步驟：

1. 導航到 **工具** > **資產** > **元資料架構**。
1. 選擇要編輯的元資料架構表單，然後按一下 **編輯** 或從頭建立新的元資料架構。
1. 選擇要編輯的元資料架構表單域並選擇 **設定** 頁籤。
1. 在 [!DNL Workfront] 自定義表單域選擇 [!DNL Workfront] 要映射到選定屬性的字AEM段。 可用選項包括：

   * 文檔自定義表單域
   * 項目自定義表單域
   * 發佈自定義表單域
   * 任務自定義表單域
   * 項目概覽欄位（ID、名稱、說明或參考編號）

1. 如果 [!DNL Workfront] 選定的欄位 [!UICONTROL Workfront自定義窗體欄位] 是「Workfront用戶預先類型」欄位，需要指定要映射的「Workfront用戶」欄位。 為此，請選中「從Workfront引用的對象欄位獲取值」，然後指定 [!UICONTROL Workfront用戶自定義表單域] 從中檢索要映射的值。

   ![元資料映射配置](/help/assets/assets/wf-metadata-mapping-config1.png)

## 映射屬性 {#map-property}

此工作流步驟允許用戶將屬性映射到 [!DNL Workfront] 項目、任務、問題或文檔上的自定義窗體。 的 [!DNL Workfront] 此步驟影響的項目是使用有效負載的相對路徑查找的。 要映射的屬性在步驟對話框配置中進行控制。

**類型**:此欄位允許您選擇屬性應映射到的Workfront對象類型。

**ID屬性**:此欄位用於指定屬性應映射到的Workfront對象ID的路徑。 此欄位中指定的路徑應與工作流負載相關。

**屬性分配**:此多欄位允許您指定屬性和AEMWorkfront欄位之間的映射。 多欄位中的每個項都將指定一個映射。 每個映射應具有格式 `<workfront-field>=<aem-mapped-property>`。

* 的 `workfront-field` 可以

   * 由前置詞標識的自定義表單域 `DE:`。
   * 由名稱標識的可編輯欄位。 欄位名稱在 [[!DNL Workfront] API資源管理器](https://experience.workfront.com/s/api-explorer)。

* 的 `aem-mapped-property` 可以：

   * 文本值。 這些應用引號括起來。
   * 一個AEM財產。 此引用應與工作流負載相關。
   * 命名值。 這些應用括弧括起來。
   * 以上3項的串聯。 使用 `{+}`。
   * 以上三項的修改 `{replace(<value>,”old-char”,”new-char”)}`。

* 例如：

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL=”https://my-aem-author/assets.html”{+}{path}`

![要映射的配置屬性](/help/assets/assets/wf-map-property-config.png)

## 設定狀態 {#set-status}

在工作流編輯器中，編輯 **[!UICONTROL Workfront — 設定狀態]** 的 **[!UICONTROL 參數]** 頁籤。

![編輯工作流以設定狀態](/help/assets/assets/wf-set-status.png)

## 注釋同步 {#comments-sync}

1. 在 [!DNL Experience Manager]訪問 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具配置]**，選擇配置，然後選擇 **[!UICONTROL 屬性]**。

   ![注釋同步](/help/assets/assets/comments-sync1.png)

1. 選擇 **[!UICONTROL 事件訂閱]** 按鈕 **[!UICONTROL 啟用注釋同步]** 上 **[!UICONTROL 將在Workfront發表的評AEM論]** 的雙曲餘切值。

   ![已啟用同步](/help/assets/assets/wf-comment-sync-enabled.png)

要test從Workfront到的注釋的同步，請執AEM行以下步驟：

1. 導航到Workfront中的連結文檔，並在「更新」頁籤中添加註釋。

   ![在Workfront發表評論](/help/assets/assets/comments-sync2.png)

1. 導航到中的同一連結AEM文檔，選擇文檔並開啟 [!UICONTROL 時間軸] 選項，然後選擇 [!UICONTROL 注釋]。 左側提要欄顯示與 [!DNL Workfront]。

## 資產版本 {#asset-versions}

要維護中的資產版本歷史記AEM錄，請在中配置資產版AEM本。

1. 在Experience Manager中，訪問 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具配置]**，然後開啟 **[!UICONTROL 高級]** 頁籤。

1. 選擇選項 **[!UICONTROL 儲存與現有資產版本同名的資產]**。 選中此選項後，可將上載的資產與現有資產的版本以相同名稱和相同位置儲存。 如果未選中，則將使用其他名稱建立新資產(例如， `asset-name.pdf` 和 `asset-name-1.pdf`)。

1. 選擇選項 **[!UICONTROL 建立新版本時更新資產元資料]**。 選中後，此選項將在建立新版本的資產時更新資產元資料。 如果未選中，資產將保留在建立新版本之前的元資料。

![配置資產版本](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>連結資料夾不支援版本控制。 建立 [!DNL Workfront] 在連結資料夾中使用文檔進行證明時，將刪除有關資產早期版本的注釋和注釋。

## 附加自定義表單 {#attach-custom-forms}

此工作流步驟允許用戶將自定義表單附加到 [!DNL Workfront] 藏物。 此工作流步驟可添加到任何工作流模型。 的 [!DNL Workfront] 此步驟影響的項目將使用有效負載的相對路徑查找。

在Experience Manager的工作流編輯器中，編輯 [!UICONTROL Workfront — 附加自定義窗體] 工作流步驟。

![自定義表單](/help/assets/assets/wf-custom-forms.png)。

## 自動發佈資產 {#auto-publish-assets}

1. 在Experience Manager中，訪問 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Workfront工具配置]**，然後開啟 **[!UICONTROL 高級]** 頁籤。

1. 選擇 **[!UICONTROL 從Workfront發送時自動發佈資產]**。 此選項允許在資產從Workfront發送到時自動發AEM布。 通過指定Workfront自定義表單域及其應設定為的值，可以有條件地啟用此功能。 只要文檔發送到AEM，如果滿足條件，則資產將自動發佈。

1. 選擇 **[!UICONTROL 在項目完成後將所有項目資產發佈到Brand Portal]**。 此選項允許自動將資產發佈到 [!DNL Brand Portal] 當他們所屬的Workfront項目的狀態更改為 `Complete`。

![配置自動發佈](/help/assets/assets/wf-auto-publish-config.png)

## Workfront文檔自定義表單更新 {#subscribe-workfront-doc-custom-form-updates}

訂閱中的更改 [!DNL Workfront] 文檔自定義窗體，選擇 **[!UICONTROL 高級]** 頁籤。 當您訂閱這些更新時，它會更新您映射的 [!DNL Experience Manager] 元資料欄位 [!DNL Workfront] 文檔自定義窗體已更改。

![Workfront文檔自定義表單更新配置 [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
