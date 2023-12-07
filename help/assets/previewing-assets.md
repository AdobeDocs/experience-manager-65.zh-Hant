---
title: 預覽資產
description: 瞭解如何套用影像預設集和檢視器預設集，以在Dynamic Media中預覽資產（例如視訊和影像）。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 84f0c406-4ab6-48c7-8223-61a8c3ade363
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 1%

---

# 使用軟體介面預覽資產 {#previewing-assets}

您可以使用「預覽」，檢視客戶在自己的Web瀏覽器中檢視您上傳的數位資產時，該資產的外觀。 指派給資產的預設內嵌跨裝置檢視器會用於預覽。

檢視器是各種設定的集合，或 *預設集*，例如檢視器顯示大小、縮放行為、色彩配置、邊框和字型。 這些預設集可決定使用者在其電腦熒幕和行動裝置上檢視多媒體資產的方式。

除了針對視訊、迴轉集及影像集使用專用的預覽功能外，您也可以使用您建立的檢視器預設集來預覽資產。 或者，使用影像預設集來預覽影像的轉譯。

* [套用影像預設集](/help/assets/image-presets.md)
* [套用檢視器預設集](/help/assets/viewer-presets.md)

>[!NOTE]
>
>當您在Adobe Experience Manager的網頁（網站）上時，無法預覽資產 **編輯** 模式。 按一下「 」以前往「預覽」模式 **[!UICONTROL 預覽]** 位於頁面的右上角。

若要在使用者介面中啟用或停用檢視器預設集，請參閱 [管理檢視器預設集](/help/assets/managing-viewer-presets.md).

**若要使用軟體介面預覽資產：**

