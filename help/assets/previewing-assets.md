---
title: 預覽資產
description: 瞭解如何在Dynamic Media預覽資產。
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

您可以使用「預覽」查看您上傳的數字資產在客戶在自己的Web瀏覽器中查看時的外觀。 分配給資產的預設嵌入式跨設備查看器用於預覽。

查看器是各種設定的集合，或 *預設*，如查看器顯示大小、縮放行為、顏色方案、邊框和字型。 這些預設決定了用戶如何在他們的電腦螢幕和移動設備上查看富媒體資產。

除了為視頻、旋轉集和影像集使用專用的「預覽」功能外，還可以使用已建立的查看器預設來預覽資產。 或者，使用影像預設來預覽影像的格式副本。

* [應用影像預設](/help/assets/image-presets.md)
* [應用查看器預設](/help/assets/viewer-presets.md)

>[!NOTE]
>
>在Adobe Experience Manager的網頁（站點）上，無法在 **編輯** 的子菜單。 按一下以轉到「預覽」模式 **[!UICONTROL 預覽]** 的右上角。

要在用戶介面中啟用或禁用查看器預設，請參見 [管理查看器預設](/help/assets/managing-viewer-presets.md)。

**要使用軟體介面預覽資產，請執行以下操作：**

1. 從 **[!UICONTROL Adobe Experience Manager]**&#x200B;的 **[!UICONTROL 導航]** ，選擇 **[!UICONTROL 資產]**，則 **[!UICONTROL 檔案]** 訪問資產。
1. 在頁面右上角，從 **[!UICONTROL 視圖]** 下拉清單，選擇 **[!UICONTROL 清單視圖]**。
1. （可選）使用 **[!UICONTROL 類型]** 列，按要預覽的類型對資產排序。
1. 在 **[!UICONTROL 標題]** 列，按一下要預覽的資產的標題名稱（而不是縮略圖）。
1. 根據您按一下的資產類型，執行以下任一操作：


   <table>
    <tbody>
      <tr>
      <td><strong>您按一下的資產類型</strong><br /> </td>
      <td><strong>是否能夠預覽特定格式副本中的資產？</strong></td>
      <td><strong>是否能夠在查看器中預覽資產？</strong></td>
      <td> </td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在維查看器中預覽3D資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下表徵圖以顯示下拉清單。 選擇 <strong>查看者</strong> 從清單中，然後選擇維查看器。</li>
      <li>選擇 <strong>重置</strong> 的子菜單。</li>
      <li>選擇 <strong>全屏</strong> 以最大化顯示設備上的查看器。</li>
      </ul>
      <p><strong>導航3D場景</strong></p>
      <ul>
      <li><p><strong>開啟3D相機</strong>  — 圍繞3D場景和對象環繞視圖。</p> 滑鼠：左鍵按一下+拖動 </p> 觸摸屏：按+拖動</p></li>
      <li><p><strong>開啟你的相機</strong>  — 左、右、上和下平移視圖。</p> 滑鼠：按一下右鍵並拖動 </p> 觸摸屏：雙指按+拖動</p></li>
      <li><p><strong>縮放相機</strong>  — 縮放相機，以便在3D場景中移入和移出區域。</p> 滑鼠：滾輪 </p> 觸摸屏：手指捏</p></li>
      <li><p><strong>重新輸入相機</strong>  — 圍繞3D場景和對象環繞視圖。</p> 滑鼠：按兩下 </p> 觸摸屏：按兩下</li></ul></td>
      </tr>
      <tr>
      <td><p>影像</p> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>在特定格式副本中預覽資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下表徵圖以顯示下拉清單。 選擇 <strong>格式副本 </strong>從清單中，選擇要預覽的特定格式副本。</li>
      </ul> <p><strong>在特定查看器中預覽資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下表徵圖以顯示下拉清單。 選擇 <strong>查看者</strong> 從清單中，選擇要應用於資產的查看器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 表徵圖，以分別增加或減小所選影像的縮放。 選擇 <strong>重置</strong> 的子菜單。<br /> 如果在觸摸屏上，請按兩下影像以按步驟放大。 達到最大縮放時，再次按兩下影像以重置縮放狀態。 拖過影像進行平移。</p> </td>
      </tr>
      <tr>
      <td>多媒體</td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>在特定格式副本中預覽資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下表徵圖以顯示下拉清單。 選擇 <strong>格式副本 </strong>從清單中，選擇要預覽的特定格式副本。</li>
      </ul> <p>選擇要預覽的高解析度視頻格式副本可能會導致視頻出現截斷。 此問題是因為格式副本預覽會向您顯示客戶在用於預覽的嵌入式查看器上下文中將看到的全部精確解析度。</p> <p>在「資產」級別預覽自適應視頻集時，格式副本將分組到一個回放體驗中。 也就是說，自適應視頻的大小適合在觀看設備和連接速度的上下文中使用最佳解析度進行觀看和回放。<br /> </p> <p><strong>在特定查看器中預覽資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下表徵圖以顯示下拉清單。 選擇 <strong>查看者</strong> 從清單中，選擇要應用於資產的查看器。</li>
      </ul> </td>
      </tr>
      <tr>
      <td>影像集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定查看器中預覽資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下表徵圖以顯示下拉清單。 選擇 <strong>查看者</strong> 從清單中，選擇要應用於資產的查看器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 表徵圖，以便您可以分別增大或減小所選影像的縮放比例。 選擇 <strong>重置</strong> 的子菜單。<br /> 如果在觸摸屏上，請按兩下影像以按步驟放大。 達到最大縮放時，再次按兩下影像以重置縮放狀態。 拖過影像進行平移。</p> </td>
      </tr>
      <tr>
      <td>旋轉集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定查看器中預覽資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下表徵圖以顯示下拉清單。 選擇 <strong>查看者</strong> 從清單中，選擇要應用於資產的查看器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 表徵圖，以分別增加或減小所選影像的縮放。 選擇 <strong>重置</strong> 的子菜單。<br /> 如果在觸摸屏上，請按兩下影像以按步驟放大。 達到最大縮放時，再次按兩下影像以重置縮放狀態。 拖過影像進行平移。</p> </td>
      </tr>
      <tr>
      <td>混合媒體集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定查看器中預覽資產</strong></p>
      <ul>
      <li>在頁面左上角附近，按一下表徵圖以顯示下拉清單。 選擇 <strong>查看者</strong> 從清單中，選擇要應用於資產的查看器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 表徵圖，以分別增加或減小所選影像的縮放。 選擇 <strong>重置</strong> 的子菜單。<br /> 如果在觸摸屏上，請按兩下影像以按步驟放大。 達到最大縮放時，再次按兩下影像以重置縮放狀態。 拖過影像進行平移。</p> </td>
      </tr>
      <tr>
      <td>旋轉木馬組</td>
      <td>否</td>
      <td>是</td>
      <td><strong>在特定查看器中預覽資產</strong>
      <ul>
      <li>在頁面左上角附近，按一下表徵圖以顯示下拉清單。 選擇要應用於資產的查看器。</li>
      </ul> </td>
      </tr>
      <tr>
      <td>360視頻<br /> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>在特定格式副本中預覽資產</strong></p>
      <ul>
      <li>在頁面左上角附近，選擇表徵圖以顯示下拉清單。 選擇 <strong>格式副本</strong>，然後選擇要預覽的格式副本。</li>
      </ul> <p><strong>在特定查看器中預覽資產</strong></p>
      <ul>
      <li>在頁面左上角附近，選擇表徵圖以顯示下拉清單。 選擇 <strong>查看者</strong>，然後選擇要應用於資產的查看器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 表徵圖，以分別增加或減小所選影像的縮放。 選擇 <strong>重置</strong> 的子菜單。<br /> 如果在觸摸屏上，請按兩下影像以按步驟放大。 達到最大縮放時，再次按兩下影像以重置縮放狀態。 拖過影像進行平移。</p> </td>
      </tr>
    </tbody>
    </table>

## 使用鍵盤預覽資產 {#keyboard-navigation-asset-preview}

1. 從「資產」用戶介面，導航到包含要預覽的資產的資料夾。

1. 在資料夾中，按 `<Tab>` 鍵盤上的鍵或箭頭鍵以選擇資產。

1. 按 `<Enter>` 這樣，您就可以在「預覽」模式下開啟選定的資產。

1. 執行下列任一操作：

   * 要放大，請按 `<Tab>` 將焦點移到放大(+)表徵圖，然後按 `<Enter>` 增量放大一次或多次。
   * 要縮小，請按 `<Tab>` 將焦點移到縮小(-)表徵圖，然後按 `<Enter>` 逐步縮小。
   * 移動視圖 *已* 沿水準或垂直方向按相應的箭頭鍵。
   * 按 `<Shift>` + `<Tab>` 這樣您就可以重置視圖並將焦點放回資產上。
