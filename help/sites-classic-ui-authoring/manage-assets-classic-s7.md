---
title: 將Scene7功能新增至您的頁面
seo-title: 將Scene7功能新增至您的頁面
description: Adobe Scene7是代管解決方案，可用來管理、增強、發佈和提供多媒體資產至網路、行動裝置、電子郵件和網際網路連線的顯示器與印刷品。
seo-description: Adobe Scene7是代管解決方案，可用來管理、增強、發佈和提供多媒體資產至網路、行動裝置、電子郵件和網際網路連線的顯示器與印刷品。
uuid: dc463e2d-a452-490e-88af-f79bdaa3b089
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dc0191d0-f181-4e1e-b3f4-73427aa22073
docset: aem65
translation-type: tm+mt
source-git-commit: 81707b4d57f7f15106459b91f95b1bc6ec333bf4
workflow-type: tm+mt
source-wordcount: '3221'
ht-degree: 0%

---


# 將Scene7功能新增至您的頁面{#adding-scene-features-to-your-page}

[Adobe Scene7是](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) 一套代管解決方案，可管理、增強、發佈和提供多媒體資產至網路、行動裝置、電子郵件和網際網路連線的顯示和列印。

您可以在各種檢視器中檢視發佈於Scene7的AEM資產：

* 縮放
* 飛出
* 影片
* 影像範本
* 影像

您可以直接從AEM發佈數位資產至Scene7，也可以從Scene7發佈數位資產至AEM。

本檔案說明如何將數位資產從AEM發佈至Scene7，反之亦然。 檢視器也會有詳細說明。 如需設定Scene7適用的AEM的詳細資訊，請參閱[整合Scene7與AEM](/help/sites-administering/scene7.md)。

另請參閱[添加映像映射](/help/assets/image-maps.md)。

如需搭配AEM使用視訊元件的詳細資訊，請參閱下列：

