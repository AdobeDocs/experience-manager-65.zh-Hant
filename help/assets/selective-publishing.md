---
title: 在 Dynamic Media 中使用選擇性發佈
description: 關於如何在Dynamic Media中使用選擇性發佈的資訊。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publishing
source-git-commit: a5164c0c2ef175f1bf63ef911bf92df36e413a6f
workflow-type: tm+mt
source-wordcount: '2960'
ht-degree: 3%

---

# 在Dynamic Media的資料夾層級設定選擇性發佈 {#selective-publish-configure-folder}

您可以在資料夾層級選擇從Adobe Experience Manager或Dynamic Media發佈或取消發佈資產。 您可以使用&#x200B;**[!UICONTROL 管理出版物]**&#x200B;或&#x200B;**[!UICONTROL 快速發佈]**，而非僅能依賴設定與Dynamic Media執行個體的所有資料夾相同的&#x200B;**[!UICONTROL Dynamic Media組態]**。

例如，透過選擇性發佈，您可以針對尚未上線的產品使用資產。 在這種情況下，行銷團隊可以存取同步至Dynamic Media的智慧型裁切影像和動態轉譯。 它們可以製作促銷文宣，而完全不需要將這些資產發佈至Dynamic Media以供全球傳送。

>[!IMPORTANT]
>
>「選擇性發佈」僅適用於Dynamic Media - Scene7模式。

>[!NOTE]
>
>** 將資產複製到資料夾和從資料夾複製會清除這些資產的發佈狀態。不過，當您將&#x200B;*移動*&#x200B;資產至資料夾屬性設為&#x200B;**[!UICONTROL 選擇性發佈]**&#x200B;的資料夾時，會維持這些資產的發佈狀態。

如果您稍後決定變更資料夾中的&#x200B;**[!UICONTROL 選擇性發佈]**&#x200B;設定，這些變更只會影響您從該時間點上傳至該資料夾的新資產。 資料夾中現有資產的發佈狀態會維持原狀，直到您從&#x200B;**[!UICONTROL 快速發佈]**&#x200B;或&#x200B;**[!UICONTROL 管理出版物]**&#x200B;對話方塊手動變更為止。

資料夾層級&#x200B;**[!UICONTROL Dynamic Media發佈模式]**&#x200B;選項一律預設為&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;中的&#x200B;**[!UICONTROL 發佈資產]**&#x200B;設定值。 不過，本主題中的下列步驟會示範如何手動變更資料夾層級的此預設值（如下列步驟所述），以覆寫&#x200B;**[!UICONTROL Dynamic Media Configuration]**&#x200B;值。

無論您是否仰賴下列其中一項：

* **[!UICONTROL 發]** 布Dynamic Media設定中 **[!UICONTROL 設定的資產值]**。
* **[!UICONTROL Dynamic Media在資]** 料夾層級屬性中設定的發佈模式值。

您可以選擇「啟動時」**[!UICONTROL 「立即」]**、「啟動時」**[!UICONTROL 或「選擇性發佈」**[!UICONTROL 。 ]**]**&#x200B;例如，您可以將&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;中的&#x200B;**[!UICONTROL 發佈資產]**&#x200B;值設為&#x200B;**[!UICONTROL 啟用時]**，但將資料夾層級的&#x200B;**[!UICONTROL Dynamic Media發佈]**&#x200B;模式值設為&#x200B;**[!UICONTROL 選擇性發佈]**，反之亦然。

在資料夾中設定選擇性發佈後，您可以執行下列任一操作：

