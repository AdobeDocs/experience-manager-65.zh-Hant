---
title: 預覽資產
description: 瞭解如何在動態媒體中預覽資產
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 3%

---


# 使用軟體介面預覽資產 {#previewing-assets}

您可以使用「預覽」來查看您上傳的數位資產在客戶在其網頁瀏覽器中檢視時的外觀。 指派給資產的預設內嵌、跨裝置檢視器會用於預覽。

檢視器是各種設定或「預設集」的集合，例如檢視器顯示大小、縮放行為、色彩配置、邊框、字型等，可決定使用者在電腦螢幕和行動裝置上檢視多媒體資產的方式。

除了針對視訊、回轉集和影像集使用專屬的「預覽」功能外，您也可以使用您建立的檢視器預設集來預覽資產。 或者，使用影像預設集來預覽影像的轉譯。

* [套用影像預設集](/help/assets/image-presets.md)
* [套用檢視器預設集](/help/assets/viewer-presets.md)

>[!NOTE]
>
>當您在AEM的網頁 (網站) 上時，無法在「編輯」模式中預 **覽資產** 。You need to go to **Preview** mode by clicking **Preview** in the upper right-hand corner of the page.

若要在使用者介面中啟用或停用檢視器預設集，請參閱「管 [理檢視器預設集」](/help/assets/managing-viewer-presets.md)。

**若要使用軟體介面預覽資產**

