---
title: 新增Dynamic Media Classic (Scene7)功能至您的頁面
description: Adobe Dynamic Media Classic (Scene7)是託管式解決方案，可管理、增強和發佈多媒體資產，並將其遞送至網路、行動裝置、電子郵件和網際網路連線的顯示和列印。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: bc9c864b-8bc3-42b4-ba25-6c5108be4f65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '3545'
ht-degree: 1%

---

# 新增Dynamic Media Classic (Scene7)功能至您的頁面{#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic (Scene7)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html)是託管式解決方案，可管理、增強、發佈多媒體資產，並將其傳送至網路、行動裝置、電子郵件及連線至網際網路的顯示器和列印。

您可以在多種檢視器中檢視在Dynamic Media Classic (Scene7)中發佈的Experience Manager資產：

* 縮放
* 彈出
* 影片
* 影像範本
* 影像

您可以直接從Experience Manager將數位資產發佈到Dynamic Media Classic (Scene7)，也可以從Dynamic Media Classic (Scene7)將數位資產發佈到Experience Manager。

本檔案說明如何從Experience Manager將數位資產發佈到Dynamic Media Classic (Scene7)，反之亦然。 檢視器也會詳細說明。 如需為Dynamic Media Classic (Scene7)設定Experience Manager的詳細資訊，請參閱[整合Dynamic Media Classic (Scene7)與Experience Manager](/help/sites-administering/scene7.md)。

另請參閱[新增影像地圖](/help/assets/image-maps.md)。

如需搭配Experience Manager使用視訊元件的詳細資訊，請參閱下列內容：

