---
title: 資產選擇器
description: 瞭解如何使用資產選擇器搜索、篩選、瀏覽和提取Adobe Experience Manager資產內資產的元資料。 還瞭解如何自定義資產選擇器介面。
contentOwner: Adobe
feature: Asset Management,Metadata,Search
role: User
exl-id: 4b518ac0-5b8b-4d61-ac31-269aa1f5abe4
source-git-commit: 0c6c269e9f0cbdcc0c5e3b925ef09b9923cbb2b3
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---

# 資產選擇器 {#asset-selector}

>[!NOTE]
>
>調用了資產選擇器 [資產選取器](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) 以前的版本 [!DNL Experience Manager]。

資產選擇器允許您瀏覽、搜索和篩選中的資產 [!DNL Adobe Experience Manager] 資產。 您還可以使用資產選擇器獲取所選資產的元資料。 要自定義資產選擇器介面，可以使用支援的請求參數啟動它。 這些參數為特定方案設定資產選擇器的上下文。

當前，您可以傳遞請求參數 `assettype` (*影像/視頻/文本*)和選擇 `mode` (*單/多*)作為資產選擇器的上下文資訊，該資訊在整個選擇過程中保持不變。

資產選擇器使用HTML5 **Window.postMessage** 消息，將所選資產的資料發送到收件人。

資產選擇器基於Granite的基金會選取者辭彙。 預設情況下，資產選擇器在瀏覽模式下運行。 但是，您可以使用Omnisearch經驗應用篩選器來優化對特定資產的搜索。

您可以將任何網頁（不管它是否是CQ容器的一部分）與資產選擇器(`https://[AEM_server]:[port]/aem/assetpicker.html`)。

## 上下文參數 {#contextual-parameters}

您可以在URL中傳遞以下請求參數以在特定上下文中啟動資產選擇器：

| 名稱 | 值 | 範例 | 用途 |
|---|---|---|---|
| 資源尾碼(B) | 作為URL中資源尾碼的資料夾路徑：`http://localhost:4502/aem/`<br>`assetpicker.html/<folder_path>` | 在選定特定資料夾（例如資料夾）的情況下啟動資產選擇器 `/content/dam/we-retail/en/activities` 選定，URL應為以下格式： `http://localhost:4502/aem/assetpicker.html`<br>`/content/dam/we-retail/en/activities?assettype=images` | 如果在啟動資產選擇器時需要選擇特定資料夾，請將其作為資源尾碼傳遞。 |
| 模式 | 單個，多個 | `http://localhost:4502/aem/assetpicker.html`<br>`?mode=multiple` <br> `http://localhost:4502/aem/assetpicker.html`<br>`?mode=single` | 在多模式下，您可以使用資產選擇器同時選擇多個資產。 |
| 對話方塊 | 真，假 | `http://localhost:4502/aem/assetpicker.html`<br>`?dialog=true` | 使用這些參數以「花崗岩」對話框的形式開啟資產選擇器。 僅當通過「花崗岩路徑欄位」啟動資產選擇器並將其配置為pickerSrc URL時，此選項才適用。 |
| 根 | `<folder_path>` | `http://localhost:4502/aem/`<br>`assetpicker.html?assettype=images`<br>`&root=/content/dam/we-retail/en/activities` | 使用此選項可指定資產選擇器的根資料夾。 在這種情況下，資產選擇器允許您僅選擇根資料夾下的子資產（直接/間接）。 |
| 視圖模式 | 搜尋 |  | 在搜索模式下使用assettype和mimetype參數啟動資產選擇器。 |
| 集類型(S) | 影像、文檔、多媒體、存檔 | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives`</li> | 使用此選項可根據傳遞的值篩選資產類型。 |
| mimetype | mimetype(s)(`/jcr:content/metadata/dc:format`)（也支援通配符） | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=image/png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&?mimetype=*png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=*presentation`</li>  <li>`http://localhost:4502/aem/assetpicker?viewmode=search&mimetype=*presentation&mimetype=*png`</li></ul> | 使用它根據MIME類型篩選資產 |

## 使用資產選擇器 {#using-the-asset-selector}

1. 要訪問資產選擇器介面，請轉到 `https://[AEM_server]:[port]/aem/assetpicker`。
1. 導航到所需資料夾，然後選擇一個或多個資產。

   ![chlimage_1-441](assets/chlimage_1-441.png)

   或者，可以從OmniSearch框搜索所需資產，然後將其選中。

   ![chlimage_1-442](assets/chlimage_1-442.png)

   如果使用OmniSearch框搜索資產，則可以從 **[!UICONTROL 篩選器]** 的子菜單。

   ![chlimage_1-443](assets/chlimage_1-443.png)

1. 點擊/按一下 **[!UICONTROL 選擇]** 的子菜單。
