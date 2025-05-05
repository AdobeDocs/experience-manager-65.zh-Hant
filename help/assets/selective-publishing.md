---
title: 在 Dynamic Media 中使用選擇性發佈
description: 您可以選擇在檔案夾層級向Adobe Experience Manager或Dynamic Media發佈或取消發佈資產。 您可以使用管理出版物或快速Publish ，而非僅能依賴在Dynamic Media執行個體使用相同資料夾設定的Dynamic Media組態。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publishing
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3000'
ht-degree: 3%

---

# 在Dynamic Media中設定資料夾層級的選擇性發佈 {#selective-publish-configure-folder}

您可以選擇在檔案夾層級向Adobe Experience Manager或Dynamic Media發佈或取消發佈資產。 您可以使用&#x200B;**[!UICONTROL 管理出版物]**&#x200B;或&#x200B;**[!UICONTROL 快速Publish]**，而不是僅能依賴其設定為在Dynamic Media執行個體中所有資料夾通用的的&#x200B;**[!UICONTROL Dynamic Media組態]**。

例如，使用選擇性發佈，您可以處理尚未上線的產品資產。 在這種情況下，行銷團隊可以存取同步至Dynamic Media的智慧型裁切影像和動態轉譯。 他們可以建立促銷文宣，而完全無須將這些資產發佈至Dynamic Media以進行全球傳送。

>[!IMPORTANT]
>
>選擇性Publish僅適用於Dynamic Media - Scene7模式。

>[!NOTE]
>
>*將*&#x200B;個資產複製到資料夾或從資料夾複製資料夾會清除這些資產的發佈狀態。 不過，當您&#x200B;*將*&#x200B;資產移至其資料夾屬性設為&#x200B;**[!UICONTROL 選擇性Publish]**&#x200B;的資料夾，或從這些資料夾移動資產時，系統會維持這些資產的發佈狀態。

如果您稍後決定變更資料夾中的&#x200B;**[!UICONTROL 選擇性Publish]**&#x200B;設定，這些變更只會影響您從此時間點上傳至該資料夾的新資產。 資料夾中現有資產的發佈狀態維持不變，直到您從&#x200B;**[!UICONTROL 快速Publish]**&#x200B;或&#x200B;**[!UICONTROL 管理出版物]**&#x200B;對話方塊手動變更為止。

資料夾層級&#x200B;**[!UICONTROL Dynamic Media Publish模式]**&#x200B;選項一律預設為在&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;中的&#x200B;**[!UICONTROL Publish Assets]**&#x200B;設定中找到的值。 不過，本主題中的下列步驟會說明如何在資料夾層級手動變更此預設值（如下列步驟所述）以覆寫&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;值。

無論您是否仰賴下列其中一項：

* 在&#x200B;**[!UICONTROL Publish設定]**&#x200B;中設定的&#x200B;**[!UICONTROL Dynamic Media Assets]**&#x200B;值。
* 在資料夾層級屬性中設定&#x200B;**[!UICONTROL Dynamic Media Publish模式]**&#x200B;值。

您可以選擇&#x200B;**[!UICONTROL 立即]**、**[!UICONTROL 啟動時]**&#x200B;或&#x200B;**[!UICONTROL 選擇性Publish]**。 例如，您可以在&#x200B;**[!UICONTROL Publish組態]**&#x200B;中將&#x200B;**[!UICONTROL Dynamic Media Assets]**&#x200B;值設定為&#x200B;**[!UICONTROL 啟動時]**，但在資料夾層級將&#x200B;**[!UICONTROL Dynamic Media Publish]**&#x200B;模式值設定為&#x200B;**[!UICONTROL 選擇性Publish]**，反之亦然。

在資料夾中設定選擇性發佈後，您可以執行下列任一項作業：

