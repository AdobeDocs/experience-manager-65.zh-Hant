---
title: 在Dynamic Media中使用選擇性發佈
description: 您可以在資料夾層級選擇從Adobe Experience Manager或Dynamic Media發佈或取消發佈資產。 您可以使用「管理出版物」或「快速發佈」，而非僅能依賴在Dynamic Media執行個體使用相同資料夾設定的Dynamic Media組態。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publishing
source-git-commit: 664e22cc4c6acd74f285a4ec1a0dbd7d301240b7
workflow-type: tm+mt
source-wordcount: '3000'
ht-degree: 4%

---

# 在Dynamic Media的資料夾層級設定選擇性發佈 {#selective-publish-configure-folder}

您可以在資料夾層級選擇從Adobe Experience Manager或Dynamic Media發佈或取消發佈資產。 您可以使用 **[!UICONTROL 管理出版物]** 或 **[!UICONTROL 快速發佈]** 而不是只依靠 **[!UICONTROL Dynamic Media設定]** 其設定與Dynamic Media執行個體中的所有資料夾皆為全域。

例如，透過選擇性發佈，您可以針對尚未上線的產品使用資產。 在這種情況下，行銷團隊可以存取同步至Dynamic Media的智慧型裁切影像和動態轉譯。 它們可以製作促銷文宣，而完全不需要將這些資產發佈至Dynamic Media以供全球傳送。

>[!IMPORTANT]
>
>「選擇性發佈」僅適用於Dynamic Media - Scene7模式。

>[!NOTE]
>
>*複製* 資產傳至資料夾和從資料夾清除這些資產的發佈狀態。 不過，若您 *移動* 將資料夾屬性設為的資料夾之間和之間的資產 **[!UICONTROL 選擇性發佈]**，則會維護這些資產的發佈狀態。

如果您稍後決定變更 **[!UICONTROL 選擇性發佈]** 設定時，這些變更只會影響您自此上傳至該資料夾的新資產。 資料夾中現有資產的發佈狀態會維持原狀，直到您手動從 **[!UICONTROL 快速發佈]** 或 **[!UICONTROL 管理出版物]** 對話框。

資料夾層級 **[!UICONTROL Dynamic Media發佈模式]** 選項一律預設為 **[!UICONTROL 發佈資產]** 在 **[!UICONTROL Dynamic Media設定]**. 不過，本主題中的下列步驟會示範如何手動變更資料夾層級的此預設值（如下列步驟所述），以覆寫 **[!UICONTROL Dynamic Media設定]** 值。

無論您是否仰賴下列其中一項：

* **[!UICONTROL 發佈資產]** 值設定 **[!UICONTROL Dynamic Media設定]**.
* **[!UICONTROL Dynamic Media發佈模式]** 在資料夾層級屬性中設定的值。

您可以選擇 **[!UICONTROL 立即]**, **[!UICONTROL 啟動時]**，或 **[!UICONTROL 選擇性發佈]**. 例如，您可以設定 **[!UICONTROL 發佈資產]** 值 **[!UICONTROL Dynamic Media設定]** to **[!UICONTROL 啟動時]**，但設定 **[!UICONTROL Dynamic Media Publish]** 資料夾層級的模式值 **[!UICONTROL 選擇性發佈]**，反之則。

在資料夾中設定選擇性發佈後，您可以執行下列任一操作：

