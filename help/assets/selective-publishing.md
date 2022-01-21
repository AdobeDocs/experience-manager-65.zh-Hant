---
title: 與選擇性出版合作在Dynamic Media
description: 您可以選擇在資料夾級別向Adobe Experience Manager或Dynamic Media發佈或取消發佈資產。 您可以使用「管理出版物」或「快速發佈」，而不是僅依賴「Dynamic Media配置」，其設定對Dynamic Media實例中的所有資料夾是全局的。
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
ht-degree: 3%

---

# 在Dynamic Media的資料夾級別配置選擇性發佈 {#selective-publish-configure-folder}

您可以選擇在資料夾級別向Adobe Experience Manager或Dynamic Media發佈或取消發佈資產。 您可以使用 **[!UICONTROL 管理發布]** 或 **[!UICONTROL 快速發佈]** 而不是單純依靠 **[!UICONTROL Dynamic Media配置]** 其設定對您的Dynamic Media實例中的所有資料夾是全局的。

例如，通過選擇性發佈，您可以針對尚未上市的產品處理資產。 在這種情況下，營銷團隊可以訪問與Dynamic Media同步的智慧作物影像和動態呈現。 它們可以製作宣傳材料，而無需將這些資產公佈到Dynamic Media，以便進行全球交付。

>[!IMPORTANT]
>
>「選擇性發佈」僅在Dynamic Media-Scene7模式下可用。

>[!NOTE]
>
>*複製* 「來自」(assets to)和「來自」(from)資料夾將清除這些資產的發佈狀態。 但是，當你 *移動* 將資料夾屬性設定為的資料夾的「資產」和「來自」 **[!UICONTROL 選擇性發佈]**&#x200B;保持這些資產的發佈狀態。

如果你以後決定 **[!UICONTROL 選擇性發佈]** 資料夾中的設定，這些更改只影響從該點開始上載到該資料夾的新資產。 資料夾中現有資產的發佈狀態保持原樣，直到您手動將其從以下任一資料夾 **[!UICONTROL 快速發佈]** 或 **[!UICONTROL 管理發布]** 對話框。

資料夾級別 **[!UICONTROL Dynamic Media發佈模式]** 選項始終預設為 **[!UICONTROL 發佈資產]** 設定 **[!UICONTROL Dynamic Media配置]**。 但是，本主題中的以下步驟將顯示如何在資料夾級別手動更改此預設值（如以下步驟所述）以覆蓋 **[!UICONTROL Dynamic Media配置]** 值。

無論您是否依賴以下任一項：

* **[!UICONTROL 發佈資產]** 設定的值 **[!UICONTROL Dynamic Media配置]**。
* **[!UICONTROL Dynamic Media發佈模式]** 在資料夾級別屬性中設定的值。

您可以選擇 **[!UICONTROL 立即]**。 **[!UICONTROL 激活時]**&#x200B;或 **[!UICONTROL 選擇性發佈]**。 例如，可以設定 **[!UICONTROL 發佈資產]** 價值 **[!UICONTROL Dynamic Media配置]** 至 **[!UICONTROL 激活時]**，但設定 **[!UICONTROL Dynamic Media出版]** 資料夾級別的模式值 **[!UICONTROL 選擇性發佈]**&#x200B;反之，

在資料夾中配置選擇性發佈後，可以執行下列任一操作：

