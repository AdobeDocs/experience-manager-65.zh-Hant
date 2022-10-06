---
title: 預覽資產
description: 了解如何在Dynamic Media中預覽資產。
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 84f0c406-4ab6-48c7-8223-61a8c3ade363
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 1%

---

# 使用軟體介面預覽資產 {#previewing-assets}

您可以使用「預覽」，查看您所上傳的數位資產在客戶自己的網頁瀏覽器中被客戶檢視時的外觀。 指派給資產的預設內嵌、跨裝置檢視器會用於預覽。

檢視器是各種設定的集合，或 *預設集*，例如檢視器的顯示大小、縮放行為、色彩配置、邊框和字型。 這些預設會決定使用者在電腦畫面和行動裝置上檢視多媒體資產的方式。

除了使用視訊、回轉集和影像集的專用「預覽」功能，您也可以使用您建立的檢視器預設集來預覽資產。 或者，使用影像預設集來預覽影像的轉譯。

* [套用影像預設集](/help/assets/image-presets.md)
* [套用檢視器預設集](/help/assets/viewer-presets.md)

>[!NOTE]
>
>當您在Adobe Experience Manager的網頁（網站）上時，無法在 **編輯** 模式。 按一下以前往「預覽」模式 **[!UICONTROL 預覽]** 在頁面的右上角。

若要在使用者介面中啟用或停用檢視器預設集，請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md).

**若要使用軟體介面預覽資產：**