* [使用管理出版物選擇性地將資產發佈至Dynamic Media或Experience Manager](#selective-publish-manage-publication).
* [使用管理出版物從Dynamic Media或Experience Manager選擇性取消發佈資產](#selective-unpublish-manage-publication).
* [使用快速發佈將資產發佈至Dynamic Media或Experience Manager](#quick-publish-aem-dm).
* [透過搜尋結果選擇性地發佈或取消發佈資產](#selective-publish-unpublish-search-results).

**若要在Dynamic Media中在資料夾層級設定選擇性發佈：**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在左側，選取「導覽」圖示（位於「工具」圖示上方），然後選取 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 執行下列任一項作業：
   * 編輯現有資料夾的屬性 — 在 **[!UICONTROL 卡片檢視]**, **[!UICONTROL 欄檢視]**，或 **[!UICONTROL 清單檢視]**，導覽至您要編輯其屬性的資料夾。 選取資料夾，然後在工具列上選取 **[!UICONTROL 屬性]**.
   * 編輯新資料夾的屬性 — 在 **[!UICONTROL 卡片檢視]**, **[!UICONTROL 欄檢視]**，或 **[!UICONTROL 清單檢視]**，在頁面右上角附近，選取 **[!UICONTROL 建立]** > **[!UICONTROL 資料夾]**. 在 **[!UICONTROL 建立資料夾]** 對話框，輸入資料夾的標題（必要），然後選擇 **[!UICONTROL 建立]**. 選取資料夾，然後在工具列上選取 **[!UICONTROL 屬性]**.

1. 在 **[!UICONTROL 同步模式]** 下拉式清單中，選取下列其中一項：

   | 同步模式 | 說明 |
   | --- | --- |
   | **[!UICONTROL 已繼承]** | 資料夾上沒有明確的同步值；相反，資料夾會繼承其上階資料夾中的一個同步值，或繼承您在 **[!UICONTROL Dynamic Media設定]**. 的詳細狀態 **[!UICONTROL 繼承]** 以工具提示顯示。 |
   | **[!UICONTROL 將此資料夾子樹狀結構中的所有項目同步至Dynamic Media]** | 若要發佈至Dynamic Media成功，必須將資產同步至Dynamic Media。 選取此選項會包含此子樹狀結構中要同步至Dynamic Media的所有資產。 資料夾特定設定會覆寫 **[!UICONTROL Dynamic Media設定]**. |
   | **[!UICONTROL 從Dynamic Media同步中排除此資料夾子樹狀結構中的所有項目]** | 排除此子樹狀結構中的所有資產，不得同步至Dynamic Media。 |

   ![資料夾層級選擇性發佈](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 在 **[!UICONTROL Dynamic Media發佈模式]** 下拉式清單中，選取選項。 此 **[!UICONTROL Dynamic Media發佈模式]** 選項一律預設為 **[!UICONTROL Dynamic Media設定]**. 不過，您可以手動覆寫此預設值 **[!UICONTROL Dynamic Media設定]** 值。

   >[!IMPORTANT]
   >
   >無論您選取的Dynamic Media發佈模式選項為何，您之後對以下資產進行的任何更新： *已* 已發佈，則這些更新會立即發佈，而不需進一步使用者動作。
   >
   >如果已發佈的視訊已更新，則必須再次發佈，以反映傳送時的變更。

   | Dynamic Media發佈模式選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 資產上傳至此資料夾時，系統會將資產內嵌至Experience Manager，並立即提供URL/內嵌。 此選項僅與Experience Manager發佈系結，不需要使用者干預即可發佈資產。<br>此選項為 *not* 若已選取，則可用 **[!UICONTROL 從Dynamic Media同步中排除此資料夾子樹狀結構中的所有項目]** in **[!UICONTROL 同步模式]** 中。 |
   | **[!UICONTROL 啟動時]** | 資產上傳至此資料夾時，您必須先明確發佈資產，才能提供URL/內嵌連結。 此選項僅與Experience Manager發佈系結。<br>此選項為 *not* 若已選取，則可用 **[!UICONTROL 從Dynamic Media同步中排除此資料夾子樹狀結構中的所有項目]** in **[!UICONTROL 同步模式]** 中。 |
   | **[!UICONTROL 選擇性發佈]** | 資產會發佈至您選擇的Experience Manager，或發佈至Dynamic Media，以便在公開網域中傳送。 兩種發佈方法彼此互斥。 也就是說，您可以將資產發佈至DMS7，以便使用智慧型裁切或動態轉譯等功能。 或者，您也可以只將資產發佈至Experience Manager，以確保安全預覽；這些資產 *not* 發佈至DMS7供在公共網域中傳遞。 如果您選取「 」，則無法使用此選項 **[!UICONTROL 從Dynamic Media同步中排除此資料夾子樹狀結構中的所有項目]** in **[!UICONTROL 同步模式]** 中。 |

1. 在頁面的右上角，選取 **[!UICONTROL 儲存並關閉]**，然後選取 **[!UICONTROL 確定]** 回到Experience Manager Assets。

## 使用管理出版物選擇性地將資產發佈至Dynamic Media或Experience Manager{#selective-publish-manage-publication}

使用之前 **[!UICONTROL 管理出版物]** 若要選擇性地將資產發佈至Dynamic Media或Experience Manager，請確定您已設定下列其中一項：

* 此 **[!UICONTROL 發佈資產]** 選項 **[!UICONTROL Dynamic Media設定]** to **[!UICONTROL 選擇性發佈]**
* 在資料夾層級設定選擇性發佈。

請參閱 [建立Dynamic Media設定](#configuring-dynamic-media-cloud-services) 或 [在Dynamic Media的資料夾層級設定選擇性發佈](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>「選擇性發佈」僅適用於Dynamic Media - Scene7模式。

>[!NOTE]
>
>*複製* 資產傳至資料夾和從資料夾清除這些資產的發佈狀態。 不過，若您 *移動* 將資料夾屬性設為的資料夾之間和之間的資產 **[!UICONTROL 選擇性發佈]**，則會維護這些資產的發佈狀態。

**若要使用「管理出版物」選擇性地將資產發佈至Dynamic Media或Experience Manager:**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在左側，選取「導覽」圖示（位於「工具」圖示上方），然後選取 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 在 **[!UICONTROL 卡片檢視]**, **[!UICONTROL 欄檢視]**，或 **[!UICONTROL 清單檢視]**，執行下列其中一項操作：
   * 導覽至您要發佈其資產的資料夾。 選取資料夾，然後在工具列上選取 **[!UICONTROL 管理出版物]**. 使用 **[!UICONTROL 清單檢視]** 以便您更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的資料夾。 開啟資料夾，然後選取一或多個資產。 在工具列上，選取 **[!UICONTROL 管理出版物]**. 使用 **[!UICONTROL 清單檢視]** 以便您更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >若 **[!UICONTROL 管理出版物]** 工具列上未顯示，請改為選取省略號按鈕，然後選取 **[!UICONTROL 管理出版物]** 的上界。

1. 在 **[!UICONTROL 管理出版物 — 選項]** 頁面下方 **[!UICONTROL 動作]**，請選取您要的啟動類型。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL 發佈]** (至Experience Manager) | 選取此選項，即可將資產發佈至Experience Manager，以便安全預覽。 |
   | **[!UICONTROL 發佈至 Dynamic Media]** | 選取此選項，即可將資產發佈至Dynamic Media以在公用網域中傳送，或是使用智慧型裁切或動態轉譯等功能。<br>只有在 **[!UICONTROL Dynamic Media發佈模式]** 設為 **[!UICONTROL 選擇性發佈]** 中。 |

1. 在 **[!UICONTROL 排程]**，設定發佈的時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 選取以立即發佈資產。 |
   | **[!UICONTROL 稍後]** | 選取以在特定日期和時間發佈資產。 |

1. 位於 **[!UICONTROL 管理出版物]** 頁面，選取 **[!UICONTROL 下一個]**.
1. 在 **[!UICONTROL 管理發布 — 範圍]** 頁面，執行下列任一操作：

   * 如有必要，請選取一或多個您要從發佈中移除的資產。
   * 位於 **[!UICONTROL 管理發布 — 範圍]** 頁面，選取 **[!UICONTROL 發佈]** 或 **[!UICONTROL 發佈至Dynamic Media]**.
1. 選擇 **[!UICONTROL 確定]**.

### 使用管理出版物從Dynamic Media或Experience Manager選擇性取消發佈資產 {#selective-unpublish-manage-publication}

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在左側，選取「導覽」圖示（位於「工具」圖示上方），然後選取 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 在 **[!UICONTROL 卡片檢視]**, **[!UICONTROL 欄檢視]**，或 **[!UICONTROL 清單檢視]**，執行下列其中一項操作：
   * 導覽至您要取消發佈其資產的資料夾。 選取資料夾，然後在工具列上選取 **[!UICONTROL 管理出版物]**. 使用 **[!UICONTROL 清單檢視]** 以便您更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要取消發佈其資產的資料夾。 開啟資料夾，然後選取一或多個資產。 在工具列上，選取 **[!UICONTROL 管理出版物]**. 使用 **[!UICONTROL 清單檢視]** 以便您更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >若 **[!UICONTROL 管理出版物]** 工具列上未顯示，請改為選取省略號按鈕，然後選取 **[!UICONTROL 管理出版物]** 的上界。

1. 在 **[!UICONTROL 管理出版物 — 選項]** 頁面下方 **[!UICONTROL 動作]**，請選取您想要的停用類型。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL 取消發佈]** (來自Experience Manager) | 如果您要從Experience Manager取消發佈資產，請選取此選項。 |
   | **[!UICONTROL 從 Dynamic Media 取消發佈]** | 如果您要從Dynamic Media取消發佈資產，請選取此選項。<br>只有在 **[!UICONTROL Dynamic Media發佈模式]** 設為 **[!UICONTROL 選擇性發佈]** 中。 |

1. 在 **[!UICONTROL 排程]**，設定取消啟用的時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 選取以立即取消發佈資產。 |
   | **[!UICONTROL 稍後]** | 選取，在特定日期和時間取消發佈資產。 |

1. 位於 **[!UICONTROL 管理出版物]** 頁面，選取 **[!UICONTROL 下一個]**.
1. 在 **[!UICONTROL 管理發布 — 範圍]** 頁面，執行下列任一操作：
   * 選取您要從取消發佈中移除的一或多個資產。
   * 位於 **[!UICONTROL 管理發布 — 範圍]** 頁面，選取 **[!UICONTROL 取消發佈]** 或 **[!UICONTROL 從Dynamic Media取消發佈]**.
1. 選擇 **[!UICONTROL 確定]**.

## 使用快速發佈將資產發佈至Dynamic Media或Experience Manager {#quick-publish-aem-dm}

您可以使用 **[!UICONTROL 快速發佈]** 適用於簡單的資產啟用案例。 **[!UICONTROL 快速發佈]** 立即發佈所選資產，而不需進一步進行使用者互動。 由於此動作，任何未發佈的參考也會自動發佈。

>[!NOTE]
>
>使用 **[!UICONTROL 快速發佈]** 若要將資產發佈至Dynamic Media或Experience Manager，請確定 **[!UICONTROL 選擇性發佈]** 在 **[!UICONTROL Dynamic Media設定]** 或在所選資料夾的資料夾屬性中。

**若要使用快速發佈將資產發佈至Dynamic Media或Experience Manager:**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在頁面左側，選取「導覽」圖示（位於「工具」圖示上方），然後在頁面右側選取 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 在 **[!UICONTROL 卡片檢視]**, **[!UICONTROL 欄檢視]**，或 **[!UICONTROL 清單檢視]**，執行下列其中一項操作：
   * 導覽至您要發佈其資產的資料夾。 選取資料夾，然後在工具列上選取 **[!UICONTROL 快速發佈]**. 使用 **[!UICONTROL 清單檢視]** 以便您更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的資料夾。 開啟資料夾，然後選取一或多個資產。 在工具列上，選取 **[!UICONTROL 快速發佈]**. 使用 **[!UICONTROL 清單檢視]** 以便您更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >若 **[!UICONTROL 快速發佈]** 工具列上未顯示，請改為選取省略號按鈕，然後選取 **[!UICONTROL 快速發佈]** 的上界。

      ![資料夾層級快速發佈至Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 從 **[!UICONTROL 快速發佈]** 清單。

   | 快速發佈選項 | 作用 |
   | --- | --- | 
   | 發佈至Experience Manager | 立即將選取的資產發佈至Experience Manager。 |
   | 發佈至 Brand Portal 網站 | 立即將所選資產發佈至 **[!UICONTROL Brand Portal]**.<br>只有在您的Experience Manager Assets執行個體已 **[!UICONTROL Brand Portal]** 已配置。 |
   | 發佈至 Dynamic Media | 立即將選取的資產發佈至Dynamic Media。<br>資產必須同步至Dynamic Media。 如有必要，請確定 **[!UICONTROL 同步模式]** 的屬性已設定為 **[!UICONTROL 將此資料夾子樹狀結構中的所有項目同步至Dynamic Media]**. |

1. 選擇 **[!UICONTROL 確定]**，然後選取 **[!UICONTROL 關閉]**.

## 透過搜尋結果選擇性地發佈或取消發佈資產 {#selective-publish-unpublish-search-results}

搜尋結果可顯示具有不同Dynamic Media發佈設定之資產資料夾中的資產。 若您從搜尋結果中選取多個資產，且每個資產有不同的Dynamic Media發佈模式設定，您可以觸發 **[!UICONTROL 管理出版物]** 從工具列、發佈或取消發佈。

另請參閱 [在Experience Manager中搜尋資產](/help/assets/search-assets.md).

**若要透過搜尋結果選擇性地發佈或取消發佈資產：**

1. 在Experience Manager的頁面左上角，選取Experience Manager標誌以存取全域導覽主控台。 在頁面左側，選取「導覽」圖示（位於「工具」圖示上方），然後選取 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 在工具列的頁面右上角附近，選取「搜尋」圖示（放大鏡）。
1. 在 **[!UICONTROL 要搜索的類型]** 文字欄位，輸入關鍵字，然後按鍵 **[!UICONTROL 輸入]**.
1. 在頁面的右上角附近，選取 **[!UICONTROL 清單檢視]** 表徵圖。
1. 在頁面左上角附近，選取 **[!UICONTROL 篩選器]** 表徵圖。

   ![搜尋結果中的清單檢視和篩選器](/help/assets/assets-dm/select-publish-search-result.png)

1. 在左側面板中，展開 **[!UICONTROL 狀態]**，然後展開 **[!UICONTROL Dynamic Media]** 搜尋述詞。
1. 使用 **[!UICONTROL 已發佈]** 和 **[!UICONTROL 未發佈]** 核取方塊，以根據已發佈的Dynamic Media資產狀態進一步調整搜尋結果。
您可以選擇將這些核取方塊與 **[!UICONTROL 發佈]** 搜尋述詞，以精簡的 **[!UICONTROL 已發佈]** 和 **[!UICONTROL 未發佈]** Experience Manager資產。
1. 執行下列任一項作業：
   * 選取您要發佈或取消發佈的一或多個資產。
   * 在 **[!UICONTROL 搜尋結果]** 頁面，選取 **[!UICONTROL 全選]**.
1. 在工具列上，選取 **[!UICONTROL 管理出版物]**. 選取工具列上的刪節號圖示，以開啟 **[!UICONTROL 管理出版物]**.
1. 在 **[!UICONTROL 管理出版物 — 選項]** 頁面，選擇所需的動作。

   | 所選操作 | 在Dynamic Media設定中發佈資產設定 | 資產包括 |
   | --- | --- | --- |
   | 發佈 | 立即或激活後 | 發佈至Experience Manager和Dynamic Media。 |
   | 發佈 | 選擇性發佈 | 僅發佈至Experience Manager。 |
   | 未發佈 | 立即或激活後 | 未發佈自Experience Manager和Dynamic Media。 |
   | 未發佈 | 選擇性發佈 | 僅取消發佈Experience Manager。 |
   | 發佈至 Dynamic Media | 立即或激活後 | 未發佈至Experience Manager、Dynamic Media或兩者。 |
   | 發佈至 Dynamic Media | 選擇性發佈 | 僅發佈至Dynamic Media。 |
   | 從 Dynamic Media 取消發佈 | 立即或激活後 | 未從Experience Manager、Dynamic Media或兩者取消發佈。 |
   | 從 Dynamic Media 取消發佈 | 選擇性發佈 | 僅從Dynamic Media取消發佈。 |

1. 在 **[!UICONTROL 排程]**，設定取消啟用的時間。

   | 所選計畫 | 發生的情況 |
   | --- | --- |
   | 立即 | 會立即執行選取的動作。 |
   | 稍後 | 所選操作將在選定的特定日期和時間運行。 |

1. 位於 **[!UICONTROL 管理出版物 — 選項]** 頁面，選取 **[!UICONTROL 下一個]**.
1. （選用）在 **[!UICONTROL 管理發布 — 範圍]** 頁面，檢閱 **[!UICONTROL 發佈目標]** 欄（位於表格中）。

   | 在Dynamic Media設定中發佈資產設定 | 所選操作 | 發佈目標 |
   | --- | --- | --- |
   | 立即或 <br>啟動時 | 發佈 | Experience Manager和Dynamic Media |
   | 立即或 <br>啟動時 | 發佈至 Dynamic Media | 無 |
   | 選擇性發佈 | 發佈 | Experience Manager |
   | 選擇性發佈 | 發佈至 Dynamic Media | Dynamic Media |
   | 立即或 <br>啟動時 | 未發佈 | Experience Manager和Dynamic Media |
   | 立即或 <br>啟動時 | 從 Dynamic Media 取消發佈 | 無 |
   | 選擇性發佈 | 未發佈 | Experience Manager |
   | 選擇性發佈 | 從 Dynamic Media 取消發佈 | Dynamic Media |

1. 在 **[!UICONTROL 管理發布 — 範圍]** 頁面，執行下列任一操作：
   * 選取您要從發佈或取消發佈中移除的一或多個資產。
   * 位於 **[!UICONTROL 管理發布 — 範圍]** 頁面，選取 **[!UICONTROL 發佈]** 或 **[!UICONTROL 取消發佈]** 開始動作。
1. 選擇 **[!UICONTROL 確定]**.

## 檢查資產的發佈狀態 {#check-publish-status-of-asset}

您可以使用 **[!UICONTROL 時間表]** with **[!UICONTROL 卡片檢視]**, **[!UICONTROL 欄檢視]**，或 **[!UICONTROL 清單檢視]** Experience Manager，以快速檢查資產的發佈狀態。

**若要檢查資產的發佈狀態：**

1. 在Experience Manager的頁面左上角，選取Experience Manager標誌以存取全域導覽主控台。 在頁面左側，選取「導覽」圖示（位於「工具」圖示上方），然後選取 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 在 **[!UICONTROL 卡片檢視]**, **[!UICONTROL 欄檢視]**，或 **[!UICONTROL 清單檢視]** (下方螢幕截圖顯示 **[!UICONTROL 清單檢視]**)，開啟包含您已發佈或取消發佈之資產的資料夾。
1. 選取資產，使其以勾選記號顯示。 如需範例，請參閱下方的螢幕擷圖。
1. 在頁面左上角附近，從下拉式功能表中選取 **[!UICONTROL 時間表]**. 此 **[!UICONTROL 狀態]** 左側面板中的「 」區域會顯示所選資產的發佈狀態。
使用 **[!UICONTROL 清單檢視]**, **[!UICONTROL Dynamic Media]** 出現發佈狀態。
   * 設定為同步至Dynamic Media的資料夾會顯示 **[!UICONTROL Dynamic Media]** 欄。
   * 資料夾 *not* 設為同步至Dynamic Media時，不會顯示「Dynamic Media」欄。
      ![清單檢視和時間軸](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 疑難排解選擇性發佈 {#selective-publish-troubleshoot}

資產未同步至Dynamic Media，但其上觸發了Dynamic Media發佈動作，會導致下列錯誤訊息和解決方案：

![選擇性發佈錯誤](/help/assets/assets-dm/selective-publish-error.png)
