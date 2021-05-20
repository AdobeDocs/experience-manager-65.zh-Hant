---
title: 在 Dynamic Media 中使用選擇性發佈
description: 關於如何在Dynamic Media中使用選擇性發佈的資訊。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: Business Practitioner, Administrator
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: 發佈
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '2935'
ht-degree: 4%

---

# 在Dynamic Media {#selective-publish-configure-folder}的資料夾層級設定選擇性發佈

您可以選擇使用&#x200B;**[!UICONTROL 管理出版物]**&#x200B;或&#x200B;**[!UICONTROL 快速發佈]**，在資料夾層級從AEM或Dynamic Media發佈或取消發佈資產，而非僅能依賴在Dynamic Media執行個體使用相同資料夾設定的&#x200B;**[!UICONTROL Dynamic Media組態]**。

例如，透過選擇性發佈，您可以針對尚未上線的產品使用資產。 在這種情況下，行銷團隊可以存取同步至Dynamic Media的智慧型裁切影像和動態轉譯，以便建立促銷文宣，而完全無需將這些資產發佈至Dynamic Media以進行全域傳送。

>[!IMPORTANT]
>
>「選擇性發佈」僅適用於Dynamic Media - Scene7模式。

>[!NOTE]
>
>** 將資產複製到資料夾和從資料夾複製會清除這些資產的發佈狀態。不過，當您將&#x200B;*移動*&#x200B;資產至資料夾屬性設為&#x200B;**[!UICONTROL 選擇性發佈]**&#x200B;的資料夾時，會維持這些資產的發佈狀態。

如果您稍後決定變更資料夾中的&#x200B;**[!UICONTROL 選擇性發佈]**&#x200B;設定，這些變更只會影響您從該時間點上傳至該資料夾的新資產。 資料夾中現有資產的發佈狀態會維持原狀，直到您從&#x200B;**[!UICONTROL 快速發佈]**&#x200B;或&#x200B;**[!UICONTROL 管理出版物]**&#x200B;對話方塊手動變更為止。

資料夾層級&#x200B;**[!UICONTROL Dynamic Media發佈模式]**&#x200B;選項一律預設為&#x200B;**[!UICONTROL Dynamic Media設定中**[!UICONTROL &#x200B;發佈資產&#x200B;]**設定中的值。]** 不過，本主題的下列步驟會示範如何手動變更資料夾層級的此預設值（如下列步驟所述），以覆寫 **[!UICONTROL Dynamic Media]** 設定值。

無論您是仰賴&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;中設定的&#x200B;**[!UICONTROL 發佈資產]**&#x200B;值，還是仰賴資料夾層級屬性中設定的&#x200B;**[!UICONTROL Dynamic Media發佈模式]**&#x200B;值，您仍可選擇「**[!UICONTROL 立即]**」、「**[!UICONTROL 啟用時]**」或「**[!UICONTROL 選擇性發佈」。]** 例如，您可以將 **[!UICONTROL Dynamic Media]** 設定中的「發佈資產」值設 **[!UICONTROL 為「啟]** 用時」 ****，但將資料夾層級的「Dynamic Media  **[!UICONTROL 發佈模式」值設為「]** 選擇性發佈 ****」，反之亦然，以此類推。

在資料夾中設定選擇性發佈後，您可以執行下列任一操作：