* [使用管理出版物有選擇地將資產發佈到Dynamic Media或Experience Manager](#selective-publish-manage-publication)。
* [使用管理出版物有選擇地從Dynamic Media或Experience Manager中取消發佈資產](#selective-unpublish-manage-publication)。
* [使用快速發佈將資產發佈到Dynamic Media或Experience Manager](#quick-publish-aem-dm)。
* [通過搜索結果有選擇地發佈或取消發佈資產](#selective-publish-unpublish-search-results)。

**要在Dynamic Media的資料夾級別配置選擇性發佈，請：**

1. 在Experience Manager中，選擇Experience Manager徽標以訪問全局導航控制台。 在左側，選擇「導航」表徵圖（就在「工具」表徵圖上方），然後選擇 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**。
1. 執行下列操作之一：
   * 編輯現有資料夾的屬性 — 在 **[!UICONTROL 卡視圖]**。 **[!UICONTROL 列視圖]**&#x200B;或 **[!UICONTROL 清單視圖]**，導航到要編輯其屬性的資料夾。 選擇資料夾，然後在工具欄上，選擇 **[!UICONTROL 屬性]**。
   * 編輯新資料夾的屬性 — 在 **[!UICONTROL 卡視圖]**。 **[!UICONTROL 列視圖]**&#x200B;或 **[!UICONTROL 清單視圖]**，靠近頁面右上角，選擇 **[!UICONTROL 建立]** > **[!UICONTROL 資料夾]**。 在 **[!UICONTROL 建立資料夾]** 對話框，輸入資料夾的標題（必需），然後選擇 **[!UICONTROL 建立]**。 選擇資料夾，然後在工具欄上，選擇 **[!UICONTROL 屬性]**。

1. 在 **[!UICONTROL 同步模式]** 下拉清單中，選擇以下選項之一：

   | 同步模式 | 說明 |
   | --- | --- |
   | **[!UICONTROL 已繼承]** | 資料夾上沒有顯式同步值；相反，資料夾會從其祖先資料夾或您的 **[!UICONTROL Dynamic Media配置]**。 詳細狀態 **[!UICONTROL 繼承]** 以刀尖顯示。 |
   | **[!UICONTROL 將此資料夾子樹中的所有內容同步到Dynamic Media]** | 要向Dynamic Media發佈成功，資產必須同步到Dynamic Media。 選擇此選項將包括此子樹中用於同步到Dynamic Media的所有資產。 特定於資料夾的設定將覆蓋 **[!UICONTROL Dynamic Media配置]**。 |
   | **[!UICONTROL 從Dynamic Media同步中排除此資料夾子樹中的所有內容]** | 排除此子樹中的所有資產，使其無法同步到Dynamic Media。 |

   ![資料夾級別選擇性發佈](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 在 **[!UICONTROL Dynamic Media發佈模式]** 下拉清單中，選擇一個選項。 的 **[!UICONTROL Dynamic Media發佈模式]** 選項始終預設為 **[!UICONTROL Dynamic Media配置]**。 但是，您可以手動覆蓋此預設值 **[!UICONTROL Dynamic Media配置]** 值。

   >[!IMPORTANT]
   >
   >無論您選擇的「Dynamic Media發佈模式」選項如何，您稍後對 *已* 發佈後，這些更新將立即發佈，而不會執行任何進一步的用戶操作。
   >
   >如果已發佈的視頻已更新，則必須再次發佈該視頻以反映交付時的更改。

   | Dynamic Media發佈模式選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 當資產上載到此資料夾時，系統會將資產放入Experience Manager中，並立即提供URL/Embed。 此選項僅與Experience Manager發佈相關，並且發佈資產不需要用戶干預。<br>此選項為 *不* 如果選定，則可用 **[!UICONTROL 從Dynamic Media同步中排除此資料夾子樹中的所有內容]** 在 **[!UICONTROL 同步模式]** 的上界。 |
   | **[!UICONTROL 啟動時]** | 將資產上載到此資料夾時，必須先顯式發佈資產，然後才能提供URL/嵌入連結。 此選項僅與Experience Manager發佈相關。<br>此選項為 *不* 如果選定，則可用 **[!UICONTROL 從Dynamic Media同步中排除此資料夾子樹中的所有內容]** 在 **[!UICONTROL 同步模式]** 的上界。 |
   | **[!UICONTROL 選擇性發佈]** | 資產將發佈給您選擇的Experience Manager或Dynamic Media，以便在公共域中交付。 兩種發佈方式相互排斥。 即，您可以將資產發佈到DMS7，以便您可以使用諸如智慧裁剪或動態格式副本等功能。 或者，您可以只將資產發佈到Experience Manager，以便安全預覽；這些資產 *不* 已發佈到DMS7以在公共域中交付。 如果選擇，則此選項不可用 **[!UICONTROL 從Dynamic Media同步中排除此資料夾子樹中的所有內容]** 在 **[!UICONTROL 同步模式]** 的上界。 |

1. 在頁面的右上角，選擇 **[!UICONTROL 保存並關閉]**，然後選擇 **[!UICONTROL 確定]** 回到Experience Manager Assets。

## 使用管理出版物有選擇地將資產發佈到Dynamic Media或Experience Manager{#selective-publish-manage-publication}

在您使用之前 **[!UICONTROL 管理發布]** 要有選擇地向Dynamic Media或Experience Manager發佈資產，請確保設定了以下選項之一：

* 的 **[!UICONTROL 發佈資產]** 選項 **[!UICONTROL Dynamic Media配置]** 至 **[!UICONTROL 選擇性發佈]**
* 已在資料夾級別配置選擇性發佈。

請參閱 [建立Dynamic Media配置](#configuring-dynamic-media-cloud-services) 或 [在Dynamic Media的資料夾級別配置選擇性發佈](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>「選擇性發佈」僅在Dynamic Media-Scene7模式下可用。

>[!NOTE]
>
>*複製* 「來自」(assets to)和「來自」(from)資料夾將清除這些資產的發佈狀態。 但是，當你 *移動* 將資料夾屬性設定為的資料夾的「資產」和「來自」 **[!UICONTROL 選擇性發佈]**&#x200B;保持這些資產的發佈狀態。

**要使用「管理出版物」有選擇地將資產發佈到Dynamic Media或Experience Manager:**

1. 在Experience Manager中，選擇Experience Manager徽標以訪問全局導航控制台。 在左側，選擇「導航」表徵圖（就在「工具」表徵圖上方），然後選擇 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**。
1. 在 **[!UICONTROL 卡視圖]**。 **[!UICONTROL 列視圖]**&#x200B;或 **[!UICONTROL 清單視圖]**，執行以下操作之一：
   * 導航到要發佈其資產的資料夾。 選擇資料夾，然後在工具欄上，選擇 **[!UICONTROL 管理發布]**。 使用 **[!UICONTROL 清單視圖]** 這樣，您就可以更輕鬆地檢查特定資料夾的發佈狀態。
   * 導航到要發佈其資產的資料夾。 開啟資料夾，然後選擇一個或多個資產。 在工具欄上，選擇 **[!UICONTROL 管理發布]**。 使用 **[!UICONTROL 清單視圖]** 這樣您就可以更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果 **[!UICONTROL 管理發布]** 工具欄上未顯示省略號按鈕，然後選擇 **[!UICONTROL 管理發布]** 的子菜單。

1. 在 **[!UICONTROL 管理發布 — 選項]** 頁，下 **[!UICONTROL 操作]**，選擇所需激活的類型。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL 發佈]** (到Experience Manager) | 選擇此選項，以便可以將資產發佈到Experience Manager以進行安全預覽。 |
   | **[!UICONTROL 發佈至 Dynamic Media]** | 選擇此選項，以便您可以將資產發佈到Dynamic Media以便在公共域中交付，或者您可以使用「智慧裁剪」或動態格式副本等功能。<br>此選項僅在以下情況下可用 **[!UICONTROL Dynamic Media發佈模式]** 設定為 **[!UICONTROL 選擇性發佈]** 的子菜單。 |

1. 下 **[!UICONTROL 計畫]**，設定發佈的時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 選擇以立即發佈資產。 |
   | **[!UICONTROL 稍後]** | 選擇以在特定日期和時間發佈資產。 |

1. 在右上角 **[!UICONTROL 管理發布]** ，選擇 **[!UICONTROL 下一個]**。
1. 在 **[!UICONTROL 管理出版物 — 範圍]** 頁，執行下列操作之一：

   * 如有必要，請選擇要從發佈中刪除的一個或多個資產。
   * 在右上角 **[!UICONTROL 管理出版物 — 範圍]** ，選擇 **[!UICONTROL 發佈]** 或 **[!UICONTROL 發佈到Dynamic Media]**。
1. 選擇 **[!UICONTROL 確定]**。

### 使用管理出版物有選擇地從Dynamic Media或Experience Manager中取消發佈資產 {#selective-unpublish-manage-publication}

1. 在Experience Manager中，選擇Experience Manager徽標以訪問全局導航控制台。 在左側，選擇「導航」表徵圖（就在「工具」表徵圖上方），然後選擇 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**。
1. 在 **[!UICONTROL 卡視圖]**。 **[!UICONTROL 列視圖]**&#x200B;或 **[!UICONTROL 清單視圖]**，執行以下操作之一：
   * 導航到要取消發佈其資產的資料夾。 選擇資料夾，然後在工具欄上，選擇 **[!UICONTROL 管理發布]**。 使用 **[!UICONTROL 清單視圖]** 這樣，您就可以更輕鬆地檢查特定資料夾的發佈狀態。
   * 導航到要取消發佈其資產的資料夾。 開啟資料夾，然後選擇一個或多個資產。 在工具欄上，選擇 **[!UICONTROL 管理發布]**。 使用 **[!UICONTROL 清單視圖]** 這樣您就可以更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果 **[!UICONTROL 管理發布]** 工具欄上未顯示省略號按鈕，然後選擇 **[!UICONTROL 管理發布]** 的子菜單。

1. 在 **[!UICONTROL 管理發布 — 選項]** 頁，下 **[!UICONTROL 操作]**，選擇所需的取消激活類型。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL 取消發佈]** (來自Experience Manager) | 如果要從Experience Manager中取消發佈資產，請選擇此選項。 |
   | **[!UICONTROL 從 Dynamic Media 取消發佈]** | 如果要取消發佈來自Dynamic Media的資產，請選擇此選項。<br>此選項僅在以下情況下可用 **[!UICONTROL Dynamic Media發佈模式]** 設定為 **[!UICONTROL 選擇性發佈]** 的子菜單。 |

1. 下 **[!UICONTROL 計畫]**，設定取消激活的時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 選擇以立即取消發佈資產。 |
   | **[!UICONTROL 稍後]** | 選擇以取消發佈特定日期和時間上的資產。 |

1. 在右上角 **[!UICONTROL 管理發布]** ，選擇 **[!UICONTROL 下一個]**。
1. 在 **[!UICONTROL 管理出版物 — 範圍]** 頁，執行下列操作之一：
   * 選擇要從取消發佈中刪除的一個或多個資產。
   * 在右上角 **[!UICONTROL 管理出版物 — 範圍]** ，選擇 **[!UICONTROL 取消發佈]** 或 **[!UICONTROL 從Dynamic Media取消出版]**。
1. 選擇 **[!UICONTROL 確定]**。

## 使用快速發佈將資產發佈到Dynamic Media或Experience Manager {#quick-publish-aem-dm}

您可以使用 **[!UICONTROL 快速發佈]** 用於簡單的資產激活案例。 **[!UICONTROL 快速發佈]** 立即發佈所選資產，而不再進行任何用戶交互。 由於此操作，任何未發佈的引用也會自動發佈。

>[!NOTE]
>
>要使用 **[!UICONTROL 快速發佈]** 向Dynamic Media或Experience Manager公佈資產， **[!UICONTROL 選擇性發佈]** 在 **[!UICONTROL Dynamic Media配置]** 或選定資料夾的資料夾屬性中。

**要使用「快速發佈」將資產發佈到Dynamic Media或Experience Manager:**

1. 在Experience Manager中，選擇Experience Manager徽標以訪問全局導航控制台。 在頁面的左側，選擇「導航」表徵圖（就在「工具」表徵圖的上方），然後在頁面的右側選擇 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**。
1. 在 **[!UICONTROL 卡視圖]**。 **[!UICONTROL 列視圖]**&#x200B;或 **[!UICONTROL 清單視圖]**，執行以下操作之一：
   * 導航到要發佈其資產的資料夾。 選擇資料夾，然後在工具欄上，選擇 **[!UICONTROL 快速發佈]**。 使用 **[!UICONTROL 清單視圖]** 這樣，您就可以更輕鬆地檢查特定資料夾的發佈狀態。
   * 導航到要發佈其資產的資料夾。 開啟資料夾，然後選擇一個或多個資產。 在工具欄上，選擇 **[!UICONTROL 快速發佈]**。 使用 **[!UICONTROL 清單視圖]** 這樣您就可以更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果 **[!UICONTROL 快速發佈]** 工具欄上未顯示省略號按鈕，然後選擇 **[!UICONTROL 快速發佈]** 的子菜單。

      ![資料夾級快速發佈到Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 從 **[!UICONTROL 快速發佈]** 的子菜單。

   | 快速發佈選項 | 它的功能 |
   | --- | --- | 
   | 發佈到Experience Manager | 立即將所選資產發佈到Experience Manager。 |
   | 發佈至 Brand Portal 網站 | 立即將所選資產發佈到 **[!UICONTROL Brand Portal]**。<br>此選項僅在您的Experience Manager Assets實例具有 **[!UICONTROL Brand Portal]** 已配置。 |
   | 發佈至 Dynamic Media | 將選定資產立即發佈到Dynamic Media。<br>資產必須與Dynamic Media同步。 如有必要，請確保 **[!UICONTROL 同步模式]** 資料夾的屬性已設定為 **[!UICONTROL 將此資料夾子樹中的所有內容同步到Dynamic Media]**。 |

1. 選擇 **[!UICONTROL 確定]**，然後選擇 **[!UICONTROL 關閉]**。

## 通過搜索結果有選擇地發佈或取消發佈資產 {#selective-publish-unpublish-search-results}

搜索結果可以顯示具有不同Dynamic Media發佈設定的資產資料夾中的資產。 如果從搜索結果中選擇多個資產，並且每個資產具有不同的Dynamic Media發佈模式設定，則可以觸發 **[!UICONTROL 管理發布]** 的子菜單。

另請參閱 [在Experience Manager中搜索資產](/help/assets/search-assets.md)。

**要通過搜索結果有選擇地發佈或取消發佈資產，請執行以下操作：**

1. 在Experience Manager中，在頁面左上角，選擇Experience Manager徽標以訪問全局導航控制台。 在頁面左側，選擇導航表徵圖（就在「工具」表徵圖上方），然後選擇 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**。
1. 在工具欄上，靠近頁面右上角，選擇「搜索」表徵圖（放大鏡）。
1. 在 **[!UICONTROL 要搜索的類型]** 文本欄位，輸入關鍵字，然後按 **[!UICONTROL 輸入]**。
1. 在頁面的右上角，選擇 **[!UICONTROL 清單視圖]** 表徵圖
1. 在頁面左上角附近，選擇 **[!UICONTROL 篩選器]** 表徵圖

   ![搜索結果中的清單視圖和篩選器](/help/assets/assets-dm/select-publish-search-result.png)

1. 在左面板中，展開 **[!UICONTROL 狀態]**，然後展開 **[!UICONTROL Dynamic Media]** 搜索謂詞。
1. 使用 **[!UICONTROL 已發佈]** 和 **[!UICONTROL 未發佈]** 複選框，以根據已發佈的Dynamic Media資產狀態進一步細化搜索結果。
（可選）您可以將這些複選框與 **[!UICONTROL 發佈]** 搜索謂詞以細化 **[!UICONTROL 已發佈]** 和 **[!UICONTROL 未發佈]** Experience Manager資產。
1. 執行下列操作之一：
   * 選擇要發佈或取消發佈的一個或多個資產。
   * 靠近 **[!UICONTROL 搜索結果]** ，選擇 **[!UICONTROL 全選]**。
1. 在工具欄上，選擇 **[!UICONTROL 管理發布]**。 選擇工具欄上的省略號表徵圖，以便開啟 **[!UICONTROL 管理發布]**。
1. 在 **[!UICONTROL 管理發布 — 選項]** 的子菜單。

   | 所選操作 | 在Dynamic Media配置中發佈資產設定 | 資產為 |
   | --- | --- | --- |
   | 發佈 | 立即或激活時 | 出版給Experience Manager和Dynamic Media。 |
   | 發佈 | 選擇性發佈 | 僅發佈到Experience Manager。 |
   | 未發佈 | 立即或激活時 | Experience Manager和Dynamic Media未發表。 |
   | 未發佈 | 選擇性發佈 | 僅從Experience Manager取消發佈。 |
   | 發佈至 Dynamic Media | 立即或激活時 | 不發表給Experience Manager或Dynamic Media，或兩者。 |
   | 發佈至 Dynamic Media | 選擇性發佈 | 僅發佈給Dynamic Media。 |
   | 從 Dynamic Media 取消發佈 | 立即或激活時 | 沒有從Experience Manager或Dynamic Media或兩者中取消發佈。 |
   | 從 Dynamic Media 取消發佈 | 選擇性發佈 | 僅從Dynamic Media發佈。 |

1. 下 **[!UICONTROL 計畫]**，設定取消激活的時間。

   | 所選計畫 | 發生的事 |
   | --- | --- |
   | 立即 | 將立即執行所選操作。 |
   | 稍後 | 所選操作將在所選特定日期和時間運行。 |

1. 在右上角 **[!UICONTROL 管理發布 — 選項]** ，選擇 **[!UICONTROL 下一個]**。
1. （可選）在 **[!UICONTROL 管理出版物 — 範圍]** 頁，查看 **[!UICONTROL 發佈目標]** 的子菜單。

   | 在Dynamic Media配置中發佈資產設定 | 所選操作 | 發佈目標 |
   | --- | --- | --- |
   | 立即或 <br>激活後 | 發佈 | Experience Manager和Dynamic Media |
   | 立即或 <br>激活後 | 發佈至 Dynamic Media | 無 |
   | 選擇性發佈 | 發佈 | Experience Manager |
   | 選擇性發佈 | 發佈至 Dynamic Media | Dynamic Media |
   | 立即或 <br>激活後 | 未發佈 | Experience Manager和Dynamic Media |
   | 立即或 <br>激活後 | 從 Dynamic Media 取消發佈 | 無 |
   | 選擇性發佈 | 未發佈 | Experience Manager |
   | 選擇性發佈 | 從 Dynamic Media 取消發佈 | Dynamic Media |

1. 在 **[!UICONTROL 管理出版物 — 範圍]** 頁，執行下列操作之一：
   * 選擇要從發佈或取消發佈中刪除的一個或多個資產。
   * 在右上角 **[!UICONTROL 管理出版物 — 範圍]** ，選擇 **[!UICONTROL 發佈]** 或 **[!UICONTROL 取消發佈]** 開始操作。
1. 選擇 **[!UICONTROL 確定]**。

## 檢查資產的發佈狀態 {#check-publish-status-of-asset}

您可以使用 **[!UICONTROL 時間軸]** 與 **[!UICONTROL 卡視圖]**。 **[!UICONTROL 列視圖]**&#x200B;或 **[!UICONTROL 清單視圖]** 中Experience Manager快速檢查資產的發佈狀態。

**要檢查資產的發佈狀態，請執行以下操作：**

1. 在Experience Manager中，在頁面左上角，選擇Experience Manager徽標以訪問全局導航控制台。 在頁面左側，選擇導航表徵圖（就在「工具」表徵圖上方），然後選擇 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**。
1. 在 **[!UICONTROL 卡視圖]**。 **[!UICONTROL 列視圖]**&#x200B;或 **[!UICONTROL 清單視圖]** (下面的螢幕截圖顯示 **[!UICONTROL 清單視圖]**)，開啟包含已發佈或未發佈的資產的資料夾。
1. 選擇一個資產，使其顯示為複選標籤。 例如，請參閱下面的螢幕截圖。
1. 在頁面左上角附近，從下拉菜單中選擇 **[!UICONTROL 時間軸]**。 的 **[!UICONTROL 狀態]** 區域顯示選定資產的發佈狀態。
使用 **[!UICONTROL 清單視圖]**&#x200B;的 **[!UICONTROL Dynamic Media]** 顯示「發佈狀態」(publish state)。
   * 配置為同步到Dynamic Media的資料夾顯示 **[!UICONTROL Dynamic Media]** 列。
   * 資料夾 *不* 配置為同步到Dynamic Media不顯示Dynamic Media列。
      ![清單視圖和時間軸](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 排除選擇性發佈故障 {#selective-publish-troubleshoot}

未同步到Dynamic Media但觸發了Dynamic Media發佈操作的資產將導致以下錯誤消息和解決方案：

![選擇性發佈錯誤](/help/assets/assets-dm/selective-publish-error.png)