* [選擇性地使用管理出版物](#selective-publish-manage-publication)將資產發佈到Dynamic Media或Experience Manager。
* [選擇性地取消發佈Dynamic Media或Experience Manager中的資產（使用管理出版物](#selective-unpublish-manage-publication)）。
* [Publish資產到Dynamic Media或使用快速Publish進行Experience Manager](#quick-publish-aem-dm)。
* [透過搜尋結果選擇性地發佈或取消發佈資產](#selective-publish-unpublish-search-results)。

**若要在Dynamic Media的資料夾層級設定選擇性發佈：**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後選取&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 檔案]**。
1. 執行下列任一項作業：
   * 編輯現有資料夾的內容 — 在&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**&#x200B;中，瀏覽至您要編輯其內容的資料夾。 選取資料夾，然後在工具列上選取&#x200B;**[!UICONTROL 屬性]**。
   * 編輯新資料夾的內容 — 在&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**&#x200B;中，在頁面的右上角附近，選取&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 資料夾]**。 在&#x200B;**[!UICONTROL 建立資料夾]**&#x200B;對話方塊中，輸入資料夾的標題（必要），然後選取&#x200B;**[!UICONTROL 建立]**。 選取資料夾，然後在工具列上選取&#x200B;**[!UICONTROL 屬性]**。

1. 在&#x200B;**[!UICONTROL 同步模式]**&#x200B;下拉式清單中，選取下列其中一項：

   | 同步模式 | 說明 |
   | --- | --- |
   | **[!UICONTROL 已繼承]** | 資料夾上沒有明確的同步值；而是從資料夾的其中一個上階資料夾或在&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;中設定的預設模式繼承同步值。 **[!UICONTROL 已繼承]**&#x200B;的詳細狀態會透過工具提示顯示。 |
   | **[!UICONTROL 將此資料夾子樹狀結構中的所有專案同步至Dynamic Media]** | 資產必須同步至Dynamic Media，才能成功發佈至Dynamic Media。 選取此選項會包含此子樹狀結構中要同步至Dynamic Media的所有資產。 資料夾特定設定會覆寫&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;中的預設設定。 |
   | **[!UICONTROL 從Dynamic Media同步處理排除此資料夾子樹狀結構中的所有專案]** | 排除此子樹狀結構中的所有資產，使其無法同步至Dynamic Media。 |

   ![資料夾層級選擇性發佈](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 在&#x200B;**[!UICONTROL Dynamic Media Publish模式]**&#x200B;下拉式清單中，選取選項。 **[!UICONTROL Dynamic Media Publish模式]**&#x200B;選項一律預設為&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;中設定的值。 不過，您可以使用下列其中一個選項，手動覆寫此預設&#x200B;**[!UICONTROL Dynamic Media組態]**&#x200B;值。

   >[!IMPORTANT]
   >
   >無論您選取的Dynamic Media Publish模式選項為何，若您稍後對&#x200B;*已發佈*&#x200B;的資產進行任何更新，這些更新都會立即發佈，使用者毋須採取任何進一步動作。
   >
   >如果發佈的視訊已更新，則必須再次發佈以反映傳送上的變更。

   | Dynamic Media Publish模式選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 將資產上傳至此資料夾時，系統會將這些資產擷取至Experience Manager，並立即提供URL/內嵌。 此選項僅繫結至Experience Manager發佈，使用者不需要介入即可發佈資產。<br>如果您在上一個步驟中選取&#x200B;**[!UICONTROL 從Dynamic Media同步處理]** （在&#x200B;**[!UICONTROL 同步處理模式]**&#x200B;中），排除此資料夾子樹狀結構中的所有專案&#x200B;**，則此選項將無法。 |
   | **[!UICONTROL 啟動時]** | 將資產上傳至此資料夾時，您必須先明確發佈資產，才能提供URL/內嵌連結。 此選項僅與Experience Manager發佈繫結。<br>如果您在上一個步驟中選取&#x200B;**[!UICONTROL 從Dynamic Media同步處理]** （在&#x200B;**[!UICONTROL 同步處理模式]**&#x200B;中），排除此資料夾子樹狀結構中的所有專案&#x200B;**，則此選項將無法。 |
   | **[!UICONTROL 選擇性Publish]** | Assets會發佈至您選擇的Experience Manager或Dynamic Media，以便在公共網域中傳送。 這兩種發佈方法彼此互斥。 也就是說，您可以將資產發佈至DMS7，以使用智慧型裁切或動態轉譯等功能。 或者，您可以將資產僅發佈到Experience Manager以進行安全預覽；這些相同的資產&#x200B;*不會*&#x200B;發佈到DMS7以在公共網域中傳送。 如果您在上一個步驟中選取&#x200B;**[!UICONTROL 從Dynamic Media同步處理]** （在&#x200B;**[!UICONTROL 同步處理模式]**&#x200B;中）排除此資料夾子樹狀結構中的所有專案，則此選項無法使用。 |

1. 在頁面的右上角，選取「**[!UICONTROL 儲存並關閉]**」，然後選取「**[!UICONTROL 確定]**」以返回Experience Manager Assets。

## 選擇性地使用管理發布將資產發佈到Dynamic Media或Experience Manager{#selective-publish-manage-publication}

使用&#x200B;**[!UICONTROL 管理出版物]**&#x200B;選擇性地將資產發佈到Dynamic Media或Experience Manager之前，請確定您已設定下列其中一項：

* **[!UICONTROL Publish組態]**&#x200B;至&#x200B;**[!UICONTROL 選擇性Assets]**&#x200B;中的&#x200B;**[!UICONTROL Dynamic Media Publish]**&#x200B;選項
* 已設定資料夾層級的選擇性發佈。

請參閱[建立Dynamic Media設定](#configuring-dynamic-media-cloud-services)或[在Dynamic Media中設定資料夾層級的選擇性發佈](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>選擇性Publish僅適用於Dynamic Media - Scene7模式。

>[!NOTE]
>
>*將*&#x200B;個資產複製到資料夾或從資料夾複製資料夾會清除這些資產的發佈狀態。 不過，當您&#x200B;*將*&#x200B;資產移至其資料夾屬性設為&#x200B;**[!UICONTROL 選擇性Publish]**&#x200B;的資料夾，或從這些資料夾移動資產時，系統會維持這些資產的發佈狀態。

**若要使用管理出版物選擇性地將資產發佈到Dynamic Media或Experience Manager：**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後選取&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 檔案]**。
1. 在&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**&#x200B;中，執行下列其中一項作業：
   * 導覽至您要發佈其資產的資料夾。 選取資料夾，然後在工具列上選取&#x200B;**[!UICONTROL 管理出版物]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，以便更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的資料夾。 開啟資料夾，然後選取一或多個資產。 在工具列中選取&#x200B;**[!UICONTROL 管理出版物]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，以便更輕鬆地檢查特定資產的發佈狀態。

     >[!NOTE]
     >
     >如果工具列上看不到&#x200B;**[!UICONTROL 管理出版物]**，請改為選取省略符號按鈕，然後從清單選單中選取&#x200B;**[!UICONTROL 管理出版物]**。

1. 在&#x200B;**[!UICONTROL 管理出版物 — 選項]**&#x200B;頁面的&#x200B;**[!UICONTROL 動作]**&#x200B;下方，選取您想要的啟動型別。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL Publish]** (要Experience Manager) | 選取此選項，您就可以將資產發佈到Experience Manager以進行安全預覽。 |
   | **[!UICONTROL Publish到Dynamic Media]** | 選取此選項，您就可以將資產發佈到Dynamic Media以在公共域中傳送，或者也可以使用智慧型裁切或動態轉譯等功能。<br>只有資料夾屬性中的&#x200B;**[!UICONTROL Dynamic Media Publish模式]**&#x200B;設定為&#x200B;**[!UICONTROL 選擇性Publish]**&#x200B;時，才能使用此選項。 |

1. 在&#x200B;**[!UICONTROL 排程]**&#x200B;底下，設定發佈時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 現在]** | 選取以立即發佈資產。 |
   | **[!UICONTROL 稍後]** | 選取此項可在特定日期和時間發佈資產。 |

1. 在&#x200B;**[!UICONTROL 管理出版物]**&#x200B;頁面的右上角，選取&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL 管理出版物 — 範圍]**&#x200B;頁面中，執行下列任一項作業：

   * 如有必要，請選取一或多個您要從發佈中移除的資產。
   * 在&#x200B;**[!UICONTROL 管理出版物 — 範圍]**&#x200B;頁面的右上角，選取&#x200B;**[!UICONTROL Publish]**&#x200B;或&#x200B;**[!UICONTROL Publish到Dynamic Media]**。
1. 選取&#x200B;**[!UICONTROL 確定]**。

### 選擇性地從Dynamic Media取消發佈資產，或使用「管理發布」Experience Manager取消發佈資產 {#selective-unpublish-manage-publication}

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後選取&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 檔案]**。
1. 在&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**&#x200B;中，執行下列其中一項作業：
   * 導覽至您要取消發佈其資產的資料夾。 選取資料夾，然後在工具列上選取&#x200B;**[!UICONTROL 管理出版物]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，以便更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要取消發佈其資產的資料夾。 開啟資料夾，然後選取一或多個資產。 在工具列中選取&#x200B;**[!UICONTROL 管理出版物]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，以便更輕鬆地檢查特定資產的發佈狀態。

     >[!NOTE]
     >
     >如果工具列上看不到&#x200B;**[!UICONTROL 管理出版物]**，請改為選取省略符號按鈕，然後從清單選單中選取&#x200B;**[!UICONTROL 管理出版物]**。

1. 在&#x200B;**[!UICONTROL 管理出版物 — 選項]**&#x200B;頁面的&#x200B;**[!UICONTROL 動作]**&#x200B;下方，選取您想要的停用型別。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL 取消發佈]** (從Experience Manager) | 如果要從Experience Manager中取消發佈資產，請選取此選項。 |
   | **[!UICONTROL 從Dynamic Media取消發佈]** | 如果要從Dynamic Media取消發佈資產，請選取此選項。<br>只有資料夾屬性中的&#x200B;**[!UICONTROL Dynamic Media Publish模式]**&#x200B;設定為&#x200B;**[!UICONTROL 選擇性Publish]**&#x200B;時，才能使用此選項。 |

1. 在&#x200B;**[!UICONTROL 排程]**&#x200B;下，設定停用時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 現在]** | 選取以立即取消發佈資產。 |
   | **[!UICONTROL 稍後]** | 選取此項可在特定日期和時間取消發佈資產。 |

1. 在&#x200B;**[!UICONTROL 管理出版物]**&#x200B;頁面的右上角，選取&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**[!UICONTROL 管理出版物 — 範圍]**&#x200B;頁面中，執行下列任一項作業：
   * 選取一或多個要從取消發佈中移除的資產。
   * 在&#x200B;**[!UICONTROL 管理出版物 — 範圍]**&#x200B;頁面的右上角，選取&#x200B;**[!UICONTROL 取消發佈]**&#x200B;或&#x200B;**[!UICONTROL 從Dynamic Media取消發佈]**。
1. 選取&#x200B;**[!UICONTROL 確定]**。

## Publish資產移至Dynamic Media或使用Quick Publish進行Experience Manager {#quick-publish-aem-dm}

對於簡單的資產啟用案例，您可以使用&#x200B;**[!UICONTROL 快速Publish]**。 **[!UICONTROL 快速Publish]**&#x200B;會立即發佈選取的資產，使用者不再進行任何互動。 因為此動作，所有未發佈的參考也會自動發佈。

>[!NOTE]
>
>若要使用&#x200B;**[!UICONTROL 快速Publish]**&#x200B;將資產發佈至Dynamic Media或Experience Manager，請確定&#x200B;**[!UICONTROL 選擇性Publish]**&#x200B;已在您的&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;或所選資料夾的資料夾屬性中啟用。

**若要使用Quick Publish將資產發佈到Dynamic Media或Experience Manager：**

1. 在Experience Manager中，選取Experience Manager標誌以存取全域導覽主控台。 在頁面左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後在頁面右側，選取&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 檔案]**。
1. 在&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**&#x200B;中，執行下列其中一項作業：
   * 導覽至您要發佈其資產的資料夾。 選取資料夾，然後在工具列上選取&#x200B;**[!UICONTROL 快速Publish]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，以便更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的資料夾。 開啟資料夾，然後選取一或多個資產。 在工具列上，選取&#x200B;**[!UICONTROL 快速Publish]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，以便更輕鬆地檢查特定資產的發佈狀態。

     >[!NOTE]
     >
     >如果工具列上看不到&#x200B;**[!UICONTROL 快速Publish]**，請改為選取省略符號按鈕，然後從清單選單中選取&#x200B;**[!UICONTROL 快速Publish]**。

     ![將資料夾層級的快速Publish傳送至Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 從&#x200B;**[!UICONTROL 快速Publish]**&#x200B;功能表清單中選取下列其中一個選項。

   | 快速Publish選項 | 作用 |
   | --- | --- | 
   | Publish至Experience Manager | 立即發佈選取的資產以Experience Manager。 |
   | 發佈至 Brand Portal 網站 | 立即將選取的資產發佈至&#x200B;**[!UICONTROL Brand Portal]**。<br>只有在您的Experience Manager Assets執行個體已設定&#x200B;**[!UICONTROL Brand Portal]**&#x200B;時，才能使用此選項。 |
   | 發佈至 Dynamic Media | 立即將選取的資產發佈至Dynamic Media。<br>資產必須同步至Dynamic Media。 如有必要，請確定資料夾屬性中的&#x200B;**[!UICONTROL 同步模式]**&#x200B;已設定為&#x200B;**[!UICONTROL 將此資料夾子樹狀結構中的所有專案同步至Dynamic Media]**。 |

1. 選取&#x200B;**[!UICONTROL 確定]**，然後選取&#x200B;**[!UICONTROL 關閉]**。

## 透過搜尋結果選擇性地發佈或取消發佈資產 {#selective-publish-unpublish-search-results}

搜尋結果會顯示不同Dynamic Media發佈設定的資產資料夾中的資產。 當您從搜尋結果中選取多個資產，且每個資產都有不同的Dynamic Media發佈模式設定時，您可以從工具列觸發&#x200B;**[!UICONTROL 管理出版物]**&#x200B;以發佈或取消發佈。

另請參閱[搜尋Experience Manager](/help/assets/search-assets.md)中的資產。

**若要透過搜尋結果選擇性地發佈或取消發佈資產：**

1. 在Experience Manager中，在頁面的左上角選取Experience Manager標誌以存取全域導覽主控台。 在頁面左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後選取&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 檔案]**。
1. 在工具列上，在頁面的右上角附近，選取「搜尋」圖示（放大鏡）。
1. 在&#x200B;**[!UICONTROL 輸入以搜尋]**&#x200B;文字欄位中，輸入關鍵字，然後按&#x200B;**[!UICONTROL Enter]**。
1. 在頁面的右上角附近，選取&#x200B;**[!UICONTROL 清單檢視]**&#x200B;圖示。
1. 在頁面的左上角附近，選取&#x200B;**[!UICONTROL 篩選器]**&#x200B;圖示。

   ![搜尋結果中的清單檢視和篩選器](/help/assets/assets-dm/select-publish-search-result.png)

1. 在左側面板中，展開&#x200B;**[!UICONTROL 狀態]**，然後展開&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;搜尋述詞。
1. 使用&#x200B;**[!UICONTROL 已發佈]**&#x200B;和&#x200B;**[!UICONTROL 已取消發佈]**&#x200B;核取方塊，根據Dynamic Media資產的已發佈狀態進一步調整搜尋結果。
您可以選擇性將這些核取方塊與&#x200B;**[!UICONTROL Publish]**&#x200B;搜尋述詞搭配使用，以精簡&#x200B;**[!UICONTROL 已發佈]**&#x200B;和&#x200B;**[!UICONTROL 已取消發佈]** Experience Manager資產的搜尋結果。
1. 執行下列任一項作業：
   * 選取一或多個要發佈或取消發佈的資產。
   * 在&#x200B;**[!UICONTROL 搜尋結果]**&#x200B;頁面的右上角附近，選取&#x200B;**[!UICONTROL 全選]**。
1. 在工具列中選取&#x200B;**[!UICONTROL 管理出版物]**。 選取工具列上的省略符號圖示，以開啟&#x200B;**[!UICONTROL 管理出版物]**。
1. 在&#x200B;**[!UICONTROL 管理出版物 — 選項]**&#x200B;頁面上，選取所需的動作。

   | 選取的動作 | Dynamic Media組態中的Publish Assets設定 | Assets是 |
   | --- | --- | --- |
   | 發佈 | 立即或啟動時 | 已發佈至Experience Manager和Dynamic Media。 |
   | 發佈 | 選擇性發佈 | 僅發佈至Experience Manager。 |
   | 未發佈 | 立即或啟動時 | 已從Experience Manager和Dynamic Media取消發佈。 |
   | 未發佈 | 選擇性發佈 | 僅從Experience Manager取消發佈。 |
   | 發佈至 Dynamic Media | 立即或啟動時 | 未發佈至Experience Manager或Dynamic Media，或兩者皆有。 |
   | 發佈至 Dynamic Media | 選擇性發佈 | 僅發佈至Dynamic Media。 |
   | 從 Dynamic Media 取消發佈 | 立即或啟動時 | 不會從Experience Manager或Dynamic Media （或兩者）取消發佈。 |
   | 從 Dynamic Media 取消發佈 | 選擇性發佈 | 僅從Dynamic Media取消發佈。 |

1. 在&#x200B;**[!UICONTROL 排程]**&#x200B;下，設定停用時間。

   | 選取的排程 | 發生什麼情況 |
   | --- | --- |
   | 現在 | 選取的動作會立即執行。 |
   | 稍後 | 選取的動作會在選取的特定日期和時間執行。 |

1. 在&#x200B;**[!UICONTROL 管理出版物 — 選項]**&#x200B;頁面的右上角，選取&#x200B;**[!UICONTROL 下一步]**。
1. （選擇性）在&#x200B;**[!UICONTROL 管理發布 — 範圍]**&#x200B;頁面中，檢閱資料表中所選資產的&#x200B;**[!UICONTROL Publish Target]**&#x200B;欄。

   | Dynamic Media組態中的Publish Assets設定 | 選取的動作 | 發佈目標 |
   | --- | --- | --- |
   | 立即或<br>啟動時 | 發佈 | Experience Manager與Dynamic Media |
   | 立即或<br>啟動時 | 發佈至 Dynamic Media | 無 |
   | 選擇性發佈 | 發佈 | Experience Manager |
   | 選擇性發佈 | 發佈至 Dynamic Media | Dynamic Media |
   | 立即或<br>啟動時 | 未發佈 | Experience Manager與Dynamic Media |
   | 立即或<br>啟動時 | 從 Dynamic Media 取消發佈 | 無 |
   | 選擇性發佈 | 未發佈 | Experience Manager |
   | 選擇性發佈 | 從 Dynamic Media 取消發佈 | Dynamic Media |

1. 在&#x200B;**[!UICONTROL 管理出版物 — 範圍]**&#x200B;頁面中，執行下列任一項作業：
   * 選取一或多個要從發佈或取消發佈中移除的資產。
   * 在&#x200B;**[!UICONTROL 管理出版物 — 範圍]**&#x200B;頁面的右上角，選取&#x200B;**[!UICONTROL Publish]**&#x200B;或&#x200B;**[!UICONTROL 取消發佈]**&#x200B;以開始動作。
1. 選取&#x200B;**[!UICONTROL 確定]**。

## 檢查資產的發佈狀態 {#check-publish-status-of-asset}

您可以在Experience Manager中使用&#x200B;**[!UICONTROL 時間表]**&#x200B;搭配&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**&#x200B;來快速檢查資產的發佈狀態。

**若要檢查資產的發佈狀態：**

1. 在Experience Manager中，在頁面的左上角選取Experience Manager標誌以存取全域導覽主控台。 在頁面左側，選取「導覽」圖示（位於「工具」圖示的正上方），然後選取&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 檔案]**。
1. 在&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]** （下面的熒幕擷圖顯示&#x200B;**[!UICONTROL 清單檢視]**）中，開啟包含您已發佈或取消發佈之資產的資料夾。
1. 選取資產，使其出現時帶有核取記號。 如需範例，請參閱下方的熒幕擷圖。
1. 在頁面的左上角附近，從下拉式功能表中選取&#x200B;**[!UICONTROL 時間軸]**。 左側面板中的&#x200B;**[!UICONTROL 狀態]**&#x200B;區域會顯示所選資產的發佈狀態。
當您使用&#x200B;**[!UICONTROL 清單檢視]**&#x200B;時，**[!UICONTROL Dynamic Media]**&#x200B;發佈狀態的額外欄會出現。
   * 設定為同步至Dynamic Media的資料夾依預設會顯示&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;欄。
   * *未*設定為同步至Dynamic Media的資料夾不會顯示Dynamic Media資料行。

     ![清單檢視和時間表](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 疑難排解選擇性Publish {#selective-publish-troubleshoot}

尚未同步至Dynamic Media但已觸發Dynamic Media發佈動作的資產，會產生下列錯誤訊息和解決方案：

![選擇性Publish錯誤](/help/assets/assets-dm/selective-publish-error.png)