* [使用管理出版物選擇性地將資產發佈至Dynamic Media或AEM。](#selective-publish-manage-publication)
* [使用「管理出版物」從Dynamic Media或AEM選擇性取消發佈資產。](#selective-unpublish-manage-publication)
* [使用快速發佈將資產發佈至Dynamic Media或AEM。](#quick-publish-aem-dm)
* [透過搜尋結果選擇性地發佈或取消發佈資產。](#selective-publish-unpublish-search-results)

**若要在Dynamic Media的資料夾層級設定選擇性發佈**

1. 在AEM中，點選AEM標誌以存取全域導覽主控台。 在左側，點選「導覽」圖示（位於「工具」圖示上方），然後點選「**[!UICONTROL 資產>檔案」。]**
1. 執行下列任一操作：
   * 編輯現有資料夾的屬性 — 在&#x200B;**[!UICONTROL 卡片視圖]**、**[!UICONTROL 列視圖]**&#x200B;或&#x200B;**[!UICONTROL 清單視圖]**&#x200B;中，導航到要編輯其屬性的資料夾。 選取資料夾，然後在工具列上，點選「 **[!UICONTROL 屬性」。]**
   * 編輯新資料夾的屬性 — 在&#x200B;**[!UICONTROL 卡片視圖]**、**[!UICONTROL 列視圖]**&#x200B;或&#x200B;**[!UICONTROL 清單視圖]**&#x200B;中，在頁面右上角附近，點選&#x200B;**[!UICONTROL 建立>資料夾。]** 在「建 **[!UICONTROL 立資]** 料夾」對話方塊中，輸入資料夾的標題（必要），然後點選「建 **[!UICONTROL 立」。]** 選取資料夾，然後在工具列上，點選「屬 **[!UICONTROL 性」。]**

1. 在&#x200B;**[!UICONTROL 同步模式]**&#x200B;下拉清單中，選擇以下選項之一：

   | 同步模式 | 說明 |
   | --- | --- |
   | **[!UICONTROL 已繼承]** | 資料夾上沒有明確的同步值；相反，資料夾會繼承其上階資料夾中的一個同步值，或繼承&#x200B;**[!UICONTROL Dynamic Media配置中設定的預設模式。]** 通過工具提 **** 示顯示「繼承」的詳細狀態。 |
   | **[!UICONTROL 將此子樹狀結構資料夾的所有項目同步至 dynamicmedia]** | 若要發佈至Dynamic Media成功，必須將資產同步至Dynamic Media。 選取此選項，會將所有資產納入此子樹狀結構中，以便同步至Dynamic Media。 資料夾特定設定會覆寫「**[!UICONTROL Dynamic Media設定」中的預設設定。]** |
   | **[!UICONTROL 從dynamicmedia同步中排除此資料夾子樹中的所有內容]** | 排除此子樹狀結構中的所有資產，使其不會同步至Dynamic Media。 |

   ![資料夾層級選擇性發佈](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 在&#x200B;**[!UICONTROL Dynamic Media發佈模式]**&#x200B;下拉式清單中，選取選項。 請注意，**[!UICONTROL Dynamic Media發佈模式]**&#x200B;選項一律預設為&#x200B;**[!UICONTROL Dynamic Media設定中設定的值。]** 不過，您可以使用下列其中一個選 **[!UICONTROL 項，]** 手動覆寫此預設的Dynamic Media設定值。

   >[!IMPORTANT]
   >
   >請注意，無論您選取的Dynamic Media發佈模式選項為何，您之後對已發佈&#x200B;*的資產所進行的任何更新，都會立即發佈這些更新，而不需進一步執行使用者動作。*

   | Dynamic Media發佈模式選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 資產上傳至此資料夾時，系統會將資產內嵌至AEM，並立即提供URL/內嵌。 此選項僅與AEM發佈系結，不需要使用者干預即可發佈資產。<br>如果您在上 ** 一步驟中選 **[!UICONTROL 取「從dynamicmedia同步模式排除此資料夾子樹中的所]** 有項 **[!UICONTROL 目」 ，則此]** 選項不可用。 |
   | **[!UICONTROL 啟動時]** | 資產上傳至此資料夾時，您必須先明確發佈資產，才能提供URL/內嵌連結。 此選項僅與AEM發佈系結。<br>如果您在上 ** 一步驟中選 **[!UICONTROL 取「從dynamicmedia同步模式排除此資料夾子樹中的所]** 有項 **[!UICONTROL 目」 ，則此]** 選項不可用。 |
   | **[!UICONTROL 選擇性發佈]** | 資產會發佈至您選擇的AEM或Dynamic Media，以便在公開網域中傳送。 兩種發佈方法彼此互斥。  也就是說，您可以將資產發佈至DMS7，以便使用智慧型裁切或動態轉譯等功能。 或者，您也可以只將資產發佈至AEM，以安全預覽；這些相同的資產是&#x200B;*not*&#x200B;發佈至DMS7以供在公共網域中傳遞。 如果您在上一步驟的&#x200B;**[!UICONTROL 同步模式]**&#x200B;中，從dynamicmedia sync ]**中選擇了**[!UICONTROL &#x200B;從此資料夾子樹中排除所有內容，則此選項不可用。 |

1. 在頁面的右上角，點選&#x200B;**[!UICONTROL 儲存並關閉]**，然後點選&#x200B;**[!UICONTROL 確定]**&#x200B;以返回AEM Assets。

## 使用管理出版物{#selective-publish-manage-publication}選擇性地將資產發佈至Dynamic Media或AEM

使用&#x200B;**[!UICONTROL 管理出版物]**&#x200B;以選擇性地將資產發佈至Dynamic Media或AEM之前，請確定您已將&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;中的&#x200B;**[!UICONTROL 發佈資產]**&#x200B;選項設為&#x200B;**[!UICONTROL 選擇性發佈]**，或在資料夾層級設定選擇性發佈。

請參閱在Dynamic Media](#selective-publish-configure-folder)中建立Dynamic Media設定](#configuring-dynamic-media-cloud-services)或在資料夾層級設定選擇性發佈[[

>[!IMPORTANT]
>
>「選擇性發佈」僅適用於Dynamic Media - Scene7模式。

>[!NOTE]
>
>** 將資產複製到資料夾和從資料夾複製會清除這些資產的發佈狀態。不過，當您將&#x200B;*移動*&#x200B;資產至資料夾屬性設為&#x200B;**[!UICONTROL 選擇性發佈]**&#x200B;的資料夾時，會維持這些資產的發佈狀態。

**若要使用「管理出版物」選擇性地將資產發佈至Dynamic Media或AEM**

1. 在AEM中，點選AEM標誌以存取全域導覽主控台。 在左側，點選「導覽」圖示（位於「工具」圖示上方），然後點選「**[!UICONTROL 資產>檔案」。]**
1. 在&#x200B;**[!UICONTROL 卡片視圖]**、**[!UICONTROL 列視圖]**&#x200B;或&#x200B;**[!UICONTROL 清單視圖]**&#x200B;中，執行以下操作之一：
   * 導覽至您要發佈其資產的資料夾。 選取資料夾，然後在工具列上，點選「 **[!UICONTROL 管理出版物」。]**  您可能會發現使用「清單檢 **[!UICONTROL 視」]** 是很有幫助的，這樣您就可以更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的資料夾。 開啟資料夾，然後選取一或多個資產。 在工具列上，點選&#x200B;**[!UICONTROL 管理出版物。]** 您可能會發現使用「清單檢 **[!UICONTROL 視」]** 很有幫助，這樣您就能更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果工具列上未顯示&#x200B;**[!UICONTROL 管理出版物]**，請改為點選省略號按鈕，然後從清單菜單中選擇&#x200B;**[!UICONTROL 管理出版物]**。

1. 在&#x200B;**[!UICONTROL 管理出版物 — 選項]**&#x200B;頁的&#x200B;**[!UICONTROL 操作]**&#x200B;下，選擇所需的激活類型。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL 發佈]** (至AEM) | 選取此選項可將資產發佈至AEM，以便安全預覽。 |
   | **[!UICONTROL 發佈至 Dynamic Media]** | 選取此選項可將資產發佈至Dynamic Media，以在公用網域中傳送，或者讓您可以使用智慧型裁切或動態轉譯等功能。<br>只有在將Dynamic Media發佈模 **[!UICONTROL 式設]** 為資料夾屬性的 **[!UICONTROL 選擇]** 性發佈時，才可使用此選項。 |

1. 在&#x200B;**[!UICONTROL Schedule]**&#x200B;下，設定發佈的時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 選取以立即發佈資產。 |
   | **[!UICONTROL 稍後]** | 選取以在特定日期和時間發佈資產。 |

1. 在&#x200B;**[!UICONTROL 管理出版物]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL Next.]**
1. 在&#x200B;**[!UICONTROL 管理發布 — 範圍]**&#x200B;頁中，執行下列操作之一：

   * 如有必要，請選取一或多個您要從發佈中移除的資產。
   * 在&#x200B;**[!UICONTROL 管理出版物 — 範圍]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL Publish]**&#x200B;或&#x200B;**[!UICONTROL Publish to Dynamic Media。]**
1. 點選&#x200B;**[!UICONTROL 確定。]**

### 使用管理出版物{#selective-unpublish-manage-publication}從Dynamic Media或AEM選擇性取消發佈資產

1. 在AEM中，點選AEM標誌以存取全域導覽主控台。 在左側，點選「導覽」圖示（位於「工具」圖示上方），然後點選「**[!UICONTROL 資產>檔案」。]**
1. 在&#x200B;**[!UICONTROL 卡片視圖]**、**[!UICONTROL 列視圖]**&#x200B;或&#x200B;**[!UICONTROL 清單視圖]**&#x200B;中，執行以下操作之一：
   * 導覽至您要取消發佈其資產的資料夾。 選取資料夾，然後在工具列上，點選「 **[!UICONTROL 管理出版物」。]**  您可能會發現使用「清單檢 **[!UICONTROL 視」]** 是很有幫助的，這樣您就可以更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要取消發佈其資產的資料夾。 開啟資料夾，然後選取一或多個資產。 在工具列上，點選&#x200B;**[!UICONTROL 管理出版物。]** 您可能會發現使用「清單檢 **[!UICONTROL 視」]** 很有幫助，這樣您就能更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果工具列上未顯示&#x200B;**[!UICONTROL 管理出版物]**，請改為點選省略號按鈕，然後從清單菜單中選擇&#x200B;**[!UICONTROL 管理出版物]**。

1. 在&#x200B;**[!UICONTROL 管理出版物 — 選項]**&#x200B;頁的&#x200B;**[!UICONTROL 操作]**&#x200B;下，選擇您想要的取消激活類型。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL 取消發佈]** (從AEM) | 選取此選項即可從AEM取消發佈資產。 |
   | **[!UICONTROL 從 Dynamic Media 取消發佈]** | 選取此選項，從Dynamic Media取消發佈資產。<br>只有在將Dynamic Media發佈模 **[!UICONTROL 式設]** 為資料夾屬性的 **[!UICONTROL 選擇]** 性發佈時，才可使用此選項。 |

1. 在&#x200B;**[!UICONTROL Schedule]**&#x200B;下，設定取消激活的時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 選取以立即取消發佈資產。 |
   | **[!UICONTROL 稍後]** | 選取，在特定日期和時間取消發佈資產。 |

1. 在&#x200B;**[!UICONTROL 管理出版物]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL Next.]**
1. 在&#x200B;**[!UICONTROL 管理發布 — 範圍]**&#x200B;頁中，執行下列操作之一：
   * 選取您要從取消發佈中移除的一或多個資產。
   * 在&#x200B;**[!UICONTROL 管理出版物 — 範圍]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 取消發佈]**&#x200B;或&#x200B;**[!UICONTROL 從Dynamic Media取消發佈。]**
1. 點選&#x200B;**[!UICONTROL 確定。]**

## 使用快速發佈{#quick-publish-aem-dm}將資產發佈至Dynamic Media或AEM

對於簡單的資產啟用案例，您可以使用&#x200B;**[!UICONTROL 快速發佈]**。 **[!UICONTROL 快速發]** 布會立即發佈所選資產，不需進一步進行使用者互動。因此，任何未發佈的參考也會自動發佈。

>[!NOTE]
>
>若要使用&#x200B;**[!UICONTROL 快速發佈]**&#x200B;將資產發佈至Dynamic Media或AEM，請確定已在您的&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;或所選資料夾的資料夾屬性中啟用&#x200B;**[!UICONTROL 選擇性發佈]**。

**若要使用快速發佈將資產發佈至Dynamic Media或AEM**

1. 在AEM中，點選AEM標誌以存取全域導覽主控台。 在頁面的左側，點選「導覽」圖示（就在「工具」圖示上方），然後在頁面的右側點選「**[!UICONTROL 資產>檔案」。]**
1. 在&#x200B;**[!UICONTROL 卡片視圖]**、**[!UICONTROL 列視圖]**&#x200B;或&#x200B;**[!UICONTROL 清單視圖]**&#x200B;中，執行以下操作之一：
   * 導覽至您要發佈其資產的資料夾。 選取資料夾，然後在工具列上，點選「 **[!UICONTROL 快速發佈」。]**  您可能會發現使用「清單檢 **[!UICONTROL 視」]** 是很有幫助的，這樣您就可以更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的資料夾。 開啟資料夾，然後選取一或多個資產。 在工具列上，點選&#x200B;**[!UICONTROL 快速發佈。]** 您可能會發現使用「清單檢 **[!UICONTROL 視」]** 很有幫助，這樣您就能更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果工具列上未顯示&#x200B;**[!UICONTROL 快速發佈]**，請點選省略號按鈕，然後從清單選單中選取&#x200B;**[!UICONTROL 快速發佈]**。

      ![資料夾層級快速發佈至Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 從&#x200B;**[!UICONTROL 快速發佈]**&#x200B;菜單清單中選擇以下選項之一。

   | 快速發佈選項 | 它的作用 |
   | --- | --- | 
   | 發佈至 AEM | 將選取的資產立即發佈至AEM。 |
   | 發佈至 Brand Portal 網站 | 立即將選取的資產發佈至&#x200B;**[!UICONTROL Brand Portal。]**<br>只有在您的AEM Assets執行個體已設定Brand Portal時，才**[!UICONTROL &#x200B;可&#x200B;]**使用此選項。 |
   | 發佈至 Dynamic Media | 立即將選取的資產發佈至Dynamic Media。<br>資產必須已同步至Dynamic Media。如有必要，請確保資料夾屬性中的&#x200B;**[!UICONTROL 同步模式]**&#x200B;已設定為&#x200B;**[!UICONTROL 將此資料夾子樹中的所有內容同步到dynamicmedia。]** |

1. 點選&#x200B;**[!UICONTROL OK]**，然後點選&#x200B;**[!UICONTROL 關閉。]**

## 透過搜尋結果{#selective-publish-unpublish-search-results}選擇性地發佈或取消發佈資產

搜尋結果可顯示具有不同Dynamic Media發佈設定之資產資料夾中的資產。 若您已從搜尋結果中選取一或多個資產，且這些資產具有不同的Dynamic Media發佈模式設定，您可以從工具列觸發&#x200B;**[!UICONTROL 管理出版物]**&#x200B;以發佈或取消發佈。

另請參閱[在AEM中搜尋資產。](/help/assets/search-assets.md)

**透過搜尋結果選擇性地發佈或取消發佈資產**

1. 在AEM中，在頁面的左上角，點選AEM標誌以存取全域導覽主控台。 在頁面左側，點選「導覽」圖示（位於「工具」圖示上方），然後點選「**[!UICONTROL 資產>檔案」。]**
1. 在工具列的頁面右上角附近，點選「搜尋」圖示（放大鏡）。
1. 在&#x200B;**[!UICONTROL 鍵入以搜索]**&#x200B;文本欄位中，輸入關鍵字，然後按&#x200B;**[!UICONTROL Enter鍵。]**
1. 在頁面的右上角附近，點選「 **[!UICONTROL 清單檢視]**」圖示。
1. 在頁面的左上角附近，點選「**[!UICONTROL 篩選器]**」圖示。

   ![搜尋結果中的清單檢視和篩選器](/help/assets/assets-dm/select-publish-search-result.png)

1. 在左側面板中，展開&#x200B;**[!UICONTROL Status]**，然後展開&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;搜尋述詞。
1. 使用&#x200B;**[!UICONTROL Published]**&#x200B;和&#x200B;**[!UICONTROL Unpublished]**核取方塊，根據Dynamic Media資產的已發佈狀態進一步調整搜尋結果。
或者，您可以選擇使用這些核取方塊搭配**[!UICONTROL Publish]**&#x200B;搜尋述詞來調整&#x200B;**[!UICONTROL Published]**&#x200B;和&#x200B;**[!UICONTROL Unpublished]** AEM資產的搜尋結果。
1. 執行下列任一操作：
   * 選取您要發佈或取消發佈的一或多個資產。
   * 在「**[!UICONTROL 搜尋結果]**」頁面的右上角附近，點選「**[!UICONTROL 全選」。]**
1. 在工具列上，點選&#x200B;**[!UICONTROL 管理出版物。]** 您可能需要點選工具列上的刪節號圖示，才能查看管理 **[!UICONTROL 出版物。]**
1. 在&#x200B;**[!UICONTROL 管理出版物 — 選項]**&#x200B;頁面上，選擇所需的操作。

   | 所選操作 | 在Dynamic Media設定中發佈資產設定 | 資產包括 |
   | --- | --- | --- |
   | 發佈 | 立即或激活後 | 發佈至AEM和Dynamic Media。 |
   | 發佈 | 選擇性發佈 | 僅發佈至AEM。 |
   | 未發佈 | 立即或激活後 | 未從AEM和Dynamic Media發佈。 |
   | 未發佈 | 選擇性發佈 | 僅從AEM取消發佈。 |
   | 發佈至 Dynamic Media | 立即或激活後 | 未發佈至AEM、Dynamic Media或兩者。 |
   | 發佈至 Dynamic Media | 選擇性發佈 | 僅發佈至Dynamic Media。 |
   | 從 Dynamic Media 取消發佈 | 立即或激活後 | 未從AEM或Dynamic Media或兩者取消發佈。 |
   | 從 Dynamic Media 取消發佈 | 選擇性發佈 | 僅從Dynamic Media取消發佈。 |

1. 在&#x200B;**[!UICONTROL Schedule]**&#x200B;下，設定取消激活的時間。

   | 所選計畫 | 發生的情況 |
   | --- | --- |
   | 立即 | 會立即執行選取的動作。 |
   | 稍後 | 所選操作將在選定的特定日期和時間運行。 |

1. 在&#x200B;**[!UICONTROL 管理出版物 — 選項]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 下一步。]**
1. （選用）在&#x200B;**[!UICONTROL 管理出版物 — 範圍]**&#x200B;頁面中，檢閱表格中的&#x200B;**[!UICONTROL 發佈目標]**&#x200B;欄以取得所選資產。

   | 在Dynamic Media設定中發佈資產設定 | 所選操作 | 發佈目標 |
   | --- | --- | --- |
   | 激活後立即或<br> | 發佈 | AEM和Dynamic Media |
   | 激活後立即或<br> | 發佈至 Dynamic Media | 無 |
   | 選擇性發佈 | 發佈 | AEM |
   | 選擇性發佈 | 發佈至 Dynamic Media | Dynamic Media |
   | 激活後立即或<br> | 未發佈 | AEM和Dynamic Media |
   | 激活後立即或<br> | 從 Dynamic Media 取消發佈 | 無 |
   | 選擇性發佈 | 未發佈 | AEM |
   | 選擇性發佈 | 從 Dynamic Media 取消發佈 | Dynamic Media |

1. 在&#x200B;**[!UICONTROL 管理發布 — 範圍]**&#x200B;頁中，執行下列操作之一：
   * 選取您要從發佈或取消發佈中移除的一或多個資產。
   * 在&#x200B;**[!UICONTROL 管理出版物 — 範圍]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL Publish]**&#x200B;或&#x200B;**[!UICONTROL Unpublish]**&#x200B;以開始動作。
1. 點選&#x200B;**[!UICONTROL 確定。]**

## 檢查資產{#check-publish-status-of-asset}的發佈狀態

您可以在AEM中使用&#x200B;**[!UICONTROL 時間軸]**&#x200B;搭配&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**，快速檢查資產的發佈狀態。

**檢查資產的發佈狀態**

1. 在AEM中，在頁面的左上角，點選AEM標誌以存取全域導覽主控台。 在頁面左側，點選「導覽」圖示（位於「工具」圖示上方），然後點選「**[!UICONTROL 資產>檔案」。]**
1. 在&#x200B;**[!UICONTROL 卡片視圖]**、**[!UICONTROL 欄視圖]**&#x200B;或&#x200B;**[!UICONTROL 清單視圖]**（下面螢幕截圖顯示&#x200B;**[!UICONTROL 清單視圖]**）中，開啟包含您已發佈或未發佈的資產的資料夾。
1. 選取資產，使其以勾選記號顯示。 如需範例，請參閱下方的螢幕擷圖。
1. 在頁面的左上角附近，從下拉式選單中選取「**[!UICONTROL 時間軸」。]** 左 **** 側面板中的「狀態」區域會顯示所選資產的發佈狀態。使用&#x200B;**[!UICONTROL 清單檢視]**&#x200B;時，會出現額外的&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;發佈狀態欄。
   * 設為同步至Dynamic Media的資料夾依預設會顯示&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;欄。
   * 設為&#x200B;*not*且已設為同步至Dynamic Media的資料夾將不會顯示Dynamic Media欄。
      ![清單檢視和時間軸](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 疑難排解選擇性發佈{#selective-publish-troubleshoot}

資產未同步至Dynamic Media，但其上觸發了Dynamic Media發佈動作，會導致下列錯誤訊息和解決方案：

![選擇性發佈錯誤](/help/assets/assets-dm/selective-publish-error.png)