* [影片](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>如果Scene7資產未正確顯示，請確定動態媒體已停用[，然後重新整理頁面。](/help/assets/config-dynamic.md#disabling-dynamic-media)

## 從資產{#manually-publishing-to-scene-from-assets}手動發佈至Scene7

您可以從傳統UI的「資產」主控台或直接從資產發佈數位資產至Scene7。

>[!NOTE]
>
>AEM以非同步方式發佈至Scene7。 按一下&#x200B;**Publish**&#x200B;後，您的資產可能需要數秒鐘才能發佈至Scene7。


### 從Assets主控台{#publishing-from-the-assets-console}發佈

若要在資產位於Scene7目標資料夾時，從「資產」主控台發佈至Scene7:

1. 在AEM傳統UI中，按一下「數位資產」**以存取數位資產管理員。**

1. 從您要發佈至Scene7的目標資料夾中選取資產（或資產）或資料夾，然後按一下滑鼠右鍵，然後選取「發佈至Scene7」**。**&#x200B;或者，您也可以從&#x200B;**工具選單**&#x200B;選擇「發佈至Scene7 **」。**

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. 前往Scene7並確認資產已可用。

   >[!NOTE]
   >
   >如果資產不在Scene7同步化資料夾中，則兩個功能表中的「發佈至Scene7 **」都會顯示，但會停用。**

### 從資產{#publishing-from-an-asset}發佈

只要資產位於同步的Scene7資料夾內，您就可以手動發佈資產。

>[!NOTE]
>
>如果資產未位於Scene7同步化資料夾中，將不會顯示「發佈至Scene7 **」的連結。**

若要直接從數位資產發佈至Scene7:

1. 在AEM中，按一下「數位資產」**以存取數位資產管理員。**

1. 按兩下以開啟資產。

1. 在資產詳細資訊窗格中，選取「發佈至Scene7 **」。**

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. 連結會變更為「發佈……」**，然後** Published **。**&#x200B;前往Scene7並確認資產可用。

   >[!NOTE]
   >
   >如果資產未正確發佈至Scene7，連結會變更為&#x200B;**Publishing Failed**。 如果資產已發佈至Scene7，連結會顯示「重新發佈至Scene7」**。**&#x200B;重新發佈可讓您在AEM中變更資產，然後重新發佈。

### 從CQ Target資料夾{#publishing-assets-from-outside-the-cq-target-folder}外部發佈資產

Adobe建議您僅從Scene7目標資料夾中的資產，將資產發佈至Scene7。 不過，如果您需要從目標資料夾外的資料夾上傳資產，您仍可將資產上傳至Scene7的&#x200B;**ad-hoc**&#x200B;資料夾，以完成此作業。

若要這麼做，請先設定資產將出現之頁面的雲端設定。 然後，您將Scene7元件新增至頁面，並在元件上拖放資產。 為該頁面設定頁面屬性後，當選取的觸發器上傳至Scene7時，會顯示&#x200B;**發佈至Scene7**&#x200B;連結。

>[!NOTE]
>
>臨機資料夾中的資產不會顯示在Scene7內容瀏覽器中。

要發佈駐留在CQ目標資料夾以外的資產：

1. 在傳統UI的AEM中，按一下「**網站**」，並導覽至您要新增數位資產至尚未發佈至Scene7的網頁。 （套用一般頁面繼承規則）。

1. 在sidekick中，按一下&#x200B;**Page**&#x200B;圖示，然後按一下&#x200B;**Page Properties**。

1. 按一下「**雲端服務**」，然後按一下「新增服務&#x200B;**」，然後選取「** Scene7 **」。**
1. 在&#x200B;**Adobe Scene7**&#x200B;下拉式清單中，選取所要的設定，然後按一下&#x200B;**確定**。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 在網頁上，將Scene7元件新增至頁面上所需的位置。
1. 從內容搜尋器，將數位資產拖曳至元件。 您會看到&#x200B;**檢查Scene7出版物狀態**&#x200B;的連結。

   >[!NOTE]
   >
   >如果數位資產位於CQ目標資料夾中，則不會顯示「檢查Scene7出版物狀態&#x200B;**」的連結。**&#x200B;資產只會放在元件中。

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. 按一下「檢查Scene7出版物狀態&#x200B;**」。**&#x200B;如果資產未發佈，AEM會將資產發佈至Scene7。 上傳資產後，資產就會位於臨機資料夾中。 依預設，臨機資料夾位於&#x200B;**name_of_the_company/CQ5_adhoc**&#x200B;中。 如果需要，您可以[配置此選項。](#configuringtheadhocfolder)

   >[!NOTE]
   >
   >如果資產不在Scene7同步化資料夾中，且目前頁面沒有關聯的Scene7雲端設定，上傳將會失敗。

## Scene7元件{#scene-components}

AEM提供下列Scene7元件：

* 縮放
* 彈出（縮放）
* 影像範本
* 影像
* 影片

>[!NOTE]
>
>這些元件預設不可用，在使用之前必須在設計模式中選取。

在「設計」模式中提供元件後，您就可以像其他AEM元件一樣，將元件新增至您的頁面。 尚未發佈至Scene7的資產會發佈至Scene7（如果位於同步化資料夾、頁面或Scene7雲端設定）。

>[!NOTE]
>
>如果您正在建立和開發自訂的S7檢視器，並使用內容搜尋器，則需要明確新增&#x200B;**allowfullscreen**&#x200B;參數。

### Flash 檢視器生命週期結束注意事項 {#flash-viewers-end-of-life-notice}

自2017年1月31日起，Adobe Scene7將正式終止對Flash檢視器平台的支援。

如需此重要變更的詳細資訊，請參閱[Flash Viewer生命週期結束常見問答集](https://docs.adobe.com/content/docs/en/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html)。

### 將Scene7元件新增至頁面{#adding-a-scene-component-to-a-page}

將Scene7元件新增至頁面與將元件新增至任何頁面相同。 Scene7元件在下列章節中有詳細說明。

若要將Scene7元件／檢視器新增至傳統UI中的頁面：

1. 在AEM中，開啟您要新增Scene7元件的頁面。

1. 如果沒有可用的Scene7元件，請按一下側點中的尺標以進入&#x200B;**Design**&#x200B;模式，按一下「編輯&#x200B;**parsys」，然後選取所有** Scene7 **元件以使其可用。**

1. 按一下側鍵中的鉛筆，返回&#x200B;**編輯**&#x200B;模式。

1. 從側腳中的&#x200B;**Scene7**&#x200B;群組拖曳元件至所需位置的頁面。

1. 按一下&#x200B;**編輯**&#x200B;以開啟元件。

1. 根據需要編輯元件，然後按一下&#x200B;**OK**&#x200B;保存更改。

### 將互動式檢視體驗新增至互動式網站{#adding-interactive-viewing-experiences-to-a-responsive-website}

針對您的資產進行多方互動設計，表示您的資產會依其顯示位置而調整。 透過多方互動設計，可在多種裝置上有效顯示相同的資產。

若要在傳統UI中將互動式檢視體驗新增至互動式網站：

1. 登入AEM，並確定您已設定[ Adobe Scene7 Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration)，且Scene7元件已可供使用。

   >[!NOTE]
   >
   >如果Scene7 WCM元件不可用，請務必透過設計模式加以啟用。

1. 在啟用Scene7元件的網站中，將&#x200B;**Image**&#x200B;檢視器拖曳至頁面。
1. 在&#x200B;**Scene7 Settings**&#x200B;標籤中編輯元件並調整中斷點。

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. 確認檢視器正在回應性地調整大小，而且所有互動都已針對桌上型電腦、平板電腦和行動裝置最佳化。

### 所有Scene7元件的常用設定{#settings-common-to-all-scene-components}

雖然設定選項不同，但下列是所有Scene7元件的常見選項：

* **檔案引用**-瀏覽到要引用的檔案。檔案參考會顯示資產URL，但不一定是完整的Scene7 URL，包括URL命令和參數。 您無法在此欄位中新增Scene7 URL命令和參數。 它們必須透過元件中的對應功能來新增。
* **寬度** -可讓您設定寬度。
* **高度** -可讓您設定高度。

您可以開啟（連按兩下）Scene7元件，例如開啟&#x200B;**Zoom**&#x200B;元件時，設定這些設定選項：

![chlimage_1-52](assets/chlimage_1-52.png)

### 縮放 {#zoom}

當您按+按鈕時，HTML5縮放元件會顯示較大的影像。

資產底部有縮放工具。 按一下&#x200B;**+**&#x200B;放大。 按一下&#x200B;**-**&#x200B;以減少。 按一下&#x200B;**x**&#x200B;或重設縮放箭頭，將影像重新調回原本匯入的大小。 按一下對角線箭頭，讓它成為全螢幕。 按一下&#x200B;**編輯**&#x200B;配置元件。 使用此元件，您可以設定所有Scene7元件](#settings-common-to-all-scene-components)的共同設定。[

![](do-not-localize/chlimage_1-3.png)

### 彈出{#flyout}

在HTML5 Flyout元件中，資產顯示為分割畫面；將資產保留在指定的大小；右側顯示縮放部分。 按一下&#x200B;**編輯**&#x200B;配置元件。 使用此元件，您可以設定所有Scene7元件](/help/sites-administering/scene7.md#settingscommontoallscene7components)的共同設定。[

>[!NOTE]
>
>如果您的Flyout元件使用自訂大小，則會使用該自訂大小，並停用元件的回應式設定。
>
>如果您的Flyout元件使用預設大小（如設計檢視中所設定），則會使用預設大小，而元件會延伸以配合頁面版面大小，並啟用元件的回應式設定。 但請注意，元件的回應式設定有限。 當您使用具有自適應設定的彈出式元件時，不應將它用於全頁延伸。 否則，彈出(Flyout)可能會超出頁面的右邊框。

![chlimage_1-53](assets/chlimage_1-53.png)

### 影像 {#image}

Scene7 Image元件可讓您將Scene7功能新增至影像，例如Scene7修飾元、影像或檢視器預設集，以及銳利化。 Scene7影像元件類似於AEM中具有特殊Scene7功能的其他影像元件。 在此範例中，影像已套用Scene7 URL修飾元&#x200B;**&amp;op_invert=1**。

![](do-not-localize/chlimage_1-4.png)

**標題、替代文** 字在「進階」索引標籤中，為影像新增標題，並為關閉圖形的使用者新增替代文字。

**URL, Open** inYou can set a sasset from to open a link.設定URL，並在「開啟於」中指出您要在相同視窗或新視窗中開啟它。

![chlimage_1-54](assets/chlimage_1-54.png)

**檢視** 器預設從下拉式選單中選取現有的檢視器預設。如果您所尋找的檢視器預設集不可見，您可能需要將它顯示。 請參閱管理檢視器預設集。 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

**Scene7** 設定選取您要用來從SPS擷取作用中影像預設集的Scene7設定。

**影像** 預設集從下拉式選單中選取現有的影像預設集。如果您要尋找的影像預設集不可見，您可能需要將它顯示。 請參閱管理影像預設集。 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

**輸出** 格式選擇影像的輸出格式，例如jpeg。視您選擇的輸出格式而定，您可能會有其他設定選項。 請參閱影像預設集最佳範例。

**銳** 利化選取影像銳利化的方式。銳利化會在影像預設集最佳實務和銳利化最佳實務中詳細說明。

**URL修** 飾元您可以提供額外的S7影像指令來變更影像效果。這些在「影像預設集」和「命令」參考中有說明。

**中斷** 點如果您的網站是互動式的，您需要調整中斷點。中斷點必須以逗號(,)分隔。

### 影像範本 {#image-template}

[Scene7 Image ](https://help.adobe.com/en_US/scene7/using/WS60B68844-9054-4099-BF69-3DC998A04D3C.html) Template是分層的Photoshop內容，已匯入Scene7，內容和屬性會因可變性而參數化。**Image template**&#x200B;元件可讓您在AEM中匯入影像並動態變更文字。 此外，您還可以設定&#x200B;**影像範本**&#x200B;元件，使用用戶端內容的值，讓每位使用者以個人化方式體驗影像。

按一下&#x200B;**編輯**&#x200B;配置元件。 您可以設定所有Scene7元件的共用[設定，以及本節所述的其他設定。](/help/sites-administering/scene7.md#settingscommontoallscene7components)

![chlimage_1-55](assets/chlimage_1-55.png)

**檔案參考、寬度、高** 度檢視所有Scene7元件的常用設定。

>[!NOTE]
>
>Scene7 URL命令和參數無法直接新增至「檔案參考URL」。 它們只能在&#x200B;**參數**&#x200B;面板中的元件UI中定義。

**標題、替代文** 字在「Scene7影像範本」索引標籤中，為影像新增標題，並為關閉圖形的使用者新增替代文字。

**URL, Open** inYou can set a sasset from to open a link.設定URL，並在「開啟於」中指出您要在相同視窗或新視窗中開啟它。

![chlimage_1-56](assets/chlimage_1-56.png)

**參數** 面板匯入影像時，會預先填入影像的資訊。如果沒有可動態變更的內容，則此視窗為空。

![chlimage_1-57](assets/chlimage_1-57.png)

#### 動態變更文字{#changing-text-dynamically}

要動態更改文本，請在欄位中輸入新文本，然後按一下&#x200B;**確定**。 在此範例中，**Price**&#x200B;現在是$50，而運費是99美分。

![chlimage_1-58](assets/chlimage_1-58.png)

影像中的文字會變更。 您可以按一下欄位旁的&#x200B;**Reset**，將文字重設回原始值。

![chlimage_1-59](assets/chlimage_1-59.png)

#### 變更文字以反映用戶端內容值{#changing-text-to-reflect-the-value-of-a-client-context-value}的值

若要將欄位連結至用戶端內容值，請按一下「選擇&#x200B;****」以開啟用戶端內容功能表，選取用戶端內容，然後按一下「確定」。 ****&#x200B;在此示例中，名稱會根據將名稱與配置檔案中的格式化名稱連結而改變。

![chlimage_1-60](assets/chlimage_1-60.png)

文字會反映目前登入使用者的名稱。 您可以按一下欄位旁的&#x200B;**Reset**，將文字重設回原始值。

![chlimage_1-61](assets/chlimage_1-61.png)

#### 將Scene7影像範本設為連結{#making-the-scene-image-template-a-link}

若要讓Scene7影像範本元件成為可點按的連結：

1. 在具有Scene7影像範本元件的頁面上，按一下「編輯」**。**
1. 在&#x200B;**URL**&#x200B;欄位中，輸入使用者在點按影像時所前往的URL。 在&#x200B;**在**&#x200B;欄位中開啟，選取您要開啟目標（新視窗或相同視窗）。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 按一下&#x200B;**「確定」**。

### 視訊元件{#video-component}

Scene7 **Video**&#x200B;元件（可從側腳的Scene7區段取得）會使用裝置和頻寬偵測，為每個畫面提供正確的視訊。 此元件為HTML5視訊播放器；它是可跨通道使用的單一檢視器。

它可用於最適化視訊集、單一MP4視訊或單一F4V視訊。

如需視訊如何與Scene7整合運作的詳細資訊，請參閱[Video](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)。 此外，查看&#x200B;**Scene7視訊**&#x200B;元件與基礎&#x200B;**視訊**&#x200B;元件](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)的比較。[

![chlimage_1-63](assets/chlimage_1-63.png)

### 視訊元件{#known-limitations-for-the-video-component}的已知限制

Adobe DAM和WCM會顯示是否上傳主要來源視訊。 它們不會顯示下列代理資產：

* Scene7編碼轉譯
* Scene7可調式視訊集

當搭配Scene7視訊元件使用最適化視訊集時，元件需要調整大小以符合視訊的尺寸。

## Scene7內容瀏覽器{#scene-content-browser}

Scene7內容瀏覽器可讓您直接在AEM中檢視Scene7的內容。 若要存取內容瀏覽器，請在「內容搜尋器」中，選取觸控最佳化使用者介面中的&#x200B;**Scene7**，或是傳統使用者介面中的&#x200B;**S7**&#x200B;圖示。 這兩個使用者介面的功能完全相同。

如果您有多個設定，AEM依預設會顯示[預設設定](/help/sites-administering/scene7.md#configuring-a-default-configuration)。 您可以直接在Scene7內容瀏覽器中的下拉式選單中選取不同的設定。

>[!NOTE]
>
>* 位於臨機資料夾的資產不會出現在Scene7內容瀏覽器中。
>* 當[啟用「保全預覽」](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)時，Scene7上已發佈和未發佈的資產都會出現在Scene7內容瀏覽器中。
>* 如果您在內容瀏覽器中未將&#x200B;**Scene7**&#x200B;或&#x200B;**S7**&#x200B;圖示視為選項，您需要[設定Scene7以搭配AEM](/help/sites-administering/scene7.md)運作。
>* 對於視訊，Scene7內容瀏覽器支援：
   >   * 最適化視訊集：容器，以便在多個螢幕上順暢播放所需的所有視訊轉譯
   >   * 單一MP4視訊
   >   * 單一F4V視訊


### 瀏覽內容{#browsing-content-in-the-classic-ui}

按一下&#x200B;**S7**&#x200B;標籤，瀏覽Scene7中的內容。

通過選擇配置，可以更改要訪問的配置。資料夾會根據您選擇的配置而更改。

![chlimage_1-64](assets/chlimage_1-64.png)

和資產的內容搜尋器一樣，您可以搜尋資產並篩選結果。 但是，與Assets finder不同，在&#x200B;**S7**&#x200B;標籤中輸入關鍵字時，檔案名稱&#x200B;**以您輸入的字串**&#x200B;開頭，而不是以檔案名稱中包含&#x200B;**關鍵字的**&#x200B;開頭。

依預設，資產會依檔案名稱顯示。 您也可以依資產類型篩選結果。

>[!NOTE]
>
>對於視訊，WCM的Scene7內容瀏覽器支援：
>
>* 最適化視訊集：容器，以便在多個螢幕上順暢播放所需的所有視訊轉譯
>* 單一MP4視訊
>* 單一F4V視訊

>



### 使用內容瀏覽器{#searching-for-scene-assets-with-the-content-browser}搜尋Scene7資產

搜尋Scene7資產與搜尋AEM資產類似，但搜尋時，您實際看到的是Scene7系統中資產的遠端檢視，而非直接將資產匯入AEM。

您可以使用傳統UI或觸控最佳化UI來檢視和搜尋資產。 視介面而定，您的搜尋方式略有不同。

在任一UI中搜尋時，您可依下列條件進行篩選（如觸控最佳化UI中所示）:

**輸入關** 鍵字您可以依名稱搜尋資產。在搜尋您輸入的關鍵字時，檔案名稱的開頭為。 例如，輸入&quot;swimming&quot;會尋找任何以該順序的字母開頭的資產檔案名稱。 在輸入詞語以尋找資產後，請務必按一下「輸入」。

![chlimage_1-65](assets/chlimage_1-65.png)

**資料夾/** 路徑所顯示的資料夾的名稱取決於您選擇的配置。您可以按一下資料夾圖示並選取子資料夾，然後按一下核取標籤以選取，以深入檢視下層。

如果您輸入關鍵字並選擇資料夾，AEM會搜尋該資料夾和任何子資料夾。 不過，如果您在搜尋時未輸入任何關鍵字，選取檔案夾將只會顯示該檔案夾中的資產，且不會包含任何子檔案夾。

依預設，AEM會搜尋選取的檔案夾和所有子檔案夾。

![chlimage_1-66](assets/chlimage_1-66.png)

**資產類** 型選取Scene7以瀏覽Scene7內容。只有已設定Scene7時，才可使用此選項。

![chlimage_1-67](assets/chlimage_1-67.png)

**設** 定若您在雲端服務中定義了多個Scene7設定，您可在此處選取它。因此，資料夾會根據您選擇的組態而變更。

![chlimage_1-68](assets/chlimage_1-68.png)

**資產** 類型在Scene7瀏覽器中，您可以篩選結果以包含下列任一項：影像、範本、視訊和最適化視訊集。如果您未選取任何資產類型，AEM依預設會搜尋所有資產類型。

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* 在傳統UI中，您也可以搜尋&#x200B;**Flash**&#x200B;和&#x200B;**FXG**。 目前不支援在觸控最佳化UI中篩選這些項目。
   >
   >
* 搜尋視訊時，您會搜尋單一轉譯。 結果會傳回原始轉譯（僅*.mp4）和編碼轉譯。
* 在搜尋最適化視訊集時，您會搜尋資料夾和所有子資料夾，但前提是您已新增關鍵字至搜尋。 如果您尚未新增關鍵字，AEM不會搜尋子資料夾。



**發佈** 狀態您可以根據發佈狀態篩選資產：未發佈或已發佈。如果您未選取任何「發佈狀態」,AEM依預設會搜尋所有發佈狀態。

![chlimage_1-70](assets/chlimage_1-70.png)
