---
title: 將 Dynamic Media 資產新增至頁面
description: 要將Dynamic Media功能添加到您在網站上使用的資產中，您可以直接在頁面上添加Dynamic Media或互動式媒體元件。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: d2ebfca5-19f9-4fa5-b142-b978f46a912f
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 3%

---

# 將 Dynamic Media 資產新增至頁面{#adding-dynamic-media-assets-to-pages}

要將Dynamic Media功能添加到您在網站上使用的資產中，您可以 **[!UICONTROL Dynamic Media]** 或 **[!UICONTROL 互動式媒體]** 元件。 輸入 **[!UICONTROL 設計]** 模式和啟用Dynamic Media元件。 然後，您可以將這些元件新增至頁面，並新增資產至元件。Dynamic Media和互動式媒體元件是智慧的，它們知道您是在添加影像還是視頻，可用選項也會相應更改。

如果將Dynamic Media資產用作WCM，則直接將Adobe Experience Manager資產添加到頁面。

>[!NOTE]
>
>影像地圖可在包裝盒外找到，用於傳送帶條幅。

## 將Dynamic Media元件添加到頁面 {#adding-a-dynamic-media-component-to-a-page}

添加 [!UICONTROL Dynamic Media] 或 [!UICONTROL 互動式媒體] 將元件添加到頁面與將元件添加到任何頁面相同。 的 [!UICONTROL Dynamic Media] 和 [!UICONTROL 互動式媒體] 在以下各節中對元件進行了詳細說明。

要將Dynamic Media元件/查看器添加到頁面：

1. 在Experience Manager中，開啟要添加Dynamic Media元件的頁面。
1. 如果沒有可用的Dynamic Media元件，請在 [!UICONTROL 側腳] 輸入 **[!UICONTROL 設計]** 的子菜單。
1. 選擇 **[!UICONTROL 編輯]** parsys。
1. 選擇 **[!UICONTROL Dynamic Media]** 這樣你就能把Dynamic Media的部件弄到手。

   >[!NOTE]
   >
   >請參閱 [在設計模式下配置元件](/help/sites-authoring/default-components-designmode.md) 的子菜單。

