---
title: 資產選擇器
description: 瞭解如何使用資產選擇器來搜尋、篩選、瀏覽及擷取Adobe Experience Manager Assets中資產的中繼資料。 也會瞭解如何自訂資產選擇器介面。
contentOwner: Adobe
feature: Asset Management,Metadata,Search
role: User
hide: true
exl-id: c84ce84a-1e52-48fd-a16c-38c7769df9af
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 2%

---

# 資產選擇器 {#asset-selector}

>[!NOTE]
>
>此 [資產選擇器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-selector.html?lang=en) 已呼叫 [資產選取器](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) 在舊版中 [!DNL Experience Manager].

資產選擇器可讓您瀏覽、搜尋及篩選中的資產 [!DNL Adobe Experience Manager] 資產。 您也可以擷取使用資產選擇器所選取資產的中繼資料。 若要自訂資產選擇器介面，您可以使用支援的請求引數來啟動它。 這些引數會為特定案例設定資產選擇器的內容。

目前，您可以傳遞請求引數 `assettype` (*影像/影片/文字*)和選取範圍 `mode` (*單一/多個*)做為資產選擇器的內容相關資訊，在整個選取範圍中維持不變。

資產選擇器使用HTML5 **Window.postMessage** 傳送所選資產的資料給收件者的訊息。

資產選擇器是根據Granite的基礎選擇器辭彙。 依預設，資產選擇器會以瀏覽模式運作。 不過，您可以使用Omnisearch體驗套用篩選器，以縮小特定資產的搜尋。

您可以將任何網頁與資產選擇器（無論其是否為CQ容器的一部分）整合`https://[AEM_server]:[port]/aem/assetpicker.html`)。

## 內容引數 {#contextual-parameters}

您可以在URL中傳遞下列請求引數，以啟動特定內容中的資產選擇器：

| 名稱 | 值 | 範例 | 用途 |
|---|---|---|---|
| 資源尾碼(B) | URL中作為資源尾碼的資料夾路徑：`http://localhost:4502/aem/`<br>`assetpicker.html/<folder_path>` | 若要在選取特定資料夾後啟動資產選擇器（例如，使用資料夾） `/content/dam/we-retail/en/activities` 選取時，URL的格式為： `http://localhost:4502/aem/assetpicker.html`<br>`/content/dam/we-retail/en/activities?assettype=images` | 如果您在啟動資產選擇器時要求選擇特定資料夾，請將其作為資源尾碼傳遞。 |
| 模式 | 單一，多個 | `http://localhost:4502/aem/assetpicker.html`<br>`?mode=multiple` <br> `http://localhost:4502/aem/assetpicker.html`<br>`?mode=single` | 在多重模式中，您可以使用資產選擇器同時選取數個資產。 |
| 對話方塊 | true， false | `http://localhost:4502/aem/assetpicker.html`<br>`?dialog=true` | 使用這些引數以Granite對話方塊開啟資產選擇器。 此選項僅適用於透過Granite路徑欄位啟動資產選擇器，並將其設定為pickerSrc URL時。 |
| 根 | `<folder_path>` | `http://localhost:4502/aem/`<br>`assetpicker.html?assettype=images`<br>`&root=/content/dam/we-retail/en/activities` | 使用此選項可指定資產選擇器的根資料夾。 在此情況下，資產選擇器可讓您僅選取根資料夾下的子資產（直接/間接）。 |
| 檢視模式 | 搜尋 |  | 若要在搜尋模式中啟動資產選擇器，請使用assettype和mimetype引數。 |
| assettype (S) | 影像、檔案、多媒體、封存 | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives`</li> | 使用此選項可依據傳遞的值來篩選資產型別。 |
| mimetype | mimetype (`/jcr:content/metadata/dc:format`) （也支援萬用字元） | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=image/png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&?mimetype=*png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=*presentation`</li>  <li>`http://localhost:4502/aem/assetpicker?viewmode=search&mimetype=*presentation&mimetype=*png`</li></ul> | 用它根據MIME型別篩選資產 |

## 使用資產選擇器 {#using-the-asset-selector}

1. 若要存取資產選擇器介面，請前往 `https://[AEM_server]:[port]/aem/assetpicker`.
1. 導覽至所需的資料夾，然後選取一或多個資產。

   ![chlimage_1-441](assets/chlimage_1-441.png)

   或者，您可以從OmniSearch方塊搜尋所需的資產，然後選取它。

   ![chlimage_1-442](assets/chlimage_1-442.png)

   如果您使用OmniSearch方塊來搜尋資產，您可以從 **[!UICONTROL 篩選器]** 窗格以縮小搜尋範圍。

   ![chlimage_1-443](assets/chlimage_1-443.png)

1. 按一下 **[!UICONTROL 選取]** 工具列中的。

>[!MORELIKETHIS]
>
>* [AEMas a Cloud Service中的微前端資產選擇器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-selector.html?lang=en)
