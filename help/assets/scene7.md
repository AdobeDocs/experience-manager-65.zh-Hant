---
title: 將Dynamic Media Classic功能新增至您的頁面
description: 瞭解如何將Dynamic Media Classic功能和元件新增至AEM頁面。
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
translation-type: tm+mt
source-git-commit: e95f26cc1a084358b6bcb78605e3acb98f257b66
workflow-type: tm+mt
source-wordcount: '2860'
ht-degree: 0%

---


# 將動態媒體經典功能新增至頁面{#adding-scene-features-to-your-page}

[Adobe Dynamic Media ](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) Classics是代管解決方案，可管理、增強、發佈和提供多媒體資產至網路、行動裝置、電子郵件和網際網路連線的展示和印刷品。

您可以在各種檢視器中檢視在Dynamic Media Classic中發佈的AEM資產：

* 縮放
* 飛出
* 影片
* 影像範本
* 影像

您可以直接從AEM發佈數位資產至Dynamic Media Classic，也可以從Dynamic Media Classic發佈數位資產至AEM。

本檔案說明如何將數位資產從AEM發佈至Dynamic Media Classic，反之亦然。 檢視器也會有詳細說明。 如需為Dynamic Media Classic設定AEM的詳細資訊，請參閱[「整合Dynamic Media Classic與AEM](/help/sites-administering/scene7.md)」。

另請參閱[添加映像映射](image-maps.md)。

如需搭配AEM使用視訊元件的詳細資訊，請參閱[ Video](video.md)。

