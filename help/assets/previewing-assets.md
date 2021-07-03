---
title: 預覽資產
description: 了解如何在Dynamic Media中預覽資產
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
feature: 資產管理
role: User, Admin
exl-id: 84f0c406-4ab6-48c7-8223-61a8c3ade363
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 2%

---

# 使用軟體介面預覽資產 {#previewing-assets}

您可以使用「預覽」，查看您所上傳的數位資產在客戶自己的網頁瀏覽器中被客戶檢視時的外觀。 指派給資產的預設內嵌、跨裝置檢視器會用於預覽。

檢視器是各種設定或「預設集」的集合，例如檢視器的顯示大小、縮放行為、色彩配置、邊框、字型等，可決定使用者在其電腦螢幕和行動裝置上檢視多媒體資產的方式。

除了使用視訊、回轉集和影像集的專用「預覽」功能，您也可以使用您建立的檢視器預設集來預覽資產。 或者，使用影像預設集來預覽影像的轉譯。

* [套用影像預設集](/help/assets/image-presets.md)
* [套用檢視器預設集](/help/assets/viewer-presets.md)

>[!NOTE]
>
>當您在AEM的網頁 (網站) 上時，無法在「編輯」模式中預 **覽資產** 。您需要按一下頁面右上角的&#x200B;**預覽**&#x200B;以前往&#x200B;**預覽**&#x200B;模式。

要在用戶介面中啟用或禁用查看器預設，請參閱[管理查看器預設集](/help/assets/managing-viewer-presets.md)。

**使用軟體介面預覽資產**