* [使用管理出版物選擇性地將資產發佈至Dynamic Media或Experience Manager](#selective-publish-manage-publication)。
* [使用「管理出版物」從Dynamic Media或Experience Manager選擇性地取消發佈資產](#selective-unpublish-manage-publication)。
* [使用快速發佈將資產發佈至Dynamic Media或Experience Manager](#quick-publish-aem-dm)。
* [透過搜尋結果選擇性地發佈或取消發佈資產](#selective-publish-unpublish-search-results)。

**若要在Dynamic Media中在資料夾層級設定選擇性發佈：**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後選取「**[!UICONTROL 資產]** > **[!UICONTROL 檔案]**」。
1. 執行下列任一操作：
   * 編輯現有資料夾的屬性 — 在&#x200B;**[!UICONTROL 卡片視圖]**、**[!UICONTROL 列視圖]**&#x200B;或&#x200B;**[!UICONTROL 清單視圖]**&#x200B;中，導航到要編輯其屬性的資料夾。 選擇資料夾，然後在工具欄上選擇&#x200B;**[!UICONTROL 屬性]**。
   * 編輯新資料夾的屬性 — 在&#x200B;**[!UICONTROL 卡片視圖]**、**[!UICONTROL 列視圖]**&#x200B;或&#x200B;**[!UICONTROL 清單視圖]**&#x200B;中，在頁面右上角附近，選擇&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 資料夾]**。 在&#x200B;**[!UICONTROL 建立資料夾]**&#x200B;對話框中，輸入資料夾的標題（必要），然後選擇&#x200B;**[!UICONTROL 建立]**。 選擇資料夾，然後在工具欄上選擇&#x200B;**[!UICONTROL 屬性]**。

1. 在&#x200B;**[!UICONTROL 同步模式]**&#x200B;下拉清單中，選擇以下選項之一：

   | 同步模式 | 說明 |
   | --- | --- |
   | **[!UICONTROL 已繼承]** | 資料夾上沒有明確的同步值；相反，資料夾會繼承其上階資料夾中的一個同步值，或繼承&#x200B;**[!UICONTROL Dynamic Media Configuration]**&#x200B;中設定的預設模式。 **[!UICONTROL Inherited]**&#x200B;的詳細狀態通過工具提示顯示。 |
   | **[!UICONTROL 將此資料夾子樹狀結構中的所有項目同步至Dynamic Media]** | 若要發佈至Dynamic Media成功，必須將資產同步至Dynamic Media。 選取此選項會包含此子樹狀結構中要同步至Dynamic Media的所有資產。 資料夾特定設定會覆寫&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;中的預設設定。 |
   | **[!UICONTROL 從Dynamic Media同步中排除此資料夾子樹狀結構中的所有項目]** | 排除此子樹狀結構中的所有資產，不得同步至Dynamic Media。 |

   ![資料夾層級選擇性發佈](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 在&#x200B;**[!UICONTROL Dynamic Media發佈模式]**&#x200B;下拉式清單中，選取選項。 **[!UICONTROL Dynamic Media發佈模式]**&#x200B;選項一律預設為&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;中設定的值。 不過，您可以使用下列其中一個選項，手動覆寫此預設&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;值。

   >[!IMPORTANT]
   >
   >無論您選取的Dynamic Media發佈模式選項為何，您之後對已發佈&#x200B;*的資產所進行的任何更新，都會立即發佈這些更新，而不需進一步使用者動作。*
   >
   >如果已發佈的視訊已更新，則必須再次發佈，以反映傳送時的變更。

   | Dynamic Media發佈模式選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 資產上傳至此資料夾時，系統會將資產內嵌至Experience Manager，並立即提供URL/內嵌。 此選項僅與Experience Manager發佈系結，不需要使用者干預即可發佈資產。<br>如果您在上 ** 一個步驟中選取「從Dynamic Media **[!UICONTROL 同步模式中排除此資料夾子樹狀]** 結構中 **[!UICONTROL 的所]** 有內容」 ，則此選項不可用。 |
   | **[!UICONTROL 啟動時]** | 資產上傳至此資料夾時，您必須先明確發佈資產，才能提供URL/內嵌連結。 此選項僅與Experience Manager發佈系結。<br>如果您在上 ** 一個步驟中選取「從Dynamic Media **[!UICONTROL 同步模式中排除此資料夾子樹狀]** 結構中 **[!UICONTROL 的所]** 有內容」 ，則此選項不可用。 |
   | **[!UICONTROL 選擇性發佈]** | 資產會發佈至您選擇的Experience Manager，或發佈至Dynamic Media，以便在公開網域中傳送。 兩種發佈方法彼此互斥。 也就是說，您可以將資產發佈至DMS7，以便使用智慧型裁切或動態轉譯等功能。 或者，您也可以只將資產發佈至Experience Manager，以確保安全預覽；這些相同的資產是&#x200B;*not*&#x200B;發佈至DMS7以供在公共網域中傳遞。 如果您在前一個步驟的&#x200B;**[!UICONTROL 同步模式]**&#x200B;中，從Dynamic Media同步&#x200B;]**中選取了**[!UICONTROL &#x200B;排除此資料夾子樹狀結構中的所有內容，則此選項不可用。 |

1. 在頁面的右上角，選取&#x200B;**[!UICONTROL 儲存並關閉]**，然後選取&#x200B;**[!UICONTROL 確定]**&#x200B;以返回Experience Manager資產。

## 使用管理出版物選擇性地將資產發佈至Dynamic Media或Experience Manager{#selective-publish-manage-publication}

使用&#x200B;**[!UICONTROL 管理出版物]**&#x200B;來選擇性地將資產發佈至Dynamic Media或Experience Manager之前，請確定您已設定下列其中一項：

* **[!UICONTROL Dynamic Media設定]**&#x200B;中的&#x200B;**[!UICONTROL 發佈資產]**&#x200B;選擇性發佈&#x200B;]**選項**[!UICONTROL 
* 在資料夾層級設定選擇性發佈。

請參閱[建立Dynamic Media設定](#configuring-dynamic-media-cloud-services)或[在Dynamic Media](#selective-publish-configure-folder)的資料夾層級設定選擇性發佈

>[!IMPORTANT]
>
>「選擇性發佈」僅適用於Dynamic Media - Scene7模式。

>[!NOTE]
>
>** 將資產複製到資料夾和從資料夾複製會清除這些資產的發佈狀態。不過，當您將&#x200B;*移動*&#x200B;資產至資料夾屬性設為&#x200B;**[!UICONTROL 選擇性發佈]**&#x200B;的資料夾時，會維持這些資產的發佈狀態。

**若要使用「管理出版物」選擇性地將資產發佈至Dynamic Media或Experience Manager:**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後選取「**[!UICONTROL 資產]** > **[!UICONTROL 檔案]**」。
1. 在&#x200B;**[!UICONTROL 卡片視圖]**、**[!UICONTROL 列視圖]**&#x200B;或&#x200B;**[!UICONTROL 清單視圖]**&#x200B;中，執行以下操作之一：
   * 導覽至您要發佈其資產的資料夾。 選擇資料夾，然後在工具欄上選擇&#x200B;**[!UICONTROL 管理出版物]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，以便更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的資料夾。 開啟資料夾，然後選取一或多個資產。 在工具欄上，選擇&#x200B;**[!UICONTROL 管理出版物]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，以便更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果工具欄上未顯示&#x200B;**[!UICONTROL 管理出版物]**，請改為選擇省略號按鈕，然後從清單菜單中選擇&#x200B;**[!UICONTROL 管理出版物]**。

1. 在&#x200B;**[!UICONTROL 管理出版物 — 選項]**&#x200B;頁的&#x200B;**[!UICONTROL 操作]**&#x200B;下，選擇所需的激活類型。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL 發佈]** (至Experience Manager) | 選取此選項，即可將資產發佈至Experience Manager，以進行安全預覽。 |
   | **[!UICONTROL 發佈至 Dynamic Media]** | 選取此選項，即可將資產發佈至Dynamic Media以在公用網域中傳送，或是使用智慧型裁切或動態轉譯等功能。<br>只有在將Dynamic Media發佈模 **[!UICONTROL 式設]** 為資料夾屬性的 **[!UICONTROL 選擇]** 性發佈時，才可使用此選項。 |

1. 在&#x200B;**[!UICONTROL Schedule]**&#x200B;下，設定發佈的時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 選取以立即發佈資產。 |
   | **[!UICONTROL 稍後]** | 選取以在特定日期和時間發佈資產。 |

1. 在&#x200B;**[!UICONTROL 管理出版物]**&#x200B;頁面的右上角，選擇&#x200B;**[!UICONTROL Next]**。
1. 在&#x200B;**[!UICONTROL 管理發布 — 範圍]**&#x200B;頁中，執行下列操作之一：

   * 如有必要，請選取一或多個您要從發佈中移除的資產。
   * 在&#x200B;**[!UICONTROL 管理出版物 — 範圍]**&#x200B;頁面的右上角，選擇&#x200B;**[!UICONTROL Publish]**&#x200B;或&#x200B;**[!UICONTROL Publish to Dynamic Media]**。
1. 選擇&#x200B;**[!UICONTROL OK]**。

### 使用管理出版物從Dynamic Media或Experience Manager選擇性取消發佈資產 {#selective-unpublish-manage-publication}

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後選取「**[!UICONTROL 資產]** > **[!UICONTROL 檔案]**」。
1. 在&#x200B;**[!UICONTROL 卡片視圖]**、**[!UICONTROL 列視圖]**&#x200B;或&#x200B;**[!UICONTROL 清單視圖]**&#x200B;中，執行以下操作之一：
   * 導覽至您要取消發佈其資產的資料夾。 選擇資料夾，然後在工具欄上選擇&#x200B;**[!UICONTROL 管理出版物]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，以便更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要取消發佈其資產的資料夾。 開啟資料夾，然後選取一或多個資產。 在工具欄上，選擇&#x200B;**[!UICONTROL 管理出版物]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，以便更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果工具欄上未顯示&#x200B;**[!UICONTROL 管理出版物]**，請改為選擇省略號按鈕，然後從清單菜單中選擇&#x200B;**[!UICONTROL 管理出版物]**。

1. 在&#x200B;**[!UICONTROL 管理出版物 — 選項]**&#x200B;頁的&#x200B;**[!UICONTROL 操作]**&#x200B;下，選擇您想要的取消激活類型。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL 取消發佈]** (從Experience Manager) | 如果您要從Experience Manager取消發佈資產，請選取此選項。 |
   | **[!UICONTROL 從 Dynamic Media 取消發佈]** | 如果您要從Dynamic Media取消發佈資產，請選取此選項。<br>只有在將Dynamic Media發佈模 **[!UICONTROL 式設]** 為資料夾屬性的 **[!UICONTROL 選擇]** 性發佈時，才可使用此選項。 |

1. 在&#x200B;**[!UICONTROL Schedule]**&#x200B;下，設定取消激活的時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 選取以立即取消發佈資產。 |
   | **[!UICONTROL 稍後]** | 選取，在特定日期和時間取消發佈資產。 |

1. 在&#x200B;**[!UICONTROL 管理出版物]**&#x200B;頁面的右上角，選擇&#x200B;**[!UICONTROL Next]**。
1. 在&#x200B;**[!UICONTROL 管理發布 — 範圍]**&#x200B;頁中，執行下列操作之一：
   * 選取您要從取消發佈中移除的一或多個資產。
   * 在&#x200B;**[!UICONTROL 管理出版物 — 範圍]**&#x200B;頁面的右上角，選擇&#x200B;**[!UICONTROL 取消發佈]**&#x200B;或&#x200B;**[!UICONTROL 從Dynamic Media取消發佈]**。
1. 選擇&#x200B;**[!UICONTROL OK]**。

## 使用快速發佈將資產發佈至Dynamic Media或Experience Manager {#quick-publish-aem-dm}

對於簡單的資產啟用案例，您可以使用&#x200B;**[!UICONTROL 快速發佈]**。 **[!UICONTROL 快速發]** 布會立即發佈所選資產，不需進一步進行使用者互動。由於此動作，任何未發佈的參考也會自動發佈。

>[!NOTE]
>
>若要使用&#x200B;**[!UICONTROL 快速發佈]**&#x200B;將資產發佈至Dynamic Media或Experience Manager，請確定已在您的&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;或所選資料夾的資料夾屬性中啟用&#x200B;**[!UICONTROL 選擇性發佈]**。

**若要使用快速發佈將資產發佈至Dynamic Media或Experience Manager:**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在頁面左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後在頁面右側選取「**[!UICONTROL 資產]** > **[!UICONTROL 檔案]**」。
1. 在&#x200B;**[!UICONTROL 卡片視圖]**、**[!UICONTROL 列視圖]**&#x200B;或&#x200B;**[!UICONTROL 清單視圖]**&#x200B;中，執行以下操作之一：
   * 導覽至您要發佈其資產的資料夾。 選取資料夾，然後在工具列上選取&#x200B;**[!UICONTROL 快速發佈]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，以便更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的資料夾。 開啟資料夾，然後選取一或多個資產。 在工具欄上，選擇&#x200B;**[!UICONTROL 快速發佈]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，以便更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果工具列上未顯示&#x200B;**[!UICONTROL 快速發佈]**，請改為選擇省略號按鈕，然後從清單菜單中選擇&#x200B;**[!UICONTROL 快速發佈]**。

      ![資料夾層級快速發佈至Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 從&#x200B;**[!UICONTROL 快速發佈]**&#x200B;菜單清單中選擇以下選項之一。

   | 快速發佈選項 | 它的作用 |
   | --- | --- | 
   | 發佈至Experience Manager | 立即將選取的資產發佈至Experience Manager。 |
   | 發佈至 Brand Portal 網站 | 立即將選取的資產發佈至&#x200B;**[!UICONTROL Brand Portal]**。<br>只有在您的Experience Manager資產例項已設定Brand Portal時，才 **[!UICONTROL 可]** 使用此選項。 |
   | 發佈至 Dynamic Media | 立即將選取的資產發佈至Dynamic Media。<br>資產必須同步至Dynamic Media。如有必要，請確定資料夾屬性中的&#x200B;**[!UICONTROL 同步模式]**&#x200B;已設為&#x200B;**[!UICONTROL 將此資料夾子樹狀結構中的所有項目同步至Dynamic Media]**。 |

1. 選擇&#x200B;**[!UICONTROL OK]**，然後選擇&#x200B;**[!UICONTROL Close]**。

## 透過搜尋結果選擇性地發佈或取消發佈資產 {#selective-publish-unpublish-search-results}

搜尋結果可顯示具有不同Dynamic Media發佈設定之資產資料夾中的資產。 若您從搜尋結果中選取多個資產，且每個資產具有不同的Dynamic Media發佈模式設定，您可以從工具列觸發&#x200B;**[!UICONTROL 管理出版物]**&#x200B;以進行發佈或取消發佈。

另請參閱[在Experience Manager](/help/assets/search-assets.md)中搜尋資產。

**若要透過搜尋結果選擇性地發佈或取消發佈資產：**

1. 在Experience Manager的頁面左上角，選取Experience Manager標誌以存取全域導覽主控台。 在頁面左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後選取「**[!UICONTROL 資產]** > **[!UICONTROL 檔案]**」。
1. 在工具列的頁面右上角附近，選取「搜尋」圖示（放大鏡）。
1. 在&#x200B;**[!UICONTROL 鍵入以搜索]**&#x200B;文本欄位中，輸入關鍵字，然後按&#x200B;**[!UICONTROL Enter]**。
1. 在頁面的右上角附近，選取&#x200B;**[!UICONTROL 清單檢視]**&#x200B;圖示。
1. 在頁面的左上角附近，選取&#x200B;**[!UICONTROL Filters]**&#x200B;圖示。

   ![搜尋結果中的清單檢視和篩選器](/help/assets/assets-dm/select-publish-search-result.png)

1. 在左側面板中，展開&#x200B;**[!UICONTROL Status]**，然後展開&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;搜尋述詞。
1. 使用&#x200B;**[!UICONTROL Published]**&#x200B;和&#x200B;**[!UICONTROL Unpublished]**核取方塊，根據Dynamic Media資產的已發佈狀態進一步調整搜尋結果。
您可以選擇使用這些核取方塊搭配**[!UICONTROL Publish]**&#x200B;搜尋述詞來調整&#x200B;**[!UICONTROL Published]**&#x200B;和&#x200B;**[!UICONTROL Unpublished]** Experience Manager資產的搜尋結果。
1. 執行下列任一操作：
   * 選取您要發佈或取消發佈的一或多個資產。
   * 在&#x200B;**[!UICONTROL 搜索結果]**&#x200B;頁的右上角附近，選擇&#x200B;**[!UICONTROL 全選]**。
1. 在工具欄上，選擇&#x200B;**[!UICONTROL 管理出版物]**。 在工具欄上選擇刪節號表徵圖，以開啟&#x200B;**[!UICONTROL 管理出版物]**。
1. 在&#x200B;**[!UICONTROL 管理出版物 — 選項]**&#x200B;頁面上，選擇所需的操作。

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

1. 在&#x200B;**[!UICONTROL Schedule]**&#x200B;下，設定取消激活的時間。

   | 所選計畫 | 發生的情況 |
   | --- | --- |
   | 立即 | 會立即執行選取的動作。 |
   | 稍後 | 所選操作將在選定的特定日期和時間運行。 |

1. 在&#x200B;**[!UICONTROL 管理出版物 — 選項]**&#x200B;頁的右上角，選擇&#x200B;**[!UICONTROL 下一頁]**。
1. （選用）在&#x200B;**[!UICONTROL 管理出版物 — 範圍]**&#x200B;頁面中，檢閱表格中的&#x200B;**[!UICONTROL 發佈目標]**&#x200B;欄以取得所選資產。

   | 在Dynamic Media設定中發佈資產設定 | 所選操作 | 發佈目標 |
   | --- | --- | --- |
   | 激活後立即或<br> | 發佈 | Experience Manager和Dynamic Media |
   | 激活後立即或<br> | 發佈至 Dynamic Media | 無 |
   | 選擇性發佈 | 發佈 | Experience Manager |
   | 選擇性發佈 | 發佈至 Dynamic Media | Dynamic Media |
   | 激活後立即或<br> | 未發佈 | Experience Manager和Dynamic Media |
   | 激活後立即或<br> | 從 Dynamic Media 取消發佈 | 無 |
   | 選擇性發佈 | 未發佈 | Experience Manager |
   | 選擇性發佈 | 從 Dynamic Media 取消發佈 | Dynamic Media |

1. 在&#x200B;**[!UICONTROL 管理發布 — 範圍]**&#x200B;頁中，執行下列操作之一：
   * 選取您要從發佈或取消發佈中移除的一或多個資產。
   * 在&#x200B;**[!UICONTROL 管理出版物 — 範圍]**&#x200B;頁面的右上角，選擇&#x200B;**[!UICONTROL Publish]**&#x200B;或&#x200B;**[!UICONTROL Unpublish]**&#x200B;以開始操作。
1. 選擇&#x200B;**[!UICONTROL OK]**。

## 檢查資產的發佈狀態 {#check-publish-status-of-asset}

您可以在Experience Manager中使用&#x200B;**[!UICONTROL 時間軸]**&#x200B;搭配&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**，快速檢查資產的發佈狀態。

**若要檢查資產的發佈狀態：**

1. 在Experience Manager的頁面左上角，選取Experience Manager標誌以存取全域導覽主控台。 在頁面左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後選取「**[!UICONTROL 資產]** > **[!UICONTROL 檔案]**」。
1. 在&#x200B;**[!UICONTROL 卡片視圖]**、**[!UICONTROL 欄視圖]**&#x200B;或&#x200B;**[!UICONTROL 清單視圖]**（下面螢幕截圖顯示&#x200B;**[!UICONTROL 清單視圖]**）中，開啟包含您已發佈或未發佈的資產的資料夾。
1. 選取資產，使其以勾選記號顯示。 如需範例，請參閱下方的螢幕擷圖。
1. 在頁面的左上角附近，從下拉式選單中選取&#x200B;**[!UICONTROL 時間軸]**。 左側面板中的&#x200B;**[!UICONTROL 狀態]**區域顯示所選資產的發佈狀態。
使用**[!UICONTROL 清單檢視]**&#x200B;時，會出現額外的&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;發佈狀態欄。
   * 設定為同步至Dynamic Media的資料夾依預設會顯示&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;欄。
   * 設為&#x200B;*not*且已設為同步至Dynamic Media的資料夾不會顯示Dynamic Media欄。
      ![清單檢視和時間軸](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 疑難排解選擇性發佈 {#selective-publish-troubleshoot}

資產未同步至Dynamic Media，但其上觸發了Dynamic Media發佈動作，會導致下列錯誤訊息和解決方案：

![選擇性發佈錯誤](/help/assets/assets-dm/selective-publish-error.png)
