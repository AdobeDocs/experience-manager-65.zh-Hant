---
title: 將Dynamic Media Classic(Scene7)功能添加到頁面
description: Adobe Dynamic Media Classic(Scene7)是一個托管解決方案，用於管理、增強、發佈和將富媒體資產提供到Web 、移動、電子郵件和網際網路連接的顯示和打印。
uuid: dc463e2d-a452-490e-88af-f79bdaa3b089
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dc0191d0-f181-4e1e-b3f4-73427aa22073
docset: aem65
exl-id: bc9c864b-8bc3-42b4-ba25-6c5108be4f65
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '3511'
ht-degree: 1%

---

# 將Dynamic Media Classic(Scene7)功能添加到頁面{#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic(Scene7)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) 是一個托管解決方案，用於管理、增強、發佈富媒體資產，並將富媒體資產交付到Web 、移動、電子郵件和網際網路連接的顯示和打印。

您可以通過各種觀看者查看在Dynamic Media Classic(Scene7)發佈的Experience Manager資產：

* 縮放
* 飛出
* 影片
* 影像範本
* 影像

您可以直接將數字資產從Experience Manager發佈到Dynamic Media Classic(Scene7)，也可以將數字資產從Dynamic Media Classic(Scene7)發佈到Experience Manager。

本文檔介紹如何將數字資產從Experience Manager發佈到Dynamic Media Classic(Scene7)，反之亦然。 還對查看者進行了詳細描述。 有關為Dynamic Media Classic(Scene7)配置Experience Manager的資訊，請參見 [Dynamic Media Classic(Scene7)與Experience Manager](/help/sites-administering/scene7.md)。

另請參閱 [添加影像映射](/help/assets/image-maps.md)。

有關使用帶Experience Manager的視頻元件的詳細資訊，請參閱以下內容：