1. 從 **[!UICONTROL Adobe Experience Manager]**，位於 **[!UICONTROL 導覽]** 頁面，選取 **[!UICONTROL 資產]**，然後 **[!UICONTROL 檔案]** 以存取資產。
1. 在頁面的右上角附近，從 **[!UICONTROL 檢視]** 下拉式清單，選取 **[!UICONTROL 清單檢視]**.
1. （選用）使用 **[!UICONTROL 型別]** 欄，依您要預覽的型別排序資產。
1. 在 **[!UICONTROL 標題]** 欄，按一下您要預覽之資產的標題名稱（而非縮圖影像）。
1. 請根據您點按的資產型別，執行下列任一項作業：


   <table>
    <tbody>
      <tr>
      <td><strong>您點按的資產型別</strong><br /> </td>
      <td><strong>是否能夠預覽特定轉譯中的資產？</strong></td>
      <td><strong>是否能在檢視器中預覽資產？</strong></td>
      <td> </td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>若要在維度檢視器中預覽3D資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下圖示以顯示下拉式清單。 選取 <strong>檢視者</strong> 從清單中，然後選取「維度」檢視器。</li>
      <li>選取 <strong>重設</strong> 如果要將影像恢復為原始縮放。</li>
      <li>選取 <strong>全熒幕</strong> 以最大化顯示裝置上的檢視器。</li>
      </ul>
      <p><strong>導覽3D場景</strong></p>
      <ul>
      <li><p><strong>轉動您的3D攝影機</strong>  — 讓檢視畫面在3D場景和物件周圍環繞。</p> 滑鼠：按一下左鍵+拖曳 </p> 觸控熒幕：按下+拖曳</p></li>
      <li><p><strong>平移相機</strong>  — 上下左右平移檢視。</p> 滑鼠：按一下右鍵+拖曳 </p> 觸控熒幕：雙指按下+拖曳</p></li>
      <li><p><strong>縮放相機</strong>  — 縮放相機，讓您能夠進出3D場景中的區域。</p> 滑鼠：捲動滾輪 </p> 觸控熒幕：手指捏合</p></li>
      <li><p><strong>重新將相機置中</strong>  — 讓檢視畫面在3D場景和物件周圍環繞。</p> 滑鼠：按兩下 </p> 觸控熒幕：雙選</li></ul></td>
      </tr>
      <tr>
      <td><p>影像</p> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>預覽特定轉譯中的資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下圖示以顯示下拉式清單。 選取 <strong>轉譯 </strong>從清單中，選取您要預覽的特定轉譯。</li>
      </ul> <p><strong>若要在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下圖示以顯示下拉式清單。 選取 <strong>檢視者</strong> 從清單中，選取您要套用至資產的檢視器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 圖示可分別增加或減少所選影像的縮放。 選取 <strong>重設</strong> 如果要將影像恢復為原始縮放。<br /> 如果您在觸控熒幕上，請按兩下要以步驟放大影像。 當您達到最大縮放時，請再次連按兩下影像以重設縮放狀態。 拖移過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>多媒體</td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>預覽特定轉譯中的資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下圖示以顯示下拉式清單。 選取 <strong>轉譯 </strong>從清單中，選取您要預覽的特定轉譯。</li>
      </ul> <p>選取較高解析度的視訊轉譯進行預覽，可能會導致視訊顯示為截斷。 此問題是因為轉譯預覽會在用於預覽的內嵌檢視器內容中，顯示您的客戶將會看到的全部的確切解析度。</p> <p>在資產層級預覽最適化視訊集時，轉譯會分組到一個播放體驗中。 也就是說，最適化視訊的大小適合檢視，並在您的檢視裝置和連線速度環境下使用最佳解析度進行播放。<br /> </p> <p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下圖示以顯示下拉式清單。 選取 <strong>檢視者</strong> 從清單中，選取您要套用至資產的檢視器。</li>
      </ul> </td>
      </tr>
      <tr>
      <td>影像集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下圖示以顯示下拉式清單。 選取 <strong>檢視者</strong> 從清單中，選取您要套用至資產的檢視器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 圖示，讓您分別增加或減少選取影像的縮放。 選取 <strong>重設</strong> 如果要將影像恢復為原始縮放。<br /> 如果您在觸控熒幕上，請按兩下要以步驟放大影像。 當您達到最大縮放時，請再次連按兩下影像以重設縮放狀態。 拖移過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>迴轉集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下圖示以顯示下拉式清單。 選取 <strong>檢視者</strong> 從清單中，選取您要套用至資產的檢視器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 圖示可分別增加或減少所選影像的縮放。 選取 <strong>重設</strong> 如果要將影像恢復為原始縮放。<br /> 如果您在觸控熒幕上，請按兩下要以步驟放大影像。 當您達到最大縮放時，請再次連按兩下影像以重設縮放狀態。 拖移過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>混合媒體集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下圖示以顯示下拉式清單。 選取 <strong>檢視者</strong> 從清單中，選取您要套用至資產的檢視器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 圖示可分別增加或減少所選影像的縮放。 選取 <strong>重設</strong> 如果要將影像恢復為原始縮放。<br /> 如果您在觸控熒幕上，請按兩下要以步驟放大影像。 當您達到最大縮放時，請再次連按兩下影像以重設縮放狀態。 拖移過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>傳送集</td>
      <td>否</td>
      <td>是</td>
      <td><strong>在特定檢視器中預覽資產</strong>
      <ul>
      <li>在頁面左上角附近，按一下圖示以顯示下拉式清單。 選取您要套用至資產的檢視器。</li>
      </ul> </td>
      </tr>
      <tr>
      <td>360度影片<br /> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>預覽特定轉譯中的資產</strong></p>
      <ul>
      <li>在頁面左上角附近，選取圖示以顯示下拉式清單。 選取 <strong>轉譯</strong>，然後選取您要預覽的轉譯。</li>
      </ul> <p><strong>若要在特定檢視器中預覽資產</strong></p>
      <ul>
      <li>在頁面左上角附近，選取圖示以顯示下拉式清單。 選取 <strong>檢視者</strong>，然後選取您要套用至資產的檢視器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 圖示可分別增加或減少所選影像的縮放。 選取 <strong>重設</strong> 如果要將影像恢復為原始縮放。<br /> 如果您在觸控熒幕上，請按兩下要以步驟放大影像。 當您達到最大縮放時，請再次連按兩下影像以重設縮放狀態。 拖移過影像以平移。</p> </td>
      </tr>
    </tbody>
    </table>

## 使用鍵盤預覽資產 {#keyboard-navigation-asset-preview}

1. 從「資產」使用者介面，導覽至包含您要預覽之資產的檔案夾。

1. 在資料夾中，按下 `<Tab>` 使用鍵盤上的鍵或方向鍵來選取資產。

1. 按下 `<Enter>` 以便您在預覽模式中開啟選取的資產。

1. 執行下列任一項作業：

   * 若要放大顯示，請按 `<Tab>` 若要將焦點移至放大顯示(+)圖示，請按下 `<Enter>` 一次或多次，以遞增方式放大。
   * 若要縮小顯示，請按 `<Tab>` 若要將焦點移至縮小顯示(-)圖示，請按下 `<Enter>` 一次或多次，以遞增方式縮小。
   * 若要移動檢視 *已縮放* 水平或垂直方向按各自的方向鍵。
   * 按下 `<Shift>` + `<Tab>` 以便重設檢視並將焦點放回資產。