>[!NOTE]
>
>如果Dynamic Media Classic資產未正確顯示，請確定Dynamic Media is [disabled](config-dynamic.md#disabling-dynamic-media)，然後重新整理頁面。

## 從資產{#manually-publishing-to-scene-from-assets}手動發佈至Dynamic Media Classic

您可以按如下方式將數位資產發佈至Dynamic Media Classic:

* [在Assets主控台的傳統使用者介面中](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [在傳統使用者介面中，從資產](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [在傳統使用者介面中，從外部的CQ Target檔案夾](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>AEM以非同步方式發佈至Dynamic Media Classic。 按一下&#x200B;**[!UICONTROL Publish]**&#x200B;後，您的資產可能需要數秒鐘才能發佈至Dynamic Media Classic。


## Dynamic Media Classic元件{#scene-components}

AEM提供下列Dynamic Media Classic元件：

* 縮放
* 彈出（縮放）
* 影像範本
* 影像
* 影片

>[!NOTE]
>
>預設情況下，這些元件不可用，在使用之前，需要在&#x200B;**[!UICONTROL Design]**&#x200B;模式中選擇這些元件。

在&#x200B;**[!UICONTROL Design]**&#x200B;模式中提供這些元件後，您就可以像其他AEM元件一樣，將元件新增至您的頁面。 尚未發佈至Dynamic Media Classic的資產會發佈至Dynamic Media Classic（位於同步化資料夾、頁面或Dynamic Media Classic雲端組態）。

>[!NOTE]
>
>如果您要建立和開發自訂檢視器，並使用內容搜尋器，則需要明確新增&#x200B;**[!UICONTROL allowfullscreen]**&#x200B;參數。

### Flash 檢視器生命週期結束注意事項 {#flash-viewers-end-of-life-notice}

自2017年1月31日起，Adobe Dynamic Media Classic停止支援Flash檢視器平台。

如需此重要變更的詳細資訊，請參閱[Flash Viewer生命週期結束常見問答集](https://docs.adobe.com/content/docs/en/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html)。

### 將Dynamic Media Classic元件(Scene7)新增至頁面{#adding-a-scene-component-to-a-page}

將Dynamic Media Classic(Scene7)元件新增至頁面與將元件新增至任何頁面相同。 Dynamic Media Classic元件將在下列章節中詳細說明。

**若要將Dynamic Media Classic(Scene7)元件新增至頁面**

1. 在AEM中，開啟您要新增Dynamic Media Classic(Scene7)元件的頁面。

1. 如果沒有可用的Dynamic Media Classic元件，請按一下&#x200B;**[!UICONTROL Design]**&#x200B;模式，點選任何藍邊框的元件，點選&#x200B;**[!UICONTROL Parent]**&#x200B;圖示，然後按一下&#x200B;**[!UICONTROL Configuration]**&#x200B;圖示。 在&#x200B;**[!UICONTROL Parsys(Design)]**&#x200B;中，選擇所有Dynamic Media Classic元件以使其可用，然後按一下&#x200B;**[!UICONTROL 確定。]**

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. 按一下&#x200B;**[!UICONTROL 編輯]**&#x200B;返回到&#x200B;**[!UICONTROL 編輯]**&#x200B;模式。

1. 將sidekick中的Dynamic Media Classic群組元件拖曳至所需位置的頁面。

1. 按一下&#x200B;**[!UICONTROL Configuration]**&#x200B;表徵圖以開啟元件。

1. 根據需要編輯元件，然後按一下&#x200B;**[!UICONTROL OK]**&#x200B;保存更改。
1. 從內容瀏覽器將您的影像或視訊拖曳至您新增至頁面的Dynamic Media Classic元件。

   >[!NOTE]
   >
   >僅在觸控UI中，您必須將影像或視訊拖放至您放在頁面上的Dynamic Media Classic元件上。 不支援選取和編輯Dynamic Media Classic元件，然後選擇資產。

### 將互動式檢視體驗新增至回應式網站{#adding-interactive-viewing-experiences-to-a-responsive-website}

針對您的資產進行多方互動設計，表示您的資產會依其顯示位置而調整。 透過多方互動設計，可在多種裝置上有效顯示相同的資產。

另請參閱[網頁自適應設計](/help/sites-developing/responsive.md)。

**若要將互動式檢視體驗新增至互動式網站**

1. 登入AEM，並確定您已設定[ Adobe Dynamic Media Classic Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration)，且Dynamic Media Classic元件已可供使用。

   >[!NOTE]
   >
   >如果Dynamic Media Classic元件不可用，請確定[要透過設計模式](/help/sites-authoring/default-components-designmode.md)啟用它們。

1. 在啟用&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;元件的網站中，將&#x200B;**[!UICONTROL Image]**&#x200B;元件拖曳至頁面。
1. 選取元件並點選設定圖示。
1. 在&#x200B;**[!UICONTROL 動態媒體經典設定]**&#x200B;標籤中，調整中斷點。

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. 確認檢視器正在回應性地調整大小，而且所有互動都已針對桌上型電腦、平板電腦和行動裝置最佳化。

### 所有Dynamic Media Classic元件的常用設定{#settings-common-to-all-scene-components}

雖然配置選項不同，但所有[!UICONTROL Dynamic Media Classic]元件都有以下通用選項：

* **[!UICONTROL 檔案引用]** -瀏覽到要引用的檔案。檔案參考會顯示資產URL，但不一定是完整的Dynamic Media Classic URL，包括URL命令和參數。 您無法在此欄位中新增Dynamic Media Classic URL命令和參數。 它們必須透過元件中的對應功能來新增。
* **[!UICONTROL 寬度]** -可讓您設定寬度。
* **[!UICONTROL 高度]** -可讓您設定高度。

您可以開啟（按兩下）Dynamic Media Classic元件，例如開啟&#x200B;**[!UICONTROL Zoom]**&#x200B;元件時，設定這些設定選項：

![chlimage_1-226](assets/chlimage_1-226.png)

### 縮放 {#zoom}

當您按下&#x200B;**[!UICONTROL +]**&#x200B;按鈕時，HTML5縮放元件會顯示較大的影像。

資產底部有縮放工具。 點選&#x200B;**[!UICONTROL +]**&#x200B;以放大。 點選&#x200B;**[!UICONTROL -]**&#x200B;以減少。 點選&#x200B;**[!UICONTROL x]**&#x200B;或重設縮放箭頭會將影像重新調整為原本匯入的大小。 點選對角線箭頭，讓它成為全螢幕。 點選「**[!UICONTROL 編輯]**」以設定元件。 使用此元件，可以配置所有[!UICONTROL Dynamic Media Classic]元件](#settings-common-to-all-scene-components)的公共[設定。

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### 彈出{#flyout}

在HTML5 **[!UICONTROL Flyout]**&#x200B;元件中，資產顯示為分割畫面；將資產保留在指定的大小；右側顯示縮放部分。 點選「**[!UICONTROL 編輯]**」以設定元件。 使用此元件，可以配置所有Dynamic Media Classic元件[的常用設定。](#settings-common-to-all-scene-components)

>[!NOTE]
>
>如果您的&#x200B;**[!UICONTROL Flyout]**&#x200B;元件使用自訂大小，則會使用該自訂大小，並停用元件的回應式設定。
>
>如果您的&#x200B;**[!UICONTROL Flyout]**&#x200B;元件使用預設大小（如&#x200B;**[!UICONTROL 設計檢視]**&#x200B;中所設定），則會使用預設大小，而元件會延伸以配合頁面版面大小，並啟用元件的回應式設定。 但請注意，元件的回應式設定有限。 當您使用具有自適應設定的&#x200B;**[!UICONTROL Flyout]**&#x200B;元件時，不應將它用於完整頁面延伸。 否則，**[!UICONTROL Flyout]**&#x200B;可延伸超過頁面的右邊框。

![chlimage_1-228](assets/chlimage_1-228.png)

### 影像 {#image}

Dynamic Media Classic **[!UICONTROL Image]**&#x200B;元件可讓您將Dynamic Media Classic功能新增至影像，例如Dynamic Media Classic修飾元、影像或檢視器預設集，以及銳利化。 Dynamic Media Classic **[!UICONTROL Image]**&#x200B;元件類似於AEM中具有特殊Dynamic Media Classic功能的其他影像元件。 在此範例中，影像已套用Dynamic Media Classic URL修飾元`&op_invert=1`。

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL 標題、替代文字]** -在「進階」 **** 索引標籤中，為影像新增標題，並為關閉圖形的使用者新增替代文字。

**[!UICONTROL URL, Open in]** - You can set an asset from to open a link.設定&#x200B;**[!UICONTROL URL]**，並在&#x200B;**[!UICONTROL 的「在]**&#x200B;中開啟」中指出您要在相同視窗或新視窗中開啟。

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL 檢視器預設]** -從下拉式選單中選取現有的檢視器預設。如果您所尋找的檢視器預設集不可見，您可能需要將它顯示。 請參閱[管理檢視器預設集](/help/assets/managing-viewer-presets.md)。 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

**[!UICONTROL Dynamic Media Classic Configuration]**  —— 選取您要用來從SPS擷取作用中影像預設集的Dynamic Media Classic組態。

**[!UICONTROL 影像預設]** -從下拉式選單中選取現有的影像預設。如果您要尋找的影像預設集不可見，您可能需要將它顯示。 請參閱[管理影像預設集](/help/assets/managing-image-presets.md)。 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

**[!UICONTROL 輸出格式]** -選擇影像的輸出格式，例如jpeg。視您選擇的輸出格式而定，您可能會有其他設定選項。 請參閱[影像預設集最佳範例](/help/assets/managing-image-presets.md#image-preset-options)。

**[!UICONTROL 銳利化]** -選擇影像銳利化的方式。銳利化在[影像預設集最佳實務](/help/assets/managing-image-presets.md#image-preset-options)和[銳利化最佳實務](/help/assets/assets/sharpening_images.pdf)中詳細說明。

**[!UICONTROL URL修飾元]** -您可以提供額外的Dynamic Media Classic影像指令來變更影像效果。這些說明在[影像預設集](/help/assets/managing-image-presets.md)和[命令參考](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html)中。

**[!UICONTROL 中斷點]** -如果您的網站是互動式的，您需要調整中斷點。中斷點必須以逗號(,)分隔。

### 影像範本 {#image-template}

[Dynamic Media Classic Image ](https://docs.adobe.com/help/en/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) Template是分層Photoshop內容，已匯入至Dynamic Media Classic，內容和屬性會因變數而參數化。**[!UICONTROL Image template]**&#x200B;元件可讓您在AEM中匯入影像並動態變更文字。 此外，您還可以設定&#x200B;**[!UICONTROL 影像範本]**&#x200B;元件，使用用戶端內容的值，讓每位使用者以個人化方式體驗影像。

點選「**[!UICONTROL 編輯]**」以設定元件。 您可以設定所有Dynamic Media Classic元件的常用[設定，以及本節所述的其他設定。](#settings-common-to-all-scene-components)

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL 檔案參考、寬度、高度]** -檢視所有ScDynamic Media Classicene7元件的常用設定。

>[!NOTE]
>
>Dynamic Media Classic URL命令和參數無法直接新增至「檔案參考URL」。 它們只能在&#x200B;**[!UICONTROL 參數]**&#x200B;面板中的元件UI中定義。

**[!UICONTROL 標題、替代文字]** -在「動態媒體經典影像範本」標籤中，為影像新增標題，並為已關閉圖形的使用者新增替代文字。

**[!UICONTROL URL, Open in]** - You can set an asset from to open a link.設定URL，並在「開啟於」中指出您要在相同視窗或新視窗中開啟它。

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL 參數面板]** -匯入影像時，會預先填入影像的資訊。如果沒有可動態變更的內容，則此視窗為空。

![chlimage_1-233](assets/chlimage_1-233.png)

#### 動態變更文字{#changing-text-dynamically}

要動態更改文本，請在欄位中輸入新文本，然後按一下「確定」。**** 在此範例中， **** Price現在是$50，而運費是99美分。

![chlimage_1-234](assets/chlimage_1-234.png)

影像中的文字會變更。 您可以點選欄位旁的&#x200B;**[!UICONTROL Reset]**，將文字重設回原始值。

![chlimage_1-235](assets/chlimage_1-235.png)

#### 變更文字以反映用戶端內容值{#changing-text-to-reflect-the-value-of-a-client-context-value}的值

若要將欄位連結至用戶端內容值，請點選&#x200B;**[!UICONTROL Select]**&#x200B;以開啟用戶端內容功能表，選取用戶端內容，然後點選&#x200B;**[!UICONTROL 確定。]** 在此示例中，名稱會根據將名稱與配置檔案中的格式化名稱連結而改變。

![chlimage_1-236](assets/chlimage_1-236.png)

文字會反映目前登入使用者的名稱。 您可以按一下欄位旁的&#x200B;**[!UICONTROL Reset]**，將文字重設回原始值。

![chlimage_1-237](assets/chlimage_1-237.png)

#### 使動態媒體經典映像模板成為連結{#making-the-scene-image-template-a-link}

1. 在具有Dynamic Media Classic **[!UICONTROL Image Template]**&#x200B;元件的頁面上，點選「編輯」。]****[!UICONTROL 
1. 在&#x200B;**[!UICONTROL URL]**&#x200B;欄位中，輸入在點選影像時使用者前往的URL。 在&#x200B;**[!UICONTROL 在]**&#x200B;欄位中開啟，選取您要開啟目標（新視窗或相同視窗）。

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. 點選&#x200B;**[!UICONTROL 確定。]**

### 視訊元件{#video-component}

Dynamic Media Classic **[!UICONTROL Video]**&#x200B;元件（可從側腳的Dynamic Media Classic區段取得）使用裝置和頻寬偵測，為每個螢幕提供正確的視訊。 此元件為HTML5視訊播放器；它是可跨通道使用的單一檢視器。

它可用於最適化視訊集、單一MP4視訊或單一F4V視訊。

如需有關視訊如何與Dynamic Media Classic整合的詳細資訊，請參閱[Video](s7-video.md)。 此外，請參閱[動態媒體經典視訊元件與Foundation Video元件](s7-video.md)。

![chlimage_1-239](assets/chlimage_1-239.png)

### 視訊元件{#known-limitations-for-the-video-component}的已知限制

Adobe DAM和WCM會顯示是否上傳主要來源視訊。 它們不會顯示下列代理資產：

* 動態媒體經典編碼轉譯
* Dynamic Media Classic可調式視訊集

當搭配Dynamic Media Classic視訊元件使用最適化視訊集時，您需要調整元件大小以符合視訊的尺寸。

## Dynamic Media Classic內容瀏覽器{#scene-content-browser}

Dynamic Media Classic內容瀏覽器可讓您直接在AEM中從Dynamic Media Classic檢視內容。 若要存取內容瀏覽器，請在&#x200B;**[!UICONTROL Content Finder]**&#x200B;中，選取觸控最佳化使用者介面中的&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;或傳統使用者介面中的&#x200B;**[!UICONTROL S7]**&#x200B;圖示。 這兩個使用者介面的功能完全相同。

如果您有多個設定，AEM依預設會顯示[預設設定](/help/sites-administering/scene7.md#configuring-a-default-configuration)。 您可以直接在下拉式選單的Dynamic Media Classic內容瀏覽器中選取不同的設定。

>[!NOTE]
>
>* 位於臨機資料夾的資產不會出現在Dynamic Media Classic內容瀏覽器中。
>* 當[啟用「保全預覽」時，Dynamic Media Classic的已發佈和未發佈資產都會顯示在Dynamic Media Classic內容瀏覽器中。](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)
>* 如果內容瀏覽器中未將&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;或&#x200B;**[!UICONTROL S7]**&#x200B;圖示視為選項，您需要[設定Dynamic Media Classic以搭配AEM](/help/sites-administering/scene7.md)運作。
>* 對於視訊，Dynamic Media Classic內容瀏覽器支援：

   >
   >   
   * 最適化視訊集：容器，以便在多個螢幕上順暢播放所需的所有視訊轉譯
   >   * 單一MP4視訊
   >   * 單一F4V視訊


### 瀏覽觸控最佳化UI中的內容{#browsing-content-in-the-touch-optimized-ui}

您可以在觸控最佳化或傳統UI中存取內容瀏覽器。 目前最佳化觸控功能有下列限制：

* 不支援Dynamic Media Classic的FXG和Flash資產。

從第三個下拉式選單中選取&#x200B;**[!UICONTROL Dynamic Media Classic]**，以瀏覽Dynamic Media Classic資產。 如果您尚未設定Dynamic Media Classic/AEM整合，Dynamic Media Classic不會出現在清單中。

>[!NOTE]
>
>* Dynamic Media Classic內容瀏覽器會載入約100個資產，並依名稱排序。
>* 如果您已設定安全的預覽伺服器，瀏覽器會使用該預覽伺服器來轉譯縮圖和資產。

>



![chlimage_1-240](assets/chlimage_1-240.png)

此外，您還可以將滑鼠指標暫留在瀏覽器中的資產上，以瀏覽解析度資訊、大小、修改後的天數和檔案名稱。

![chlimage_1-241](assets/chlimage_1-241.png)

* 對於最適化視訊集和範本，不會產生縮圖的大小資訊。
* 對於最適化視訊集，不會產生縮圖的解析度。

### 使用內容瀏覽器{#searching-for-scene-assets-with-the-content-browser}搜尋Dynamic Media Classic資產

搜尋Dynamic Media Classic資產類似於搜尋AEM資產，但搜尋時，您實際看到的是Dynamic Media Classic系統中資產的遠端檢視，而非直接將資產匯入AEM。

您可以使用傳統UI或觸控最佳化UI來檢視和搜尋資產。 視介面而定，您的搜尋方式略有不同。

在任一UI中搜尋時，您可依下列條件進行篩選（如觸控最佳化UI中所示）:

**[!UICONTROL 輸入關鍵字]** -您可以依名稱搜尋資產。在搜尋您輸入的關鍵字時，檔案名稱的開頭為。 例如，輸入&quot;swimming&quot;會尋找任何以該順序的字母開頭的資產檔案名稱。 在輸入詞語以尋找資產後，請務必點選「輸入」。

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL 資料夾／路徑]** -顯示的資料夾的名稱取決於您選擇的配置。您可以點選資料夾圖示並選取子資料夾，然後點選核取標籤以選取它，以深入探究至較低層級。

如果您輸入關鍵字並選擇資料夾，AEM會搜尋該資料夾和任何子資料夾。 不過，如果您在搜尋時未輸入任何關鍵字，選取檔案夾將只會顯示該檔案夾中的資產，且不會包含任何子檔案夾。

依預設，AEM會搜尋選取的檔案夾和所有子檔案夾。

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL 資產類型]** -選取「動 **[!UICONTROL 態媒體]** 類別」以瀏覽Dynamic Media Classic內容。只有已配置Dynamic Media Classic時，此選項才可用。

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL 配置]** -如果您在 [!UICONTROL Cloud Services中定義了多個Dynamic Media Classic配置]，則可在此處選擇它。因此，資料夾會根據您選擇的組態而變更。

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL 資產類型]** -在Dynamic Media Classic瀏覽器中，您可以篩選結果以包含下列任一項：影像、範本、視訊和最適化視訊集。如果您未選取任何資產類型，AEM依預設會搜尋所有資產類型。

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* 在傳統UI中，您也可以搜尋&#x200B;**Flash**&#x200B;和&#x200B;**FXG**。 目前不支援在觸控最佳化UI中篩選這些項目。
   >
   >
* 搜尋視訊時，您會搜尋單一轉譯。 結果會傳回原始轉譯（僅&amp;ast;.mp4）和編碼轉譯。
>* 在搜尋最適化視訊集時，您會搜尋資料夾和所有子資料夾，但前提是您已新增關鍵字至搜尋。 如果您尚未新增關鍵字，AEM不會搜尋子資料夾。

>



**[!UICONTROL 發佈狀態]** -您可以根據發佈狀態篩選資產： **[!UICONTROL 未發]** 布或已 **[!UICONTROL 發佈。]** 如果您未選取任何「發 **[!UICONTROL 布狀態]**」,AEM依預設會搜尋所有發佈狀態。

![chlimage_1-247](assets/chlimage_1-247.png)