* [影片](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>如果Dynamic Media Classic(Scene7)資產顯示不正確，請確保Dynamic Media [禁用](/help/assets/config-dynamic.md#disabling-dynamic-media) 然後刷新頁面。

## 從資產手動發佈到Dynamic Media Classic(Scene7) {#manually-publishing-to-scene-from-assets}

您可以從經典UI中的「資產」控制台或直接從資產向Dynamic Media Classic(Scene7)發佈數字資產。

>[!NOTE]
>
>Experience Manager非同步發行到Dynamic Media Classic(Scene7)。 選擇後 **[!UICONTROL 發佈]**，您的資產可能需要幾秒鐘才能發佈到Dynamic Media Classic(Scene7)。

### 從Assets控制台發佈 {#publishing-from-the-assets-console}

如果資產位於Dynamic Media Classic(Scene7)目標資料夾中，則可以從「資產」控制台發佈到Scene7。

1. 在Experience Manager經典UI中，選擇 **[!UICONTROL 數字資產]** 訪問數字資產管理器。

1. 從要發佈到Dynamic Media Classic(Scene7)的目標資料夾中選擇資產（或資產）或資料夾，然後按一下右鍵並選擇 **[!UICONTROL 發佈到Dynamic Media Classic(Scene7)]**。 或者，可以選擇 **[!UICONTROL 發佈到Dynamic Media Classic(Scene7)]** 從 **[!UICONTROL 工具]** 的子菜單。

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. 轉到Dynamic Media Classic(Scene7)，確認資產可用。

   >[!NOTE]
   >
   >如果資產不在Dynamic Media Classic(Scene7)同步資料夾中， **[!UICONTROL 發佈到Dynamic Media Classic(Scene7)]** 在兩個菜單中均可見，但已禁用。

### 從資產發佈 {#publishing-from-an-asset}

只要資產位於同步的Dynamic Media Classic(Scene7)資料夾內，您就可以手動發佈該資產。

>[!NOTE]
>
>如果資產不在Dynamic Media Classic(Scene7)同步資料夾中，則指向 **[!UICONTROL 發佈到Dynamic Media Classic(Scene7)]** 中。

要直接從數字資產發佈到Dynamic Media Classic(Scene7)，請執行以下操作：

1. 在Experience Manager中，選擇 **[!UICONTROL 數字資產]** 訪問數字資產管理器。

1. 按兩下以開啟資產。

1. 在資產詳細資訊窗格中，選擇 **[!UICONTROL 發佈到Dynamic Media Classic(Scene7)]**。

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. 連結更改為 **[!UICONTROL 正在發佈……]** 然後 **[!UICONTROL 已發佈]**。 轉到Dynamic Media Classic(Scene7)並確認資產可用。

   >[!NOTE]
   >
   >如果資產未正確發佈到Dynamic Media Classic(Scene7)，則連結將更改為 **[!UICONTROL 發佈失敗]**。 如果資產已發佈到Dynamic Media Classic(Scene7)，則連結為 **[!UICONTROL 重新出版到Dynamic Media Classic(Scene7)]**。 重新發佈允許您在Experience Manager中更改資產並重新發佈它們。

### 從CQ目標資料夾外部發佈資產 {#publishing-assets-from-outside-the-cq-target-folder}

Adobe建議您僅從Dynamic Media Classic(Scene7)目標資料夾中的資產向Dynamic Media Classic(Scene7)發佈資產。 但是，如果必須從目標資料夾外的資料夾上載資產，您仍然可以通過將資產上載到Dynamic Media Classic(Scene7)上的按需資料夾來執行此操作。 首先，為希望資產顯示的頁面配置雲配置。 然後，將一個Dynamic Media Classic(Scene7)元件添加到頁面，並在元件上拖放一個資產。 為該頁設定頁面屬性後， **[!UICONTROL 發佈到Dynamic Media Classic(Scene7)]** 連結，當選定的觸發器上載到Dynamic Media Classic(Scene7)時。

>[!NOTE]
>
>在按需資料夾中的資產不會顯示在Dynamic Media Classic(Scene7)內容瀏覽器中。

**要從CQ目標資料夾外部發佈資產：**

1. 在經典UI中的Experience Manager中，選擇 **[!UICONTROL 網站]** 導航至您要向尚未發佈到Dynamic Media Classic(Scene7)的網頁添加數字資產的網頁。 （適用普通頁繼承規則。）

1. 在旁角中，選擇 **[!UICONTROL 頁面]** 表徵圖 **[!UICONTROL 頁面屬性]**。

1. 選擇 **[!UICONTROL Cloud Services]**。
1. 選擇 **[!UICONTROL 添加服務]**。
1. 選擇 **[!UICONTROL Dynamic Media Classic(Scene7)]**。
1. 在 **[!UICONTROL Adobe Dynamic Media Classic(Scene7)]** 下拉清單，選擇所需的配置，然後選擇 **[!UICONTROL 確定]**。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 在網頁上，將Dynamic Media Classic(Scene7)元件添加到頁面上的所需位置。
1. 從內容查找器，將數字資產拖到元件。 您會看到指向的連結 **[!UICONTROL 查看Dynamic Media Classic(Scene7)出版情況]**。

   >[!NOTE]
   >
   >如果數字資產在CQ目標資料夾中，則沒有指向 **[!UICONTROL 查看Dynamic Media Classic(Scene7)出版情況]** 的子菜單。 資產將置於元件中。

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. 選擇 **[!UICONTROL 查看Dynamic Media Classic(Scene7)出版情況]**。 如果資產未公佈，Experience Manager將資產公佈給Dynamic Media Classic(Scene7)。 上載後，在按需資料夾中找到該資產。 預設情況下，按需資料夾位於 **[!UICONTROL 名稱_of_the_company/CQ5_adhoc]**。 你可以 [根據需要配置按需資料夾](#configuringtheadhocfolder)。

   >[!NOTE]
   >
   >如果資產不在Dynamic Media Classic(Scene7)同步資料夾中，且當前頁面沒有關聯的Dynamic Media Classic(Scene7)雲配置，則上載失敗。

## Dynamic Media Classic(Scene7)元件 {#scene-components}

以下Dynamic Media Classic(Scene7)部件可在Experience Manager提供：

* 縮放
* 浮動（縮放）
* 影像範本
* 影像
* 影片

>[!NOTE]
>
>預設情況下，這些元件不可用，在使用之前必須在「設計」模式下選取。

在「設計」模式下使這些元件可用後，可以像其他任何Experience Manager元件一樣將這些元件添加到頁面中。 尚未發佈到Dynamic Media Classic(Scene7)的資產將發佈到Dynamic Media Classic(Scene7)(如果位於同步資料夾或頁面或Dynamic Media Classic(Scene7)雲配置)。

>[!NOTE]
>
>如果要建立和開發自定義S7查看器並使用Content Finder ，則必須顯式添加 `allowfullscreen` 的下界。

### Flash 檢視器生命週期結束注意事項 {#flash-viewers-end-of-life-notice}

自2017年1月31日起，Adobe Dynamic Media Classic(Scene7)正式結束對Flash觀看平台的支援。

### 將Dynamic Media Classic(Scene7)元件添加到頁面 {#adding-a-scene-component-to-a-page}

將Dynamic Media Classic(Scene7)元件添加到頁面與將元件添加到任何頁面相同。 Dynamic Media Classic(Scene7)各組成部分在以下各節中作了詳細說明。

要將Dynamic Media Classic(Scene7)元件/查看器添加到經典UI中的頁面：

1. 在Experience Manager中，開啟要添加Dynamic Media Classic(Scene7)元件的頁面。

1. 如果沒有可用的Dynamic Media Classic(Scene7)元件，請選擇旁角中的標尺以輸入 **設計** 模式，選擇 **[!UICONTROL 編輯]** parsys，並選擇所有 **[!UICONTROL Dynamic Media Classic(Scene7)]** 元件，使其可用。

1. 返回到 **編輯** 鍵。

1. 從 **[!UICONTROL Dynamic Media Classic(Scene7)]** 在副腳上組到所需位置的頁面。

1. 選擇***[!UICONTROL 編輯]** 以便開啟元件。

1. 根據需要編輯元件並選擇 **[!UICONTROL 確定]** 的子菜單。

### 將互動式觀看體驗添加到響應性網站 {#adding-interactive-viewing-experiences-to-a-responsive-website}

對資產進行響應性設計意味著您的資產會根據其顯示位置進行調整。 通過響應性設計，可以在多個設備上有效地顯示相同的資產。

要向標準UI中的響應站點添加互動式查看體驗，請：

1. 登錄到Experience Manager，並確保 [配置的Adobe Dynamic Media Classic(Scene7)Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) 以及Dynamic Media Classic(Scene7)的部件可用。

   >[!NOTE]
   >
   >如果Dynamic Media Classic(Scene7)WCM元件不可用，請確保通過「設計」模式啟用它們。

1. 在啟用了Dynamic Media Classic(Scene7)元件的網站中，拖動 **[!UICONTROL 影像]** 查看器。
1. 編輯元件並調整 **[!UICONTROL Dynamic Media Classic(Scene7)設定]** 頁籤。

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. 確認查看器正在響應性地調整大小，並且所有交互都針對案頭、平板電腦和移動設備進行了優化。

### 所有Dynamic Media Classic(Scene7)元件的公用設定 {#settings-common-to-all-scene-components}

儘管配置選項各不相同，但以下是所有Dynamic Media Classic(Scene7)元件的通用選項：

* **檔案引用** — 瀏覽到要引用的檔案。 檔案引用顯示資產URL，而不一定是包括URL命令和參數的完整Dynamic Media Classic(Scene7)URL。 不能在此欄位中添加Dynamic Media Classic(Scene7)URL命令和參數。 相反，必須通過元件中的相應功能來添加它們。
* **寬度**  — 用於設定寬度。
* **高度**  — 用於設定高度。

通過開啟（按兩下）Dynamic Media Classic(Scene7)元件(例如，在開啟 **縮放** 元件：

![chlimage_1-52](assets/chlimage_1-52.png)

### 縮放 {#zoom}

按+按鈕時，HTML5縮放元件將顯示更大的影像。

資產底部有縮放工具。 選擇 **[!UICONTROL +]** 放大。 選擇 **[!UICONTROL -]** 減少。 選擇 **[!UICONTROL x]** 或者，重置縮放箭頭會將影像恢復為原來導入的大小。 選擇對角線箭頭，使其全屏。 選擇 **[!UICONTROL 編輯]** 這樣您就可以配置元件。 使用此元件，您可以 [所有Dynamic Media Classic(Scene7)元件的公用設定](#settings-common-to-all-scene-components)。

![](do-not-localize/chlimage_1-3.png)

### 飛出 {#flyout}

在HTML5浮出元件中，資產顯示為分割螢幕；將資產保留在指定的規模；右側顯示縮放部分。 選擇 **[!UICONTROL 編輯]** 這樣您就可以配置元件。 使用此元件，您可以 [所有Dynamic Media Classic(Scene7)元件的公用設定](/help/sites-administering/scene7.md#settingscommontoallscene7components)。

>[!NOTE]
>
>如果「浮出」元件使用自定義大小，則使用該自定義大小，並禁用元件的響應設定。
>
>如果「浮出」(Flyout)元件使用預設大小（如「設計」視圖中設定），則使用預設大小。 該元件延伸以在啟用元件的響應設定的情況下適應頁面佈局大小。 但是，請注意，對元件的響應設定存在限制。 使用帶有響應設定的浮出元件時，不應將其用於全頁延伸。 否則，浮出窗口可能會超出頁面的右邊框。

![chlimage_1-53](assets/chlimage_1-53.png)

### 影像 {#image}

Dynamic Media Classic(Scene7)影像元件允許您向影像添加Dynamic Media Classic(Scene7)功能，如Dynamic Media Classic(Scene7)修飾符、影像或查看器預設和銳化。 Dynamic Media Classic(Scene7)影像元件與Experience Manager中具有特殊Dynamic Media Classic(Scene7)功能的其他影像元件類似。 在此示例中，影像具有Dynamic Media Classic(Scene7)URL修飾符， `&op_invert=1` 。

![](do-not-localize/chlimage_1-4.png)

**標題，替代文字**  — 在「高級」頁籤中，為圖形關閉的用戶添加標題和替代文字。

**URL，在中開啟**  — 您可以設定資產，以開啟連結。 設定URL，在「開啟」(Open)中，指明希望在同一窗口或新窗口中開啟它。

![chlimage_1-54](assets/chlimage_1-54.png)

**查看器預設**  — 從下拉菜單中選擇現有查看器預設。 如果您要查找的查看器預設不可見，則必須使其可見。 請參閱管理查看器預設。 如果使用影像預設，則不能選擇查看器預設，反之，則無法選擇。

**Dynamic Media Classic(Scene7)配置**  — 選擇要用於從SPS中提取活動影像預設的Dynamic Media Classic(Scene7)配置。

**影像預設**  — 從下拉菜單中選擇現有影像預設。 如果您要查找的影像預設不可見，則必須使其可見。 請參閱管理影像預設。 如果使用影像預設，則不能選擇查看器預設，反之，則無法選擇。

**輸出格式**  — 選擇影像的輸出格式，例如jpeg。 根據您選擇的輸出格式，您可能還有其他配置選項。 請參閱映像預設最佳實踐。

**銳化**  — 選擇銳化影像的方式。 銳化在「影像預設最佳實踐」和「銳化最佳實踐」中進行了詳細說明。

**URL修飾符**  — 您可以通過提供附加的S7影像命令來更改影像效果。 這些命令在「影像預設」和「命令」參考中介紹。

**斷點**  — 如果網站響應，則要調整斷點。 斷點必須用逗號(,)分隔。

### 影像範本 {#image-template}

Dynamic Media Classic(Scene7)影像模板是分層的Photoshop內容，導入到Dynamic Media Classic(Scene7)，內容和屬性在此參數化，以便於變化。 的 **[!UICONTROL 影像模板]** 元件允許導入影像並動態更改Experience Manager中的文本。 此外，您還可以 **[!UICONTROL 影像模板]** 元件使用客戶端上下文中的值，以便每個用戶以個性化的方式體驗影像。

選擇 **[!UICONTROL 編輯]**  — 配置元件。 您可以配置 [所有Dynamic Media Classic(Scene7)元件的公用設定](/help/sites-administering/scene7.md#settingscommontoallscene7components) 以及本節中介紹的其他設定。

![chlimage_1-55](assets/chlimage_1-55.png)

**檔案引用、寬度、高度**  — 請參閱 [所有Dynamic Media Classic(Scene7)元件的公用設定](/help/sites-administering/scene7.md#settingscommontoallscene7components)。

>[!NOTE]
>
>Dynamic Media Classic(Scene7)URL命令和參數不能直接添加到檔案引用URL。 它們只能在元件UI中定義 **[!UICONTROL 參數]** 的子菜單。

**標題，替代文字**  — 在「Dynamic Media Classic(Scene7)影像模板」頁籤中，為已關閉圖形的用戶添加影像標題和替代文字。

**URL，在中開啟**  — 您可以設定資產，以開啟連結。 設定URL，在「開啟」(Open)中，指明希望在同一窗口或新窗口中開啟它。

![chlimage_1-56](assets/chlimage_1-56.png)

**參數面板**  — 導入映像時，參數會預先填充映像中的資訊。 如果沒有可動態更改的內容，則此窗口為空。

![chlimage_1-57](assets/chlimage_1-57.png)

#### 動態更改文本 {#changing-text-dynamically}

要動態更改文本，請在欄位中輸入新文本，然後選擇 **[!UICONTROL 確定]**。 在此示例中， **價格** 現在是50美元，運費是99美分。

![chlimage_1-58](assets/chlimage_1-58.png)

影像中的文本將更改。 通過選擇 **[!UICONTROL 重置]** 的子菜單。

![chlimage_1-59](assets/chlimage_1-59.png)

#### 更改文本以反映客戶端上下文值的值 {#changing-text-to-reflect-the-value-of-a-client-context-value}

要將欄位連結到客戶端上下文值，請選擇 **[!UICONTROL 選擇]** 要開啟客戶端上下文菜單，請選擇客戶端上下文，然後選擇 **[!UICONTROL 確定]**。 在本示例中，名稱會根據將「名稱」與配置檔案中的格式化名稱連結而更改。

![chlimage_1-60](assets/chlimage_1-60.png)

文本反映當前登錄用戶的名稱。 通過選擇 **[!UICONTROL 重置]** 的子菜單。

![chlimage_1-61](assets/chlimage_1-61.png)

#### 使Dynamic Media Classic(Scene7)影像模板成為連結 {#making-the-scene-image-template-a-link}

您可以將Dynamic Media Classic(Scene7)影像模板元件設定為可點擊連結。

1. 在帶有Dynamic Media Classic(Scene7)影像模板元件的頁面上，選擇 **[!UICONTROL 編輯]**。
1. 在 **[!UICONTROL URL]** 欄位，輸入按一下影像時用戶轉到的URL。 在 **[!UICONTROL 開啟位置]** 欄位中，選擇是否要開啟目標（新窗口或同一窗口）。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 選擇 **[!UICONTROL 確定]**。

### 視頻元件 {#video-component}

Dynamic Media Classic(Scene7) **[!UICONTROL 視頻]** 元件(可從側腳的Dynamic Media Classic(Scene7)部分獲得)使用設備和頻寬檢測為每個螢幕提供正確的視頻。 該元件是HTML5視頻播放器；它是一個可以跨頻道使用的查看器。

它可用於自適應視頻集、單個MP4視頻或單個F4V視頻。

請參閱 [視頻](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md) 有關視頻如何與Dynamic Media Classic(Scene7)整合協作的詳細資訊。 此外，請參見 [這樣 **Dynamic Media Classic(Scene7)視頻** 元件與基礎的比較 **視頻** 元件](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)。

![chlimage_1-63](assets/chlimage_1-63.png)

### 視頻元件的已知限制 {#known-limitations-for-the-video-component}

AdobeDAM和WCM顯示是否上載主源視頻。 它們不顯示這些代理資產：

* Dynamic Media Classic(Scene7)編碼格式副本
* Dynamic Media Classic(Scene7)自適應視頻集

使用帶有Dynamic Media Classic(Scene7)視頻元件的自適應視頻集時，必須調整該元件的大小以適合視頻的尺寸。

## Dynamic Media Classic(Scene7)內容瀏覽器 {#scene-content-browser}

使用Dynamic Media Classic(Scene7)內容瀏覽器，您可以直接以Experience Manager查看來自Dynamic Media Classic(Scene7)的內容。 要訪問內容瀏覽器，請在Content Finder中，選擇 **Dynamic Media Classic(Scene7)** 在觸控優化用戶介面或 **S7** 表徵圖。 兩個用戶介面的功能完全相同。

如果您有多個配置，預設情況下Experience Manager將顯示 [預設配置](/help/sites-administering/scene7.md#configuring-a-default-configuration)。 您可以直接在Dynamic Media Classic(Scene7)內容瀏覽器的下拉菜單中選擇不同的配置。

>[!NOTE]
>
>* 按需資料夾中的資產不顯示在Dynamic Media Classic(Scene7)內容瀏覽器中。
>* 當 [已啟用安全預覽](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)，在Dynamic Media Classic(Scene7)上已發佈和未發佈的資產都會在Dynamic Media Classic(Scene7)內容瀏覽器中出現。
>* 如果你看不到 **[!UICONTROL Dynamic Media Classic(Scene7)]** 或 **[!UICONTROL S7]** 表徵圖作為內容瀏覽器中的選項，您必須 [配置Dynamic Media Classic(Scene7)與Experience Manager合作](/help/sites-administering/scene7.md)。
>* 對於視頻，Dynamic Media Classic(Scene7)內容瀏覽器支援：
   >   * 自適應視頻集：容器，用於跨多個螢幕無縫播放所需的所有視頻格式副本
   >   * 單個MP4視頻
   >   * 單個F4V視頻


### 瀏覽內容 {#browsing-content-in-the-classic-ui}

通過選擇以下選項瀏覽Dynamic Media Classic(Scene7)中的內容： **[!UICONTROL S7]** 頁籤。

通過選擇配置，可以更改正在訪問的配置。 資料夾會根據您選擇的配置而更改。

![chlimage_1-64](assets/chlimage_1-64.png)

與Assets的內容查找器一樣，您可以搜索資產並篩選結果。 但是，與Assets finder不同，在 **S7** 頁籤，檔案名 **開頭** 輸入的字串，而不是 **含** 檔案名中的關鍵字。

預設情況下，資產按檔案名顯示。 但是，您也可以按資產類型篩選結果。

>[!NOTE]
>
>對於視頻，WCM的Dynamic Media Classic(Scene7)內容瀏覽器支援：
>
>* 自適應視頻集：容器，用於跨多個螢幕無縫播放所需的所有視頻格式副本
>* 單個MP4視頻
>* 單個F4V視頻
>


### 使用內容瀏覽器搜索Dynamic Media Classic(Scene7)資產 {#searching-for-scene-assets-with-the-content-browser}

搜索Dynamic Media Classic(Scene7)資產與搜索Experience Manager資產類似。 例外是，在搜索時，您實際看到的是Dynamic Media Classic(Scene7)系統中資產的遠程視圖，而不是直接將它們導入Experience Manager。

您可以使用經典UI或觸控優化UI來查看和搜索資產。 根據介面的不同，搜索方式稍有不同。

在任一UI中搜索時，可以按以下條件進行篩選（如觸控優化UI中所示）:

**輸入關鍵字**  — 您可以按名稱搜索資產。 搜索關鍵字時，輸入的是檔案名的開頭。 例如，鍵入單詞&quot;swimming&quot;將查找以這些字母開頭的所有資產檔案名。 鍵入要查找資產的術語後，請務必選擇「輸入」。

![chlimage_1-65](assets/chlimage_1-65.png)

**資料夾/路徑**  — 資料夾的名稱基於您選擇的配置。 通過選擇資料夾表徵圖並選擇子資料夾，然後選擇複選標籤以選擇它，可以細化到較低級別。

如果輸入關鍵字並選擇資料夾，則Experience Manager將搜索該資料夾和任何子資料夾。 但是，如果在搜索時未輸入任何關鍵字，則選擇資料夾只會顯示該資料夾中的資產，並且不包括任何子資料夾。

預設情況下，Experience Manager會搜索選定的資料夾和所有子資料夾。

![chlimage_1-66](assets/chlimage_1-66.png)

**資產類型**  — 選擇Dynamic Media Classic(Scene7)瀏覽Dynamic Media Classic(Scene7)內容。 僅當配置了Dynamic Media Classic(Scene7)時，此選項才可用。

![chlimage_1-67](assets/chlimage_1-67.png)

**配置**  — 如果您在Cloud Services中定義了多個Dynamic Media Classic(Scene7)配置，則可以在此處選擇它。 因此，資料夾會根據您選擇的配置進行更改。

![chlimage_1-68](assets/chlimage_1-68.png)

**資產類型**  — 在Dynamic Media Classic(Scene7)瀏覽器中，您可以篩選結果以包括以下任何內容：影像、模板、視頻和自適應視頻集。 如果未選擇任何資產類型，則預設Experience Manager會搜索所有資產類型。

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* 在經典UI中，您還可以搜索 **Flash** 和 **FXG**。 不支援在觸控優化用戶介面中過濾這兩個術語。
>
>* 搜索視頻時，您正在搜索單個格式副本。 結果返回原始格式副本(僅 &#42;.mp4)和編碼格式副本。
>* 搜索自適應視頻集時，您正在搜索資料夾和所有子資料夾，但前提是您向搜索中添加了關鍵字。 如果未添加關鍵字，則Experience Manager不會搜索子資料夾。
>


**發佈狀態**  — 您可以根據發佈狀態篩選資產：未發佈或已發佈。 如果未選擇任何「發佈狀態」，則預設情況下Experience Manager會搜索所有發佈狀態。

![chlimage_1-70](assets/chlimage_1-70.png)