1. 從 **[!UICONTROL Adobe Experience Manager]**，在 **[!UICONTROL 導覽]** 頁面，選取 **[!UICONTROL 資產]**，然後 **[!UICONTROL 檔案]** 存取資產。
1. 在頁面的右上角附近，從 **[!UICONTROL 檢視]** 下拉清單，選擇 **[!UICONTROL 清單檢視]**.
1. （選用）使用 **[!UICONTROL 類型]** 欄，依您要預覽的類型來排序資產。
1. 在 **[!UICONTROL 標題]** 欄，按一下您要預覽之資產的標題名稱（而非縮圖影像）。
1. 視您所點按的資產類型而定，執行下列任一項作業：


   <table>
    <tbody>
      <tr>
      <td><strong>您點按的資產類型</strong><br /> </td>
      <td><strong>能否在特定轉譯中預覽資產？</strong></td>
      <td><strong>能在檢視器中預覽資產嗎？</strong></td>
      <td> </td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>要在維查看器中預覽3D資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 選擇 <strong>檢視器</strong> 從清單中，然後選擇「維」查看器。</li>
      <li>選擇 <strong>重設</strong> 如果要將影像返回到原始縮放。</li>
      <li>選擇 <strong>全螢幕</strong> 以最大化顯示裝置上的檢視器。</li>
      </ul>
      <p><strong>導航3D場景</strong></p>
      <ul>
      <li><p><strong>轉動3D相機</strong>  — 圍繞3D場景和對象環繞視圖。</p> 滑鼠：按一下左鍵+拖曳 </p> 觸摸屏：按下+拖曳</p></li>
      <li><p><strong>平移您的相機</strong>  — 向左、向右、向上和向下平移視圖。</p> 滑鼠：按一下滑鼠右鍵+拖曳 </p> 觸摸屏：雙指按+拖動</p></li>
      <li><p><strong>縮放您的相機</strong>  — 縮放攝像機，以便在3D場景中移入和移出區域。</p> 滑鼠：滾輪 </p> 觸摸屏：手指夾</p></li>
      <li><p><strong>重新輸入您的相機</strong>  — 圍繞3D場景和對象環繞視圖。</p> 滑鼠：按兩下 </p> 觸摸屏：按兩下</li></ul></td>
      </tr>
      <tr>
      <td><p>影像</p> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>在特定轉譯中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 選擇 <strong>轉譯 </strong>從清單中，選擇要預覽的特定轉譯。</li>
      </ul> <p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 選擇 <strong>檢視器</strong> 從清單中，選取您要套用至資產的檢視器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 表徵圖，以分別增加或減少所選影像的縮放。 選擇 <strong>重設</strong> 如果要將影像返回到原始縮放。<br /> 如果您在觸控式螢幕上，請點選兩下影像以依步驟放大。 達到最大縮放時，請再次點選兩下影像以重設縮放狀態。 拖過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>多媒體</td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>在特定轉譯中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 選擇 <strong>轉譯 </strong>從清單中，選擇要預覽的特定轉譯。</li>
      </ul> <p>選取要預覽的高解析度視訊轉譯可能會導致視訊顯示為截斷。 此問題是因為轉譯預覽會顯示客戶在用於預覽的內嵌檢視器內容中，將看到所有內容的確切解析度。</p> <p>在資產層級預覽最適化視訊集時，轉譯會分組為一個播放體驗。 也就是說，最適化視訊的大小已適當調整，以便在檢視裝置和連線速度的情境下，使用最佳解析度來檢視及播放。<br /> </p> <p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 選擇 <strong>檢視器</strong> 從清單中，選取您要套用至資產的檢視器。</li>
      </ul> </td>
      </tr>
      <tr>
      <td>影像集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 選擇 <strong>檢視器</strong> 從清單中，選取您要套用至資產的檢視器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 表徵圖，以便您可以分別增加或減少所選影像的縮放。 選擇 <strong>重設</strong> 如果要將影像返回到原始縮放。<br /> 如果您在觸控式螢幕上，請點選兩下影像以依步驟放大。 達到最大縮放時，請再次點選兩下影像以重設縮放狀態。 拖過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>回轉集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 選擇 <strong>檢視器</strong> 從清單中，選取您要套用至資產的檢視器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 表徵圖，以分別增加或減少所選影像的縮放。 選擇 <strong>重設</strong> 如果要將影像返回到原始縮放。<br /> 如果您在觸控式螢幕上，請點選兩下影像以依步驟放大。 達到最大縮放時，請再次點選兩下影像以重設縮放狀態。 拖過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>混合媒體集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 選擇 <strong>檢視器</strong> 從清單中，選取您要套用至資產的檢視器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 表徵圖，以分別增加或減少所選影像的縮放。 選擇 <strong>重設</strong> 如果要將影像返回到原始縮放。<br /> 如果您在觸控式螢幕上，請點選兩下影像以依步驟放大。 達到最大縮放時，請再次點選兩下影像以重設縮放狀態。 拖過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>輪播集</td>
      <td>否</td>
      <td>是</td>
      <td><strong>在特定檢視器中預覽資產</strong>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 選取您要套用至資產的檢視器。</li>
      </ul> </td>
      </tr>
      <tr>
      <td>360段視頻<br /> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>在特定轉譯中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，選取圖示以顯示下拉式清單。 選擇 <strong>轉譯</strong>，然後選取您要預覽的轉譯。</li>
      </ul> <p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，選取圖示以顯示下拉式清單。 選擇 <strong>檢視器</strong>，然後選取您要套用至資產的檢視器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 表徵圖，以分別增加或減少所選影像的縮放。 選擇 <strong>重設</strong> 如果要將影像返回到原始縮放。<br /> 如果您在觸控式螢幕上，請點選兩下影像以依步驟放大。 達到最大縮放時，請再次點選兩下影像以重設縮放狀態。 拖過影像以平移。</p> </td>
      </tr>
    </tbody>
    </table>

## 使用鍵盤預覽資產 {#keyboard-navigation-asset-preview}

1. 從「資產」使用者介面，導覽至包含您要預覽之資產的資料夾。

1. 在資料夾中，按 `<Tab>` 鍵盤上的鍵或方向鍵以選取資產。

1. Press `<Enter>` 這樣，您就能在「預覽」模式中開啟選取的資產。

1. 執行下列任一操作：

   * 要放大，請按 `<Tab>` 要將焦點移到放大(+)表徵圖，然後按 `<Enter>` 增量放大一或多次。
   * 要縮小，請按 `<Tab>` 要將焦點移到縮小(-)表徵圖，然後按 `<Enter>` 一次或多次以增量方式縮小。
   * 移動 *放大* 水準或垂直按各自的方向鍵。
   * Press `<Shift>` + `<Tab>` 如此一來，您就能重設檢視，並將焦點放回資產上。
