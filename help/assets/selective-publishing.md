---
title: 在動態媒體中使用選擇性發佈
description: 有關如何在動態媒體中使用選擇性發佈的資訊。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 4a144e53217c4353818d778415cc303b21412566
workflow-type: tm+mt
source-wordcount: '2934'
ht-degree: 3%

---


# 在動態媒體的資料夾層級設定選擇性發佈 {#selective-publish-configure-folder}

您可以選擇使用「管理出版物」或「快速發佈」，在檔案夾層級將資產發佈或從AEM或動態媒體取消發佈，而不是只依賴 **[!UICONTROL Dynamic Media Configuration]********** ，其設定對動態媒體例項的所有檔案夾都是全域性的。

例如，透過選擇性發佈，您可以針對尚未上線的產品處理資產。 在這種情況下，行銷團隊可以存取與動態媒體同步的智慧型裁切影像和動態轉譯，以便建立促銷文宣，完全不需要將這些資產發佈至動態媒體以進行全域傳送。

>[!IMPORTANT]
>
>「選擇性發佈」僅適用於動態媒體- Scene7模式。

>[!NOTE]
>
>*將資產復* 制至資料夾或從資料夾複製資產，會清除這些資產的發佈狀態。 不過，當您將資 *產移至*****/從資料夾屬性設為「選擇性發佈」的檔案夾移出或移出時，這些資產的發佈狀態會維持。

如果您稍後決定變更資料夾中的「 **[!UICONTROL Selective Publish]** 」（選擇性發佈）設定，這些變更只會影響您從該點上傳至該資料夾的新資產。 資料夾中現有資產的發佈狀態會維持原狀，直到您從「快速發佈」或「管理出版物」對話方塊 **[!UICONTROL 手動變更資產]****** 為止。

資料夾層 **[!UICONTROL 級的「動態媒體發佈模式]** 」選項一律預設為「動態媒體設定」中「發佈資產 **[!UICONTROL 」設定中]****[!UICONTROL 的值。]** 但是，本主題中的下列步驟將顯示如何在資料夾級別手動更改此預設值（如以下步驟所述）以覆蓋 **** 動態媒體配置值。

無論您是依賴 **[!UICONTROL Dynamic Configuration中設定的]** Assets **[!UICONTROL 值還是資料夾級別中設定的]** Dynamic Publish模式值，您仍然可以選擇立即發佈、啟動介質 **[!UICONTROL On Dynamic Configuration或Dynamic Publish Selective Media]************[!UICONTROL Publish。]** 例如，您可以在啟動時將 **[!UICONTROL Dynamic Media Configuration中的]** Publish **[!UICONTROL Assets值設為]** Opin Activation **[!UICONTROL ，但是在資料夾層級將]********** Dynamic Media PublishMode值設為Oracle Selective Publish Applizing，反之亦然，依此類推。

在資料夾中設定選擇性發佈後，您可以執行下列任一項作業：