* [影片](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>如果Dynamic Media Classic (Scene7)資產未正確顯示，請確定Dynamic Media已[停用](/help/assets/config-dynamic.md#disabling-dynamic-media)，然後重新整理頁面。

## 從Assets手動發佈至Dynamic Media Classic (Scene7) {#manually-publishing-to-scene-from-assets}

您可以在傳統UI中從Dynamic Media Classic主控台發佈數位資產到Assets (Scene7)，或直接從資產發佈。

>[!NOTE]
>
>Experience Manager以非同步方式發佈至Dynamic Media Classic (Scene7)。 選取&#x200B;**[!UICONTROL Publish]**&#x200B;後，您的資產可能需要幾秒鐘才能發佈至Dynamic Media Classic (Scene7)。
>

### 從Assets主控台發佈 {#publishing-from-the-assets-console}

如果資產位於Dynamic Media Classic (Scene7)目標資料夾，您可以從Assets主控台發佈至Dynamic Media Classic (Scene7)。

1. 在Experience Manager Classic UI中，選取&#x200B;**[!UICONTROL 數位Assets]**&#x200B;以存取數位資產管理器。

1. 從目標資料夾中選取您要發佈至Dynamic Media Classic (Scene7)的資產（或資產）或資料夾，然後按一下滑鼠右鍵並選取&#x200B;**[!UICONTROL Publish至Dynamic Media Classic (Scene7)]**。 或者，您也可以從&#x200B;**[!UICONTROL 工具]**&#x200B;功能表選取&#x200B;**[!UICONTROL Publish到Dynamic Media Classic (Scene7)]**。

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. 前往Dynamic Media Classic (Scene7)並確認資產可供使用。

   >[!NOTE]
   >
   >如果資產不在Dynamic Media Classic (Scene7)同步資料夾中，兩個功能表中的&#x200B;**[!UICONTROL Publish到Dynamic Media Classic (Scene7)]**&#x200B;可見但停用。

### 從資產執行Publish {#publishing-from-an-asset}

您可以手動發佈資產，只要該資產位於已同步的Dynamic Media Classic (Scene7)資料夾內即可。

>[!NOTE]
>
>如果資產不在Dynamic Media Classic (Scene7)已同步處理的資料夾中，則不會顯示&#x200B;**[!UICONTROL Publish到Dynamic Media Classic (Scene7)]**&#x200B;的連結。

若要直接從數位資產發佈至Dynamic Media Classic (Scene7)：

1. 在Experience Manager中，選取&#x200B;**[!UICONTROL 數位Assets]**&#x200B;以存取數位資產管理器。

1. 按兩下以開啟資產。

1. 在資產詳細資料窗格中，選取&#x200B;**[!UICONTROL Publish to Dynamic Media Classic (Scene7)]**。

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. 連結變更為&#x200B;**[!UICONTROL 發佈……]**，然後&#x200B;**[!UICONTROL 發佈]**。 前往Dynamic Media Classic (Scene7)並確認資產可供使用。

   >[!NOTE]
   >
   >如果資產未正確發佈至Dynamic Media Classic (Scene7)，連結會變更為&#x200B;**[!UICONTROL 發佈失敗]**。 如果資產已發佈至Dynamic Media Classic (Scene7)，連結會顯示&#x200B;**[!UICONTROL 重新Publish至Dynamic Media Classic (Scene7)]**。 重新發佈可讓您變更Experience Manager中的資產並重新發佈。

### CQ目標資料夾外部的Publish資產 {#publishing-assets-from-outside-the-cq-target-folder}

Adobe建議您只從Dynamic Media Classic (Scene7)目標資料夾內的資產將資產發佈到Dynamic Media Classic (Scene7)。 不過，如果您必須從目標資料夾以外的資料夾上傳資產，您仍然可以透過將其上傳到Dynamic Media Classic (Scene7)上的隨選資料夾來執行此操作。 首先，針對您想要資產出現的頁面，設定雲端設定。 然後新增Dynamic Media Classic (Scene7)元件至頁面，並將資產拖放到元件上。 為該頁面設定頁面屬性後，在選取的觸發器上傳至Dynamic Media Classic (Scene7)時，會顯示&#x200B;**[!UICONTROL Publish至Dynamic Media Classic (Scene7)]**&#x200B;連結。

>[!NOTE]
>
>隨選資料夾中的Assets不會出現在Dynamic Media Classic (Scene7)內容瀏覽器中。

**若要從CQ目標資料夾外部發佈資產：**

1. 在傳統UI的Experience Manager中，選取&#x200B;**[!UICONTROL 網站]**，並導覽至您要新增數位資產至但尚未發佈至Dynamic Media Classic (Scene7)的網頁。 （適用一般頁面繼承規則。）

1. 在Sidekick中，選取&#x200B;**[!UICONTROL 頁面]**&#x200B;圖示並選取&#x200B;**[!UICONTROL 頁面屬性]**。

1. 選取&#x200B;**[!UICONTROL Cloud Service]**。
1. 選取&#x200B;**[!UICONTROL 新增服務]**。
1. 選取&#x200B;**[!UICONTROL Dynamic Media Classic (Scene7)]**。
1. 在&#x200B;**[!UICONTROL Adobe Dynamic Media Classic (Scene7)]**&#x200B;下拉式清單中，選取所需的組態，然後選取&#x200B;**[!UICONTROL 確定]**。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 在網頁上，將Dynamic Media Classic (Scene7)元件新增至頁面上所需位置。
1. 從內容尋找器中，將數位資產拖曳至元件。 您看到指向&#x200B;**[!UICONTROL 檢查Dynamic Media Classic (Scene7)出版物狀態]**&#x200B;的連結。

   >[!NOTE]
   >
   >如果數位資產在CQ目標資料夾中，則不會顯示指向&#x200B;**[!UICONTROL 檢查Dynamic Media Classic (Scene7)發佈狀態]**&#x200B;的連結。 資產會放置在元件中。

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. 選取&#x200B;**[!UICONTROL 檢查Dynamic Media Classic (Scene7)發佈狀態]**。 如果資產未發佈，Experience Manager會將資產發佈至Dynamic Media Classic (Scene7)。 上傳之後，即可在隨選資料夾中找到資產。 依預設，隨選資料夾位於&#x200B;**[!UICONTROL name_of_the_company/CQ5_adhoc]**。 如果需要，您可以[設定隨選資料夾](#configuringtheadhocfolder)。

   >[!NOTE]
   >
   >如果資產不在Dynamic Media Classic (Scene7)同步資料夾中，而且沒有Dynamic Media Classic (Scene7)雲端設定與目前頁面相關聯，上傳會失敗。

## Dynamic Media Classic (Scene7)元件 {#scene-components}

下列Dynamic Media Classic (Scene7)元件均可在Experience Manager中使用：

* 縮放
* 彈出（縮放）
* 影像範本
* 影像
* 影片

>[!NOTE]
>
>預設不會提供這些元件，且必須在使用之前在設計模式中選取這些元件。

在「設計」模式中提供元件後，您就可以像新增任何其他Experience Manager元件一樣將元件新增至頁面。 如果是在已同步處理的資料夾或頁面上，或是使用Assets (Scene7)雲端設定，則尚未發佈至Dynamic Media Classic (Scene7)的Dynamic Media Classic會發佈至Dynamic Media Classic (Scene7)。

>[!NOTE]
>
>如果您要建立及開發自訂S7檢視器並使用「內容尋找器」，則必須明確新增`allowfullscreen`引數。

### Flash檢視器生命週期結束通知 {#flash-viewers-end-of-life-notice}

自2017年1月31日起，Adobe Dynamic Media Classic (Scene7)正式停止支援Flash檢視器平台。

### 將Dynamic Media Classic (Scene7)元件新增至頁面 {#adding-a-scene-component-to-a-page}

將Dynamic Media Classic (Scene7)元件新增至頁面，與將元件新增至任何頁面相同。 以下各節將詳細說明Dynamic Media Classic (Scene7)元件。

若要將Dynamic Media Classic (Scene7)元件/檢視器新增至傳統UI中的頁面：

1. 在Experience Manager中，開啟您要新增Dynamic Media Classic (Scene7)元件的頁面。

1. 如果沒有可用的Dynamic Media Classic (Scene7)元件，請選取sidekick中的尺標以進入&#x200B;**設計**&#x200B;模式，選取&#x200B;**[!UICONTROL 編輯]** parsys，然後選取所有&#x200B;**[!UICONTROL Dynamic Media Classic (Scene7)]**&#x200B;元件以供使用。

1. 選取sidekick中的鉛筆，返回&#x200B;**編輯**&#x200B;模式。

1. 將元件從Sidekick中的&#x200B;**[!UICONTROL Dynamic Media Classic (Scene7)]**&#x200B;群組拖曳到頁面上的所需位置。

1. 選取***[!UICONTROL 編輯]**，以便開啟元件。

1. 視需要編輯元件，並選取&#x200B;**[!UICONTROL 確定]**&#x200B;以儲存變更。

### 在回應式網站中新增互動式檢視體驗 {#adding-interactive-viewing-experiences-to-a-responsive-website}

資產的回應式設計表示您的資產會根據顯示位置進行調整。 透過回應式設計，相同的資產能夠有效地在多部裝置上顯示。

若要在傳統UI中新增互動式檢視體驗至回應式網站：

1. 登入Experience Manager，並確認您已設定[Adobe Dynamic Media Classic (Scene7)Cloud Service](/help/sites-administering/scene7.md#configuring-scene-integration)，而且Dynamic Media Classic (Scene7)元件可供使用。

   >[!NOTE]
   >
   >如果Dynamic Media Classic (Scene7) WCM元件無法使用，請務必透過設計模式將其啟用。

1. 在啟用Dynamic Media Classic (Scene7)元件的網站中，將&#x200B;**[!UICONTROL Image]**&#x200B;檢視器拖曳至頁面。
1. 在&#x200B;**[!UICONTROL Dynamic Media Classic (Scene7)設定]**&#x200B;索引標籤中編輯元件並調整中斷點。

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. 確認檢視器是否以回應式方式調整大小，以及所有互動是否針對桌上型電腦、平板電腦和行動裝置進行最佳化。

### 所有Dynamic Media Classic (Scene7)元件的通用設定 {#settings-common-to-all-scene-components}

雖然設定選項有所差異，下列專案是所有Dynamic Media Classic (Scene7)元件的共同專案：

* **檔案參考** — 瀏覽您要參考的檔案。 檔案參考會顯示資產URL，不一定是完整的Dynamic Media Classic (Scene7) URL，包括URL命令和引數。 您無法在此欄位中新增Dynamic Media Classic (Scene7) URL命令和引數。 反之，必須透過元件中的對應功能新增這些引數。
* **寬度** — 可讓您設定寬度。
* **高度** — 可讓您設定高度。

您可以透過開啟（按兩下） Dynamic Media Classic (Scene7)元件來設定這些組態選項，例如，當您開啟&#x200B;**Zoom**&#x200B;元件時：

![chlimage_1-52](assets/chlimage_1-52.png)

### 縮放 {#zoom}

按下+按鈕時，HTML5縮放元件會顯示較大的影像。

資產底部有縮放工具。 選取&#x200B;**[!UICONTROL +]**&#x200B;以放大。 選取&#x200B;**[!UICONTROL -]**&#x200B;以縮小。 選取&#x200B;**[!UICONTROL x]**&#x200B;或重設縮放箭頭，將影像回覆為匯入的原始大小。 選取對角線箭頭，讓您可以全熒幕操作。 選取「**[!UICONTROL 編輯]**」以設定元件。 使用此元件，您可以設定所有Dynamic Media Classic (Scene7)元件的[共同設定](#settings-common-to-all-scene-components)。

![HTML5 Zoom元件內的鬱金香花朵影像。](do-not-localize/chlimage_1-3.png)

### 彈出 {#flyout}

在HTML5彈出式元件中，資產會顯示為拆分畫面；將資產留成指定大小；顯示縮放部分時會顯示為右側。 選取「**[!UICONTROL 編輯]**」以設定元件。 使用此元件，您可以設定所有Dynamic Media Classic (Scene7)元件的[共同設定](/help/sites-administering/scene7.md#settingscommontoallscene7components)。

>[!NOTE]
>
>如果您的彈出式元件使用自訂大小，則會使用該自訂大小，並停用元件的回應式設定。
>
>如果您的彈出式元件使用預設大小（在「設計」檢視中設定），則使用預設大小。 元件會延伸以容納頁面版面大小，並啟用元件的回應式設定。 但是，請注意，元件的回應式設定存在限制。 搭配回應式設定使用彈出式元件時，請勿將其用於完整頁面延伸。 否則，彈出式視窗可能會超出頁面的右邊框。

![chlimage_1-53](assets/chlimage_1-53.png)

### 影像 {#image}

Dynamic Media Classic (Scene7)影像元件可讓您將Dynamic Media Classic (Scene7)功能新增至影像，例如Dynamic Media Classic (Scene7)修飾元、影像或檢視器預設集，以及銳利化。 Dynamic Media Classic (Scene7)影像元件類似於Experience Manager中的其他影像元件，具有特殊的Dynamic Media Classic (Scene7)功能。 在此範例中，影像已套用Dynamic Media Classic (Scene7) URL修飾元`&op_invert=1`。

![Dynamic Media Classic (Scene 7)影像元件內的球面影像](do-not-localize/chlimage_1-4.png)

**標題，替代文字** — 在[進階]索引標籤中，為圖形關閉的使用者新增標題和替代文字。

**URL，在**&#x200B;中開啟 — 您可以從設定開啟連結的資產。 設定URL，並在的「開啟」中指定您要在相同視窗中開啟還是要在新視窗中開啟。

![chlimage_1-54](assets/chlimage_1-54.png)

**檢視器預設集** — 從下拉式選單中選取現有的檢視器預設集。 如果您要尋找的檢視器預設集未顯示，您必須讓它顯示。 請參閱管理檢視器預設集。 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

**Dynamic Media Classic (Scene7)設定** — 選取您要用來從SPS擷取作用中影像預設集的Dynamic Media Classic (Scene7)設定。

**影像預設集** — 從下拉式選單中選取現有的影像預設集。 如果您要尋找的影像預設集不可見，您必須讓它可見。 請參閱管理影像預設集。 如果您使用影像預設集，則無法選取檢視器預設集，反之亦然。

**輸出格式** — 選取影像的輸出格式，例如jpeg。 根據您選取的輸出格式，您可能有其他組態選項。 請參閱影像預設集最佳作法。

**銳利化** — 選取您要如何銳利化影像。 「影像預設集」最佳實務和「銳利化」最佳實務中會詳細說明銳利化。

**URL修飾元** — 您可以提供其他S7影像命令來變更影像效果。 這些指令在「影像預設集」和「指令」參照中進行了說明。

**中斷點** — 如果您的網站有回應，您想要調整中斷點。 中斷點必須以逗號(，)分隔。

### 影像範本 {#image-template}

Dynamic Media Classic (Scene7)影像範本是匯入至Dynamic Media Classic (Scene7)的圖層Photoshop內容，其內容和屬性已引數化為變動。 **[!UICONTROL 影像範本]**&#x200B;元件可讓您以Experience Manager匯入影像並動態變更文字。 此外，您可以將&#x200B;**[!UICONTROL 影像範本]**&#x200B;元件設定為使用使用者端內容的值，讓每位使用者都能透過個人化的方式體驗影像。

選取&#x200B;**[!UICONTROL 編輯]** — 以設定元件。 您可以設定所有Dynamic Media Classic (Scene7)元件的[通用設定](/help/sites-administering/scene7.md#settingscommontoallscene7components)以及本節中說明的其他設定。

![chlimage_1-55](assets/chlimage_1-55.png)

**檔案參考、寬度、高度** — 檢視所有Dynamic Media Classic (Scene7)元件共有的[設定](/help/sites-administering/scene7.md#settingscommontoallscene7components)。

>[!NOTE]
>
>Dynamic Media Classic (Scene7) URL命令和引數無法直接新增至檔案參考URL。 它們只能在&#x200B;**[!UICONTROL 引數]**&#x200B;面板的元件UI中定義。

**標題，替代文字** — 在Dynamic Media Classic (Scene7)的「影像範本」標籤中，為已關閉圖形的使用者新增標題和替代文字。

**URL，在**&#x200B;中開啟 — 您可以從設定開啟連結的資產。 設定URL，並在的「開啟」中指定您要在相同視窗中開啟還是要在新視窗中開啟。

![chlimage_1-56](assets/chlimage_1-56.png)

**引數面板** — 匯入影像時，引數會預先填入影像中的資訊。 如果沒有可動態變更的內容，此視窗為空白。

![chlimage_1-57](assets/chlimage_1-57.png)

#### 動態變更文字 {#changing-text-dynamically}

若要動態變更文字，請在欄位中輸入新文字，並選取&#x200B;**[!UICONTROL 確定]**。 在此範例中，**價格**&#x200B;現在為$50，而運費為99美分。

![chlimage_1-58](assets/chlimage_1-58.png)

影像中的文字會變更。 您可以選取欄位旁的&#x200B;**[!UICONTROL 重設]**，將文字重設為原始值。

![chlimage_1-59](assets/chlimage_1-59.png)

#### 變更文字以反映使用者端內容值的值 {#changing-text-to-reflect-the-value-of-a-client-context-value}

若要將欄位連結到使用者端內容值，請選取&#x200B;**[!UICONTROL 選取]**&#x200B;以開啟使用者端內容功能表，選取使用者端內容，然後選取&#x200B;**[!UICONTROL 確定]**。 在此範例中，名稱會根據連結設定檔中帶有格式化名稱的「名稱」而變更。

![chlimage_1-60](assets/chlimage_1-60.png)

此文字反映目前登入使用者的名稱。 您可以選取欄位旁的&#x200B;**[!UICONTROL 重設]**，將文字重設為原始值。

![chlimage_1-61](assets/chlimage_1-61.png)

#### 將Dynamic Media Classic (Scene7)影像範本設為連結 {#making-the-scene-image-template-a-link}

您可以將Dynamic Media Classic (Scene7)影像範本元件設成可點按的連結。

1. 在具有Dynamic Media Classic (Scene7)影像範本元件的頁面上，選取&#x200B;**[!UICONTROL 編輯]**。
1. 在&#x200B;**[!UICONTROL URL]**&#x200B;欄位中，輸入使用者按一下影像時前往的URL。 在&#x200B;**[!UICONTROL 在]**&#x200B;中開啟欄位中，選取是否要開啟目標（新視窗或相同視窗）。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 選取&#x200B;**[!UICONTROL 確定]**。

### 視訊元件 {#video-component}

Dynamic Media Classic (Scene7) **[!UICONTROL 影片]**&#x200B;元件(可從Sidekick的Dynamic Media Classic (Scene7)區段取得)使用裝置和頻寬偵測將正確的影片提供給每個熒幕。 此元件是HTML5視訊播放器；它是可用於跨頻道的單一檢視器。

它可用於自我調整視訊集、單一MP4視訊或單一F4V視訊。

請參閱[影片](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)，以取得有關影片如何搭配Dynamic Media Classic (Scene7)整合使用的詳細資訊。 此外，請檢視[Dynamic Media Classic (Scene7) video **元件與foundation** video **元件](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)的比較結果。**

![chlimage_1-63](assets/chlimage_1-63.png)

### 視訊元件的已知限制 {#known-limitations-for-the-video-component}

AdobeDAM和WCM會顯示是否上傳了主要來源影片。 它們不會顯示這些Proxy資產：

* Dynamic Media Classic (Scene7)編碼轉譯
* Dynamic Media Classic (Scene7)最適化視訊集

搭配Dynamic Media Classic (Scene7)視訊元件使用自我調整視訊集時，必須調整元件大小以符合視訊的尺寸。

## Dynamic Media Classic (Scene7)內容瀏覽器 {#scene-content-browser}

Dynamic Media Classic (Scene7)內容瀏覽器可讓您直接在Experience Manager中檢視Dynamic Media Classic (Scene7)的內容。 若要存取內容瀏覽器，請在「內容尋找器」中，選取觸控最佳化使用者介面中的&#x200B;**Dynamic Media Classic (Scene7)**，或傳統使用者介面中的&#x200B;**S7**&#x200B;圖示。 兩個使用者介面之間的功能相同。

如果您有多個組態，依預設Experience Manager會顯示[預設組態](/help/sites-administering/scene7.md#configuring-a-default-configuration)。 您可以在下拉式功能表中直接在Dynamic Media Classic (Scene7)內容瀏覽器中選取不同的設定。

>[!NOTE]
>
>* 隨選資料夾中的Assets未出現在Dynamic Media Classic (Scene7)內容瀏覽器中。
>* 啟用[安全預覽](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)時，Dynamic Media Classic (Scene7)上已發佈和未發佈的資產都會出現在Dynamic Media Classic (Scene7)內容瀏覽器中。
>* 如果您在內容瀏覽器中看不到&#x200B;**[!UICONTROL Dynamic Media Classic (Scene7)]**&#x200B;或&#x200B;**[!UICONTROL S7]**&#x200B;圖示作為一個選項，您必須[設定Dynamic Media Classic (Scene7)以使用Experience Manager](/help/sites-administering/scene7.md)。
>* 對於視訊，Dynamic Media Classic (Scene7)內容瀏覽器支援：
>   * 最適化視訊集：包含跨多個熒幕無縫播放所需的所有視訊轉譯的容器
>   * 單一MP4視訊
>   * 單一F4V視訊

### 瀏覽內容 {#browsing-content-in-the-classic-ui}

選取&#x200B;**[!UICONTROL S7]**&#x200B;索引標籤，以瀏覽Dynamic Media Classic (Scene7)中的內容。

您可以透過選取組態來變更您正在存取的組態。 資料夾會依選取的組態而變更。

![chlimage_1-64](assets/chlimage_1-64.png)

就像Assets的內容尋找器一樣，您可以搜尋資產和篩選結果。 不過，不同於Assets Finder，在&#x200B;**S7**&#x200B;索引標籤中輸入關鍵字時，檔案名稱&#x200B;**會以**&#x200B;您所輸入的字串開頭，而非&#x200B;**在檔案名稱中包含**&#x200B;關鍵字。

依預設，資產會依檔案名稱顯示。 不過，您也可以依資產型別篩選結果。

>[!NOTE]
>
>對於視訊，WCM的Dynamic Media Classic (Scene7)內容瀏覽器支援：
>
>* 最適化視訊集：包含跨多個熒幕無縫播放所需的所有視訊轉譯的容器
>* 單一MP4視訊
>* 單一F4V視訊
>

### 使用內容瀏覽器搜尋Dynamic Media Classic (Scene7)資產 {#searching-for-scene-assets-with-the-content-browser}

搜尋Dynamic Media Classic (Scene7)資產與搜尋Experience Manager資產類似。 例外情況是，當您搜尋時，實際上是在Dynamic Media Classic (Scene7)系統中看到資產的遠端檢視，而不是直接將資產匯入Experience Manager。

您可以使用傳統UI或觸控最佳化UI來檢視和搜尋資產。 依介面而定，您的搜尋方式會有些微差異。

在任一UI中搜尋時，您可以依據以下條件進行篩選（如觸控最佳化UI中所示）：

**輸入關鍵字** — 您可以依名稱搜尋資產。 在搜尋關鍵字時，您會輸入檔案名稱的開頭為。 例如，輸入「swimming」會尋找任何以那個順序開頭字母的資產檔案名稱。 輸入字詞以尋找資產後，請務必選取`Enter`。

![chlimage_1-65](assets/chlimage_1-65.png)

**資料夾/路徑** — 資料夾的名稱是根據您選取的設定。 您可以透過選取資料夾圖示並選取子資料夾，然後選取核取記號來向下展開至較低層級。

如果您輸入關鍵字並選取資料夾，Experience Manager會搜尋該資料夾及任何子資料夾。 但是，如果您在搜尋時未輸入任何關鍵字，則選取資料夾只會顯示該資料夾中的資產，不包含任何子資料夾。

根據預設，Experience Manager會搜尋選取的資料夾和所有子資料夾。

![chlimage_1-66](assets/chlimage_1-66.png)

**資產型別** — 選取Dynamic Media Classic (Scene7)以瀏覽Dynamic Media Classic (Scene7)內容。 此選項僅在已設定Dynamic Media Classic (Scene7)時可用。

![chlimage_1-67](assets/chlimage_1-67.png)

**組態** — 如果您在Cloud Service中定義了多個Dynamic Media Classic (Scene7)組態，您可以在這裡選取它。 因此，資料夾會根據您選擇的設定而變更。

![chlimage_1-68](assets/chlimage_1-68.png)

**資產型別** — 在Dynamic Media Classic (Scene7)瀏覽器中，您可以篩選結果以納入下列任一專案：影像、範本、視訊和最適化視訊集。 如果您未選取任何資產型別，則「Experience Manager」預設會搜尋所有資產型別。

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* 在傳統UI中，您也可以搜尋&#x200B;**Flash**&#x200B;和&#x200B;**FXG**。 不支援在觸控最佳化UI中篩選這兩個詞語。
>
>* 搜尋視訊時，您會搜尋單一轉譯。 結果會傳回原始轉譯（僅限&#42;.mp4）和編碼的轉譯。
* 搜尋最適化視訊集時，您會搜尋資料夾和所有子資料夾，但前提是您已新增關鍵字至搜尋。 如果您尚未新增關鍵字，Experience Manager不會搜尋子資料夾。
>

**Publish狀態** — 您可以根據發佈狀態來篩選資產：已取消發佈或已發佈。 如果您未選取任何Publish狀態，Experience Manager預設會搜尋所有發佈狀態。

![chlimage_1-70](assets/chlimage_1-70.png)