1. 從&#x200B;**[!UICONTROL Adobe Experience Manager]**，在&#x200B;**[!UICONTROL 導覽]**&#x200B;頁面上，點選&#x200B;**[!UICONTROL 資產]**，然後點選&#x200B;**[!UICONTROL 檔案]**&#x200B;以存取資產。
1. 在頁面的右上角，從&#x200B;**[!UICONTROL View]**&#x200B;下拉式清單中，點選&#x200B;**[!UICONTROL List View]**。
1. （選用）使用&#x200B;**[!UICONTROL Type]**&#x200B;欄，依您要預覽的類型來排序資產。
1. 在&#x200B;**[!UICONTROL Title]**&#x200B;欄下，按一下您要預覽之資產的標題名稱（而非縮圖影像）。
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
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 按一下清單中的<strong>檢視器</strong>，然後選取維度檢視器。</li>
      <li>點選<strong>重設</strong>以將影像傳回原始縮放。</li>
      <li>點選<strong>全螢幕</strong>以最大化顯示裝置上的檢視器。</li>
      </ul>
      <p><strong>導航3D場景</strong></p>
      <ul>
      <li><p><strong>旋轉3D相機</strong>  — 圍繞3D場景和對象環繞視圖。</p> 滑鼠：按一下左鍵+拖曳。 </p> 觸摸屏：按+拖曳。</p></li>
      <li><p><strong>平移相機</strong>  — 向左、向右、向上和向下平移視圖。</p> 滑鼠：按一下右鍵+拖動。 </p> 觸摸屏：用雙指按+拖。</p></li>
      <li><p><strong>縮放相機</strong>  — 縮放相機以在3D場景中移入和移出區域。</p> 滑鼠：滾輪。 </p> 觸摸屏：手指捏。</p></li>
      <li><p><strong>重新進入相機</strong>  — 圍繞3D場景和對象環繞視圖。</p> 滑鼠：按兩下。 </p> 觸摸屏：點兩下。</li></ul></td>
      </tr>
      <tr>
      <td><p>影像</p> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>在特定轉譯中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 按一下清單中的「<strong>轉譯</strong>」 ，然後選取您要預覽的特定轉譯。</li>
      </ul> <p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 按一下清單中的「<strong>檢視器</strong>」 ，然後選取您要套用至資產的檢視器。</li>
      </ul> <p>使用<strong>+</strong>和<strong>-</strong>表徵圖分別增加或減少所選影像的縮放。 按一下<strong>重設</strong>將影像返回到原始縮放。<br /> 如果您在觸控式螢幕上，請點選兩下影像以依步驟放大。達到最大縮放時，請再次點選兩下影像以重設縮放狀態。 拖過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>多媒體</td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>在特定轉譯中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 按一下清單中的「<strong>轉譯</strong>」 ，然後選取您要預覽的特定轉譯。</li>
      </ul> <p>選取要預覽的高解析度視訊轉譯可能會導致視訊顯示為截斷。 這是因為轉譯預覽會在用於預覽的內嵌檢視器內容中，顯示客戶將看到的確切解析度。</p> <p>在資產層級預覽最適化視訊集時，轉譯會分組為一個播放體驗。 也就是說，最適化視訊的大小已適當調整，以便在檢視裝置和連線速度的情境下，使用最佳解析度來檢視及播放。<br /> </p> <p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 按一下清單中的「<strong>檢視器</strong>」 ，然後選取您要套用至資產的檢視器。</li>
      </ul> </td>
      </tr>
      <tr>
      <td>影像集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 按一下清單中的「<strong>檢視器</strong>」 ，然後選取您要套用至資產的檢視器。</li>
      </ul> <p>使用<strong>+</strong>和<strong>-</strong>表徵圖分別增加或減少所選影像的縮放。 按一下<strong>重設</strong>將影像返回到原始縮放。<br /> 如果您在觸控式螢幕上，請點選兩下影像以依步驟放大。達到最大縮放時，請再次點選兩下影像以重設縮放狀態。 拖過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>回轉集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 按一下清單中的「<strong>檢視器</strong>」 ，然後選取您要套用至資產的檢視器。</li>
      </ul> <p>使用<strong>+</strong>和<strong>-</strong>表徵圖分別增加或減少所選影像的縮放。 按一下<strong>重設</strong>將影像返回到原始縮放。<br /> 如果您在觸控式螢幕上，請點選兩下影像以依步驟放大。達到最大縮放時，請再次點選兩下影像以重設縮放狀態。 拖過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>混合媒體集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，按一下圖示以顯示下拉式清單。 按一下清單中的「<strong>檢視器</strong>」 ，然後選取您要套用至資產的檢視器。</li>
      </ul> <p>使用<strong>+</strong>和<strong>-</strong>表徵圖分別增加或減少所選影像的縮放。 按一下<strong>重設</strong>將影像返回到原始縮放。<br /> 如果您在觸控式螢幕上，請點選兩下影像以依步驟放大。達到最大縮放時，請再次點選兩下影像以重設縮放狀態。 拖過影像以平移。</p> </td>
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
      <td>360視頻<br /> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>在特定轉譯中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，點選圖示以顯示下拉式清單。 選擇「<strong>轉譯</strong>」，然後選擇要預覽的轉譯。</li>
      </ul> <p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面的左上角附近，點選圖示以顯示下拉式清單。 選取「<strong>檢視器</strong>」，然後選取您要套用至資產的檢視器。</li>
      </ul> <p>使用<strong>+</strong>和<strong>-</strong>表徵圖分別增加或減少所選影像的縮放。 按一下<strong>重設</strong>將影像返回到原始縮放。<br /> 如果您在觸控式螢幕上，請點選兩下影像以依步驟放大。達到最大縮放時，請再次點選兩下影像以重設縮放狀態。 拖過影像以平移。</p> </td>
      </tr>
    </tbody>
    </table>

## 使用鍵盤預覽資產 {#keyboard-navigation-asset-preview}

1. 從「資產」使用者介面，導覽至包含您要預覽之資產的資料夾。

1. 在資料夾中，按鍵盤上的`<Tab>`鍵或箭頭鍵以選取資產。

1. 按`<Enter>`以在預覽模式中開啟選取的資產。

1. 執行下列任一操作：

   * 要放大，請按`<Tab>`將焦點移動到放大(+)表徵圖，然後按`<Enter>`一次或多次以增量方式放大。

   * 要縮小，請按`<Tab>`將焦點移到縮小(-)表徵圖，然後按`<Enter>`一次或多次以增量方式縮小。

   * 若要水準或垂直移動&#x200B;*縮放*&#x200B;資產的檢視，請按各自的方向鍵。

   * 按`<Shift>` + `<Tab>`重設檢視並將焦點放回資產上。