* [使用「管理出版物」，選擇性地將資產發佈至動態媒體或AEM。](#selective-publish-manage-publication)
* [使用「管理出版物」，從動態媒體或AEM選擇性地取消發佈資產。](#selective-unpublish-manage-publication)
* [使用「快速發佈」將資產發佈至動態媒體或AEM。](#quick-publish-aem-dm)
* [透過搜尋結果，選擇性地發佈或取消發佈資產。](#selective-publish-unpublish-search-results)

**若要在動態媒體的資料夾層級設定選擇性發佈**

1. 在AEM中，點選AEM標誌以存取全域導覽主控台。 在左側，點選「導覽」圖示（就在「工具」圖示上方），然後點選「資 **[!UICONTROL 產>檔案」。]**
1. 執行下列任一項作業：
   * 編輯現有資料夾的屬性——在「卡片視圖」、「列視圖」或「清單視圖」中 ************，導航到要編輯其屬性的資料夾。 選擇資料夾，然後在工具欄上按一下「 **[!UICONTROL Properties」。]**
   * 編輯新資料夾的屬性——在頁面右上角的「 **[!UICONTROL 卡片檢視」、「欄檢視]**」或「清單檢視」中，點選「 **********[!UICONTROL 建立>資料夾」。]** 在「建 **[!UICONTROL 立資料夾]** 」對話方塊中，輸入資料夾的標題（必要），然後點選「 **[!UICONTROL 建立」。]** 選擇資料夾，然後在工具欄上按一下「 **[!UICONTROL Properties」。]**

1. 在「同 **[!UICONTROL 步模式]** 」下拉式清單中，選取下列其中一項：

   | 同步模式 | 說明 |
   | --- | --- |
   | **[!UICONTROL 已繼承]** | 資料夾上沒有明確的同步值；而是會繼承其中一個祖先資料夾或動態媒體配置中設定的預設模式的 **[!UICONTROL 同步值。]** 「繼承」的詳 **[!UICONTROL 細狀態]** ，通過工具提示顯示。 |
   | **[!UICONTROL 將此子樹狀結構資料夾的所有項目同步至 dynamicmedia]** | 若要發佈至動態媒體才能成功，資產必須同步至動態媒體。 選取此選項，會在此子樹狀結構中包含所有資產，以同步至動態媒體。 資料夾特定設定會覆寫動態媒體設定中的 **[!UICONTROL 預設設定。]** |
   | **[!UICONTROL 從動態媒體同步中排除此資料夾子樹狀結構中的所有項目]** | 排除此子樹狀結構中的所有資產，使其無法同步至動態媒體。 |

   ![資料夾層級選擇性發佈](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 在「動 **[!UICONTROL 態媒體發佈」模式下]** ，選取一個選項。 請注意，「動 **[!UICONTROL 態媒體發佈」模式]** ，選項一律預設為「動態媒體設定」中 **[!UICONTROL 設定的值。]** 不過，您可以使用下列其中一個選 **[!UICONTROL 項，手動覆寫此預設的「動態媒體設定]** 」值。

   >[!IMPORTANT]
   >
   >請注意，無論您選取的「動態媒體發佈」模式選項為何，您日後對已發佈的資產所做的任何更新 ** ，都會立即發佈這些更新，而不需執行任何使用者動作。

   | 動態媒體發佈模式選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 當資產上傳至此檔案夾時，系統會將資產收錄至AEM並立即提供URL/內嵌。 此選項僅系結至AEM發佈，而且不需要使用者干預來發佈資產。<br>如果您在上 *一步* ，在「同步」模式中選 **[!UICONTROL 擇「從動態媒體同步中排除此資料夾子樹中的所有內容]****** 」，則此選項不可用。 |
   | **[!UICONTROL 啟動時]** | 資產上傳至此檔案夾時，您必須先明確發佈資產，才能提供URL/內嵌連結。 此選項僅系結至AEM發佈。<br>如果您在上 *一步* ，在「同步」模式中選 **[!UICONTROL 擇「從動態媒體同步中排除此資料夾子樹中的所有內容]****** 」，則此選項不可用。 |
   | **[!UICONTROL 選擇性發佈]** | 資產會發佈至您選擇的AEM或Dynamic Media，以便在公共網域中傳送。 兩種發佈方式互斥。  也就是說，您可以將資產發佈到DMS7，以便使用智慧型裁切或動態轉譯等功能。 或者，您可以將資產獨家發佈至AEM，以進行安全預覽；這些相同的資 *產不* 會發佈至DMS7，以便在公共網域中傳送。 如果您在上一步驟的「同步」模式中選取「從動態媒體同步中排除此資料夾子樹狀結構中的所有項目 ******** 」，則此選項不可用。 |

1. 在頁面的右上角，點選「 **[!UICONTROL Save &amp; Close]**」，然後點選「 **[!UICONTROL OK]** 」以返回AEM Assets。

## 使用「管理出版物」，選擇性地將資產發佈至動態媒體或AEM{#selective-publish-manage-publication}

在您可以使用「管理出版物 **[!UICONTROL 」來選擇性地將資產發佈至Dynamic Media或AEM之前，請確定您已將]****[!UICONTROL Dynamic Media Configuration中的「發佈資產」選項設定為]** Selective Publish Configuration ******** ，或在資料夾層級設定選擇性發佈。

請參 [閱在動態媒體的資料夾層級](#configuring-dynamic-media-cloud-services)[建立動態媒體設定或設定選擇性發佈](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>「選擇性發佈」僅適用於動態媒體- Scene7模式。

>[!NOTE]
>
>*將資產復* 制至資料夾或從資料夾複製資產，會清除這些資產的發佈狀態。 不過，當您將資 *產移至*****/從資料夾屬性設為「選擇性發佈」的檔案夾移出或移出時，這些資產的發佈狀態會維持。

**若要使用「管理出版物」選擇性地將資產發佈至動態媒體或AEM**

1. 在AEM中，點選AEM標誌以存取全域導覽主控台。 在左側，點選「導覽」圖示（就在「工具」圖示上方），然後點選「資 **[!UICONTROL 產>檔案」。]**
1. 在「 **[!UICONTROL 卡片檢視]**」、「欄檢視 **[!UICONTROL 」或「清單檢]**&#x200B;視」中 ****，執行下列任一項作業：
   * 導覽至您要發佈其資產的檔案夾。 選取資料夾，然後在工具列上點選「管 **[!UICONTROL 理出版物」。]**  您可能會發現使用「清單檢 **[!UICONTROL 視」很有幫助]** ，以便更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的檔案夾。 開啟檔案夾，然後選取一或多個資產。 在工具列上，點選「管 **[!UICONTROL 理出版物」。]** 您可能會發現使用「清單檢 **[!UICONTROL 視」]** ，以便更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果 **[!UICONTROL 工具列上未顯示「管理出版物]** 」，請改用省略號按鈕，然後從清單選單中選 **[!UICONTROL 取「管理出版物]** 」。

1. 在「管 **[!UICONTROL 理出版物——選項]** 」頁面的「 **[!UICONTROL 動作]**」下，選取您想要的啟動類型。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL 發佈]** （至AEM） | 選取這個選項，將資產發佈至AEM以進行安全預覽。 |
   | **[!UICONTROL 發佈至 Dynamic Media]** | 選取此選項，將資產發佈至動態媒體，以便在公用網域中傳送，或者您可以使用智慧型裁切或動態轉譯等功能。<br>只有在資料夾屬性中 **[!UICONTROL 的「動態媒體發佈]** 」模式設定為「 **[!UICONTROL 選擇性發佈]** 」時，此選項才可用。 |

1. 在「 **[!UICONTROL 排程]**」下方，設定發佈的時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 選取以立即發佈資產。 |
   | **[!UICONTROL 稍後]** | 選擇以在特定日期和時間發佈資產。 |

1. 在「管理出版物」頁面的右上 **[!UICONTROL 角]** ，點選「下 **[!UICONTROL 一步」。]**
1. 在「管 **[!UICONTROL 理出版物——範圍]** 」頁中，執行下列任一操作：
   * 視需要，選取一或多個您要從發佈中移除的資產。
   * 在「管理出版物——範圍」頁 **[!UICONTROL 面的右上角]** ，點選「發佈 **[!UICONTROL 」或「]****[!UICONTROL 發佈至動態媒體」。]**
1. 點選「 **[!UICONTROL 確定」。]**

### 使用「管理出版物」從動態媒體或AEM選擇性地取消發佈資產 {#selective-unpublish-manage-publication}

1. 在AEM中，點選AEM標誌以存取全域導覽主控台。 在左側，點選「導覽」圖示（就在「工具」圖示上方），然後點選「資 **[!UICONTROL 產>檔案」。]**
1. 在「 **[!UICONTROL 卡片檢視]**」、「欄檢視 **[!UICONTROL 」或「清單檢]**&#x200B;視」中 ****，執行下列任一項作業：
   * 導覽至您要解除發佈其資產的檔案夾。 選取資料夾，然後在工具列上點選「管 **[!UICONTROL 理出版物」。]**  您可能會發現使用「清單檢 **[!UICONTROL 視」很有幫助]** ，以便更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要解除發佈其資產的檔案夾。 開啟檔案夾，然後選取一或多個資產。 在工具列上，點選「管 **[!UICONTROL 理出版物」。]** 您可能會發現使用「清單檢 **[!UICONTROL 視」]** ，以便更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果 **[!UICONTROL 工具列上未顯示「管理出版物]** 」，請改用省略號按鈕，然後從清單選單中選 **[!UICONTROL 取「管理出版物]** 」。

1. 在「管 **[!UICONTROL 理出版物——選項]** 」頁面的「動作 ****」下方，選取您想要的停用類型。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL 取消發佈]** （從AEM） | 選取這個選項，可從AEM取消發佈資產。 |
   | **[!UICONTROL 從 Dynamic Media 取消發佈]** | 選取此選項，可從動態媒體取消發佈資產。<br>只有在資料夾屬性中 **[!UICONTROL 的「動態媒體發佈]** 」模式設定為「 **[!UICONTROL 選擇性發佈]** 」時，此選項才可用。 |

1. 在「 **[!UICONTROL 排程]**」下，設定取消啟動的時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 選取以立即取消發佈資產。 |
   | **[!UICONTROL 稍後]** | 選取以取消發佈特定日期和時間的資產。 |

1. 在「管理出版物」頁面的右上 **[!UICONTROL 角]** ，點選「下 **[!UICONTROL 一步」。]**
1. 在「管 **[!UICONTROL 理出版物——範圍]** 」頁中，執行下列任一操作：
   * 選取一或多個要從取消發佈移除的資產。
   * 在「管理出版物——範圍」頁面的右上 **[!UICONTROL 角，點選「從動態媒體取消發佈]****[!UICONTROL 」或「取]****[!UICONTROL 消發佈」。]**
1. 點選「 **[!UICONTROL 確定」。]**

## 使用「快速發佈」將資產發佈至動態媒體或AEM {#quick-publish-aem-dm}

您可以使用「 **[!UICONTROL 快速發佈]** 」進行簡單的資產啟動案例。 **[!UICONTROL 快速發佈]** (Quick Publish)會立即發佈選取的資產，而不需進一步的使用者互動。 因此，任何未發佈的參照也會自動發佈。

>[!NOTE]
>
>若要使 **[!UICONTROL 用「快速發佈]********** 」將資產發佈至Dynamic Media或AEM，請確定已在您的「動態媒體設定」或選取資料夾的檔案夾屬性中啟用「選擇性發佈」。

**若要使用「快速發佈」將資產發佈至動態媒體或AEM**

1. 在AEM中，點選AEM標誌以存取全域導覽主控台。 在頁面的左側，點選「導覽」圖示（就在「工具」圖示上方），然後在頁面的右側點選「資產> **[!UICONTROL 檔案」。]**
1. 在「 **[!UICONTROL 卡片檢視]**」、「欄檢視 **[!UICONTROL 」或「清單檢]**&#x200B;視」中 ****，執行下列任一項作業：
   * 導覽至您要發佈其資產的檔案夾。 選取資料夾，然後在工具列上點選「快 **[!UICONTROL 速發佈」。]**  您可能會發現使用「清單檢 **[!UICONTROL 視」很有幫助]** ，以便更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的檔案夾。 開啟檔案夾，然後選取一或多個資產。 在工具列上，點選「 **[!UICONTROL 快速發佈」。]** 您可能會發現使用「清單檢 **[!UICONTROL 視」]** ，以便更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果 **[!UICONTROL 工具列上未顯示]** 「快速發佈」，請改用省略號按鈕，然後從清單選單中選 **[!UICONTROL 取「快速發佈]** 」。

      ![資料夾層級快速發佈至動態媒體](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 從「快速發佈」功能表清單中，選取 **[!UICONTROL 下列選項之一]** 。

   | 快速發佈選項 | 它的功能 |
   | --- | --- | 
   | 發佈至 AEM | 將選取的資產立即發佈至AEM。 |
   | 發佈至 Brand Portal 網站 | 將選取的資產立即發佈至 **[!UICONTROL 品牌入口網站。]**<br>只有在您的AEM Assets例項已設定品牌入口網站時，**[!UICONTROL &#x200B;才能使用此選項&#x200B;]**。 |
   | 發佈至 Dynamic Media | 立即將選取的資產發佈至動態媒體。<br>資產必須已同步至動態媒體。 如有必要，請確 **[!UICONTROL 定資料夾屬性中的「同步模式]****[!UICONTROL 」已設定為「將此資料夾子樹中的所有內容同步到動態媒體」。]** |

1. 點選「 **[!UICONTROL 確定]**」，然後點選「 **[!UICONTROL 關閉」。]**

## 透過搜尋結果，選擇性地發佈或取消發佈資產 {#selective-publish-unpublish-search-results}

搜尋結果可顯示不同動態媒體發佈設定之資產檔案夾中的資產。 如果您已從搜尋結果中選取一或多個資產，而資產具有不同的動態媒體發佈模式設定，您可以從工具列觸發「管理出版物 **** 」，以進行發佈或取消發佈。

另請參閱「 [在AEM中搜尋資產」。](/help/assets/search-assets.md)

**若要透過搜尋結果選擇性地發佈或取消發佈資產**

1. 在AEM中，在頁面的左上角，點選AEM標誌以存取全域導覽主控台。 在頁面的左側，點選「導覽」圖示（就在「工具」圖示上方），然後點選「資產> **[!UICONTROL 檔案」。]**
1. 在工具列上，在頁面右上角附近點選「搜尋」圖示（放大鏡）。
1. 在「要搜 **[!UICONTROL 尋的類型]** 」文字欄位中，輸入關鍵字，然後按 **[!UICONTROL Enter。]**
1. 在頁面的右上角附近，點選「清單檢視」 **[!UICONTROL 圖示]** 。
1. 在頁面的左上角附近，點選「篩選 **[!UICONTROL 器]** 」圖示。

   ![搜尋結果中的清單檢視和篩選](/help/assets/assets-dm/select-publish-search-result.png)

1. 在左側面板中，展開「 **[!UICONTROL 狀態]**」，然後展開 **** 「動態媒體搜尋謂語」。
1. 使用「已 **[!UICONTROL 發佈]** 」和「未發佈 **** 」核取方塊，根據動態媒體資產的已發佈狀態進一步調整搜尋結果。
或者，您可以搭配使用這些核取方塊與 **[!UICONTROL Publish]** search predicate，來調整 **[!UICONTROL Published]** 和 **[!UICONTROL Unpublished]** AEM資產的搜尋結果。
1. 執行下列任一項作業：
   * 選取一或多個您要發佈或取消發佈的資產。
   * 在「搜尋結果」頁面的右上角 **[!UICONTROL 附近]** ，點選「全 **[!UICONTROL 選」。]**
1. 在工具列上，點選「管 **[!UICONTROL 理出版物」。]** 您可能需要點選工具列上的省略號圖示，才能查看「管 **[!UICONTROL 理出版物」。]**
1. 在「管 **[!UICONTROL 理出版物——選項]** 」頁面上，選取所要的動作。

   | 選取的動作 | 動態媒體設定中的發佈資產設定 | 資產是 |
   | --- | --- | --- |
   | 發佈 | 立即或在啟動時 | 發佈至AEM和動態媒體。 |
   | 發佈 | 選擇性發佈 | 僅發佈至AEM。 |
   | 未發佈 | 立即或在啟動時 | 未從AEM和動態媒體發佈。 |
   | 未發佈 | 選擇性發佈 | 僅從AEM取消發佈。 |
   | 發佈至 Dynamic Media | 立即或在啟動時 | 未發佈至AEM或Dynamic Media，或兩者。 |
   | 發佈至 Dynamic Media | 選擇性發佈 | 僅發佈至動態媒體。 |
   | 從 Dynamic Media 取消發佈 | 立即或在啟動時 | 未從AEM或Dynamic Media或兩者取消發佈。 |
   | 從 Dynamic Media 取消發佈 | 選擇性發佈 | 僅從動態媒體取消發佈。 |

1. 在「 **[!UICONTROL 排程]**」下，設定取消啟動的時間。

   | 選定的計畫 | 發生的事 |
   | --- | --- |
   | 立即 | 會立即執行選取的動作。 |
   | 稍後 | 所選動作會在選取的特定日期和時間執行。 |

1. 在「管理出版物——選項」頁面的右上 **[!UICONTROL 角，點選「下一]** 步」 **[!UICONTROL 。]**
1. （可選）在「管 **[!UICONTROL 理出版物——範圍]** 」頁面中，檢視選定資產 **[!UICONTROL 表格中的「發佈目標]** 」欄。

   | 動態媒體設定中的發佈資產設定 | 選取的動作 | 發佈目標 |
   | --- | --- | --- |
   | 立即或在 <br>啟動時 | 發佈 | AEM和Dynamic Media |
   | 立即或在 <br>啟動時 | 發佈至 Dynamic Media | 無 |
   | 選擇性發佈 | 發佈 | AEM |
   | 選擇性發佈 | 發佈至 Dynamic Media | Dynamic Media |
   | 立即或在 <br>啟動時 | 未發佈 | AEM和Dynamic Media |
   | 立即或在 <br>啟動時 | 從 Dynamic Media 取消發佈 | 無 |
   | 選擇性發佈 | 未發佈 | AEM |
   | 選擇性發佈 | 從 Dynamic Media 取消發佈 | Dynamic Media |

1. 在「管 **[!UICONTROL 理出版物——範圍]** 」頁中，執行下列任一操作：
   * 選取一或多個要從發佈或取消發佈移除的資產。
   * 在「管理出版物——範圍 **[!UICONTROL 」頁面的右上角，點選「發佈]** 」或「 **[!UICONTROL 解除發佈]****** 」以開始動作。
1. 點選「 **[!UICONTROL 確定」。]**

## 檢查資產的發佈狀態 {#check-publish-status-of-asset}

您可以將時間軸與 **[!UICONTROL Card檢視]** 、 **[!UICONTROL Column View]**，或List View **[!UICONTROL in AEM搭配使]****** 用，以快速勾選資產的發佈狀態。

**若要檢查資產的發佈狀態**

1. 在AEM中，在頁面的左上角，點選AEM標誌以存取全域導覽主控台。 在頁面的左側，點選「導覽」圖示（就在「工具」圖示上方），然後點選「資產> **[!UICONTROL 檔案」。]**
1. 在「 **[!UICONTROL 檢視]**」、「欄檢視 **[!UICONTROL 」或「清單檢視」]**(下方的螢幕擷取顯示「清單檢視 ********」卡)中，開啟包含已發佈或未發佈之資產的資料夾。
1. 選取資產，以便以勾號顯示。 請參閱以下螢幕擷取範例。
1. Near the upper-left corner of the page, from the drop-down menu, select **[!UICONTROL Timeline.]** 左側 **[!UICONTROL 面板中的]** 「狀態」區域會顯示所選資產的發佈狀態。
當您使用「 **[!UICONTROL 清單檢視]**」時，會出現另一欄 **[!UICONTROL ，顯示「動態媒體]** 」發佈狀態。
   * 設定為同步至動態媒體的資料夾，預設會顯 **[!UICONTROL 示「動態媒體]** 」欄。
   * 未設定為 *同步至* 「動態媒體」的資料夾將不會顯示「動態媒體」欄。
      ![清單檢視和時間軸](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 疑難排解選擇性發佈 {#selective-publish-troubleshoot}

未同步至動態媒體但在其上觸發動態媒體發佈動作的資產會產生下列錯誤訊息和解決方案：

![選擇性發佈錯誤](/help/assets/assets-dm/selective-publish-error.png)