1. 在 **[!UICONTROL Adobe Experience Manager**，在 **[!UICONTROL導覽頁面上，點選「資產** 」，然後點選「檔 ******** 案」以存取資產。
1. 在頁面的右上角附近，從「檢視」下拉式清單 **[!UICONTROL 中]** ，點選「清單 **[!UICONTROL 檢視」。]**
1. （可選）使用 **[!UICONTROL Type]** 欄，依您要預覽的類型排序資產。
1. 在「標 **[!UICONTROL 題]** 」欄下方，按一下您要預覽之資產的標題名稱（而非縮圖影像）。
1. 視您所點按的資產類型而定，執行下列任一項作業：


   <table>
    <tbody>
      <tr>
      <td><strong>您點按的資產類型</strong><br /> </td>
      <td><strong>能夠在特定轉譯中預覽資產嗎？</strong></td>
      <td><strong>能夠在檢視器中預覽資產嗎？</strong></td>
      <td> </td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在維度檢視器中預覽3D資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 從清單 <strong>中按一下</strong> 「檢視器」，然後選取「維度檢視器」。</li>
      <li>點選 <strong>「重設</strong> 」，將影像還原為原始縮放。</li>
      <li>點選「 <strong>全螢幕</strong> 」，以最大化顯示裝置上的檢視器。</li>
      </ul>
      <p><strong>導覽3D場景</strong></p>
      <ul>
      <li><p><strong>轉動您的3D相機</strong> -圍繞3D場景和物件環繞視圖。</p> 滑鼠： 左鍵按一下+拖動。 </p> 觸控螢幕： 按+拖曳。</p></li>
      <li><p><strong>平移您的相機</strong> -向左、向右、向上和向下平移您的檢視。</p> 滑鼠： 按一下右鍵+拖動。 </p> 觸控螢幕： 雙指按+拖曳。</p></li>
      <li><p><strong>縮放您的相機</strong> -縮放您的相機，以在3D場景中移入和移出區域。</p> 滑鼠： 滾輪。 </p> 觸控螢幕： 手指捏。</p></li>
      <li><p><strong>重新輸入您的相機</strong> -環繞3D場景和物件環繞視圖。</p> 滑鼠： 按兩下。 </p> 觸控螢幕： 點兩下。</li></ul></td>
      </tr>
      <tr>
      <td><p>影像</p> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>在特定轉譯中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 按一 <strong>下清 </strong>單中的「轉譯」，然後選取您要預覽的特定轉譯。</li>
      </ul> <p><strong>若要在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 按一 <strong>下清單中的</strong> 「檢視器」，然後選取您要套用至資產的檢視器。</li>
      </ul> <p>使用 <strong>+</strong><strong></strong> 和——圖示分別增加或減少所選影像的縮放。 按一 <strong>下「重設</strong> 」，將影像還原為原始縮放。<br /> 如果您是在觸控螢幕上，請點選兩下影像，依步驟放大。 達到最大縮放時，再點兩下影像以重設縮放狀態。 拖曳影像以進行平移。</p> </td>
      </tr>
      <tr>
      <td>多媒體</td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>在特定轉譯中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 按一 <strong>下清 </strong>單中的「轉譯」，然後選取您要預覽的特定轉譯。</li>
      </ul> <p>選取較高解析度的視訊轉譯以進行預覽，可能會導致視訊出現截斷。 這是因為轉譯預覽會在用於預覽的內嵌檢視器中，顯示客戶將看到的精確解析度。</p> <p>當您在「資產」層級預覽最適化視訊集時，轉譯會分組為一個播放體驗。 也就是說，最適化視訊的大小會適當調整，以便在檢視裝置和連線速度時，使用最佳解析度來檢視和播放。<br /> </p> <p><strong>若要在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 按一 <strong>下清單中的</strong> 「檢視器」，然後選取您要套用至資產的檢視器。</li>
      </ul> </td>
      </tr>
      <tr>
      <td>影像集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>若要在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 按一 <strong>下清單中的</strong> 「檢視器」，然後選取您要套用至資產的檢視器。</li>
      </ul> <p>使用 <strong>+</strong><strong></strong> 和——圖示分別增加或減少所選影像的縮放。 按一 <strong>下「重設</strong> 」，將影像還原為原始縮放。<br /> 如果您是在觸控螢幕上，請點選兩下影像，依步驟放大。 達到最大縮放時，再點兩下影像以重設縮放狀態。 拖曳影像以進行平移。</p> </td>
      </tr>
      <tr>
      <td>回轉集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>若要在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 按一 <strong>下清單中的</strong> 「檢視器」，然後選取您要套用至資產的檢視器。</li>
      </ul> <p>使用 <strong>+</strong><strong></strong> 和——圖示分別增加或減少所選影像的縮放。 按一 <strong>下「重設</strong> 」，將影像還原為原始縮放。<br /> 如果您是在觸控螢幕上，請點選兩下影像，依步驟放大。 達到最大縮放時，再點兩下影像以重設縮放狀態。 拖曳影像以進行平移。</p> </td>
      </tr>
      <tr>
      <td>混合媒體集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>若要在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 按一 <strong>下清單中的</strong> 「檢視器」，然後選取您要套用至資產的檢視器。</li>
      </ul> <p>使用 <strong>+</strong><strong></strong> 和——圖示分別增加或減少所選影像的縮放。 按一 <strong>下「重設</strong> 」，將影像還原為原始縮放。<br /> 如果您是在觸控螢幕上，請點選兩下影像，依步驟放大。 達到最大縮放時，再點兩下影像以重設縮放狀態。 拖曳影像以進行平移。</p> </td>
      </tr>
      <tr>
      <td>轉盤集</td>
      <td>否</td>
      <td>是</td>
      <td><strong>若要在特定檢視器中預覽資產</strong>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 選取您要套用至資產的檢視器。</li>
      </ul> </td>
      </tr>
      <tr>
      <td>360 Video<br /> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>在特定轉譯中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近點選圖示，以便顯示下拉式清單。 選取「 <strong>轉譯</strong>」，然後選取您要預覽的轉譯。</li>
      </ul> <p><strong>若要在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近點選圖示，以便顯示下拉式清單。 選取 <strong>檢視器</strong>，然後選取您要套用至資產的檢視器。</li>
      </ul> <p>使用 <strong>+</strong><strong></strong> 和——圖示分別增加或減少所選影像的縮放。 按一 <strong>下「重設</strong> 」，將影像還原為原始縮放。<br /> 如果您是在觸控螢幕上，請點選兩下影像，依步驟放大。 達到最大縮放時，再點兩下影像以重設縮放狀態。 拖曳影像以進行平移。</p> </td>
      </tr>
    </tbody>
    </table>

## 使用鍵盤預覽資產 {#keyboard-navigation-asset-preview}

1. 從「資產」使用者介面，導覽至包含您要預覽之資產的檔案夾。

1. 在資料夾中，按鍵 `<Tab>` 盤上的鍵或箭頭鍵以選取資產。

1. 按 `<Enter>` 以預覽模式開啟選取的資產。

1. 執行下列任一操作：

   * 若要放大，請 `<Tab>` 按以移動焦點至放大(+)圖示，然後按一 `<Enter>` 或多次以遞增方式放大。

   * 若要縮小，請按 `<Tab>` 將焦點移至縮小(-)圖示，然後按一 `<Enter>` 或多次遞增縮小。

   * 若要水準或垂直移動 *縮放* 資產的視圖，請按相應的箭頭鍵。

   * 按 `<Shift>` + `<Tab>` 重設檢視並將焦點放回資產上。