1. 返回到 **[!UICONTROL 編輯]** 中按一下鉛筆表徵圖 [!UICONTROL 側腳]。
1. 拖動 **[!UICONTROL Dynamic Media]** 或 **[!UICONTROL 互動式媒體]** 元件 **[!UICONTROL 其他]** 在副腳上組到所需位置的頁面。
1. 選擇 **[!UICONTROL 編輯]** 這樣，元件就會開啟。
1. [編輯元件](#dynamic-media-component) 必要時。
1. 選擇 **[!UICONTROL 確定]** 這樣您的更改就會保存。

## Dynamic Media元件 {#dynamic-media-components}

[!UICONTROL Dynamic Media] 和 [!UICONTROL 互動式媒體] 在 [!UICONTROL 側腳] 在 **[!UICONTROL Dynamic Media]**。 使用 **[!UICONTROL 互動式媒體]** 用於任何互動式資產（如互動式視頻、互動式影像或旋轉盤集）的元件。 對於所有其他Dynamic Media元件，使用 **[!UICONTROL Dynamic Media]** 元件。

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>預設情況下，這些元件不可用，在使用之前必須在「設計」模式下選取。 [在「設計」模式下使用它們後](/help/sites-authoring/default-components-designmode.md)，可以像添加任何其它Experience Manager元件一樣將元件添加到頁面。

### Dynamic Media分量 {#dynamic-media-component}

Dynamic Media元件是智慧的 — 根據您是添加影像還是添加視頻，您有各種選項。 該元件支援影像預設、基於影像的查看器，如影像集、旋轉集、混合媒體集和視頻。 此外，觀看者是響應的。 即，螢幕大小根據螢幕大小自動更改。 所有查看者都是基於HTML5的查看者。

>[!NOTE]
>
>添加 [!UICONTROL Dynamic Media] 元件和 **[!UICONTROL Dynamic Media設定]** 為空或無法正確添加資產，請檢查以下內容：
>
>* 您 [啟用Dynamic Media](/help/assets/config-dynamic.md)。 Dynamic Media預設為禁用。
>* 影像具有金字塔型tiff檔案。 在啟用Dynamic Media之前導入的影像沒有金字塔tiff檔案。
>


#### 使用影像時 {#when-working-with-images}

的 [!UICONTROL Dynamic Media] 元件用於添加動態映像，包括映像集、旋轉集和混合媒體集。 您可以放大、縮小，如果適用，可以在旋轉集內旋轉影像或從另一類型的集合中選擇影像。

您也可以直接在元件中配置查看器預設、影像預設或影像格式。 要使影像響應，可以設定斷點或應用響應影像預設。

![chlimage_1-72](assets/chlimage_1-72a.png)

可通過按一下以下Dynamic Media設定 **[!UICONTROL 編輯]** ，然後按一下 **[!UICONTROL Dynamic Media設定]** 頁籤。

![chlimage_1-73](assets/chlimage_1-73a.png)

>[!NOTE]
>
>依預設，動態媒體影像元件是可調式的。如果要將其設定為固定大小，請在 **[!UICONTROL 高級]** 頁籤 **[!UICONTROL 寬度]** 和 **[!UICONTROL 高度]** 屬性。

**[!UICONTROL 查看器預設]**  — 從下拉菜單中選擇現有查看器預設。 如果您要查找的查看器預設不可見，則必須使其可見。 請參閱 [管理查看器預設](/help/assets/managing-viewer-presets.md)。 如果使用影像預設，則不能選擇查看器預設，反之，則無法選擇。

僅當查看映像集、旋轉集或混合媒體集時，此選項才可用。 顯示的查看器預設是智慧的。 即，只顯示相關的查看器預設。

**[!UICONTROL 影像預設]**  — 從下拉菜單中選擇現有影像預設。 如果您要查找的影像預設不可見，則必須使其可見。 請參閱 [管理影像預設](/help/assets/managing-image-presets.md)。 如果使用影像預設，則不能選擇查看器預設，反之，則無法選擇。

如果您正在查看映像集、旋轉集或混合媒體集，則此選項不可用。

**[!UICONTROL 影像修飾符]**  — 可以通過提供附加影像命令來更改影像效果。 這些命令在中介紹 [管理影像預設](/help/assets/managing-viewer-presets.md) 和 [命令引用](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html)。

如果您正在查看映像集、旋轉集或混合媒體集，則此選項不可用。

**[!UICONTROL 斷點]**  — 如果在響應站點上使用此資產，則必須添加頁面斷點。 影像斷點由逗號(,)分隔。 當影像預設中沒有定義高度或寬度時，此選項有效。

如果您正在查看映像集、旋轉集或混合媒體集，則此選項不可用。

可以編輯以下內容 [!UICONTROL 高級設定] 按一下 **[!UICONTROL 編輯]** 的子菜單。

**[!UICONTROL 標題]**  — 更改影像的標題。

**[!UICONTROL 替代文字]**  — 為關閉圖形的用戶添加影像標題。

如果您正在查看映像集、旋轉集或混合媒體集，則此選項不可用。

**[!UICONTROL URL，在中開啟]**  — 您可以設定資產，以開啟連結。 設定 **[!UICONTROL URL]** 和 **[!UICONTROL 開啟位置]** 以指示希望在同一窗口或新窗口中開啟它。

如果您正在查看映像集、旋轉集或混合媒體集，則此選項不可用。

**[!UICONTROL 寬度和高度]**  — 如果希望影像為固定大小，請以像素為單位輸入值。 將這些值留空可使資產具有自適應性。

#### 使用視頻時 {#when-working-with-video}

使用 **[!UICONTROL Dynamic Media]** 元件將動態視頻添加到網頁。 編輯元件時，您可以選擇使用預定義的視頻查看器預設在頁面上播放視頻。

![chlimage_1-74](assets/chlimage_1-74a.png)

可以編輯以下內容 [!UICONTROL Dynamic Media設定] 按一下 **[!UICONTROL 編輯]** 的子菜單。

>[!NOTE]
>
>預設情況下，Dynamic Media視頻元件是自適應的。 如果要將其設定為固定大小，請在元件中 **[!UICONTROL 寬度]** 和 **[!UICONTROL 高度]** 的 **[!UICONTROL 高級]** 頁籤。

**[!UICONTROL 查看器預設]**  — 從下拉菜單中選擇現有視頻查看器預設。 如果您要查找的查看器預設不可見，則必須使其可見。 請參閱 [管理查看器預設](/help/assets/managing-viewer-presets.md)。

可以編輯以下內容 [!UICONTROL 高級] 按一下 **[!UICONTROL 編輯]** 的子菜單。

**[!UICONTROL 標題]**  — 更改視頻標題。

**[!UICONTROL 寬度和高度]**  — 如果希望視頻大小固定，請以像素為單位輸入值。 將這些值留空可使其適應。

#### 提供安全視頻 {#how-to-delivery-secure-video}

在Experience Manager6.2中，安裝 [FP-13480](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq620/featurepack/cq-6.2.0-featurepack-13480)，您可以控制是通過安全SSL連接(HTTPS)還是不安全連接(HTTP)傳送視頻。 預設情況下，視頻傳送協定自動從嵌入網頁的協定中繼承。 如果網頁是通過HTTPS載入的，則視頻也是通過HTTPS傳送的。 反之，如果網頁在HTTP上，則視頻通過HTTP傳送。 通常，此預設行為是正常的，無需進行任何配置更改。 但是，您可以覆蓋此預設行為。 追加 `VideoPlayer.ssl=on` 到URL路徑的結尾或嵌入代碼段中其他查看器配置參數的清單。 無論採取哪種行動，都會強制確保視頻傳輸。

有關安全視頻傳輸和使用的詳細資訊 `VideoPlayer.ssl` URL路徑中的配置屬性，請參見 [安全視頻傳送](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-viewer-20-securevideodelivery.html) 的下界。 除視頻查看器外，Mixed Media viewer和Interactive Video viewer還提供安全視頻傳輸。

### 互動式媒體元件 {#interactive-media-component}

互動式媒體元件用於那些具有交互性的資產，例如熱點或影像映射。 如果您有互動式影像、互動式視頻或旋轉木馬橫幅，請使用 **[!UICONTROL 互動式媒體]** 元件。

的 [!UICONTROL 互動式媒體] 元件是智慧的 — 根據您是添加影像還是添加視頻，您有各種選項。 此外，觀看者是響應的。 即，螢幕大小根據螢幕大小自動更改。 所有查看者都是基於HTML5的查看者。

![chlimage_1-75](assets/chlimage_1-75a.png)

可以編輯以下內容 **[!UICONTROL 常規]** 按一下 **[!UICONTROL 編輯]** 的子菜單。

**[!UICONTROL 查看器預設]**  — 從下拉菜單中選擇現有查看器預設。 如果您要查找的查看器預設不可見，則必須使其可見。 必須先發佈查看器預設，然後才能使用它們。 請參閱 [管理查看器預設](/help/assets/managing-viewer-presets.md)。

**[!UICONTROL 標題]**  — 更改視頻標題。

**[!UICONTROL 寬度和高度]**  — 如果希望視頻大小固定，請以像素為單位輸入值。 將這些值留空可使其適應。

可以編輯以下內容 **[!UICONTROL 添加到購物車]** 按一下 **[!UICONTROL 編輯]** 的子菜單。

**[!UICONTROL 顯示產品資產]**  — 預設情況下，此值處於選中狀態。 產品資產顯示在「商務」模組中定義的產品影像。 清除複選標籤以不顯示產品資產。

**[!UICONTROL 顯示產品價格]**  — 預設情況下，此值處於選中狀態。 產品價格顯示在「商務」模組中定義的物料價格。 清除複選標籤以不顯示產品價格。

**[!UICONTROL 顯示產品窗體]**  — 預設情況下，未選擇此值。 「產品表單」包括任何產品變型，如尺寸和顏色。 清除複選標籤以不顯示產品變型。
