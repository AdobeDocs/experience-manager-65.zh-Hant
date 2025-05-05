---
title: 使用版面模式調整最適化表單元件的大小
description: 使用版面配置模式中可用的回應式格線來定義元件位置
feature: Adaptive Forms,Foundation Components
exl-id: 5cf76cb1-c92c-4aed-9945-37494fef2d29
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 6%

---

# 使用版面模式調整元件大小 {#use-layout-mode-to-resize-components}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/resize-using-layout-mode.html?lang=zh-Hant&) |
| AEM 6.5 | 本文章 |


最適化表單製作介面可讓您使用版面模式調整元件大小。 在欄中拖放藍點以定義起始點和終止點來定位元件。 點選回應式格線中的元件後，系統會顯示藍點。 回應式格線由12個相等的欄組成。 替代欄中的白色和藍色陰影可區分一欄與另一欄。

您可以使用「配置」模式來調整所有裝置型別（例如桌上型電腦、平板電腦、手機和其他小型裝置）的元件大小。 平板電腦會自動從桌上型電腦版本衍生配置組態，而較小的裝置則會從手機衍生配置組態。 不過，您可以覆寫自動衍生的配置，以針對每種裝置型別定義不同的配置。

## 存取配置模式 {#access-layout-mode}

從出現在最適化表單製作介面頂端、**預覽**&#x200B;選項旁的下拉式清單中選取&#x200B;**版面配置**。 表單會以「版面」模式顯示。

1. 登入AEM作者執行個體並導覽至&#x200B;**Adobe Experience Manager** > **Forms** > **Forms和檔案**。
1. 建立[最適化表單](../../forms/using/creating-adaptive-form.md)或開啟現有的表單。
1. 從位於&#x200B;**預覽**&#x200B;選項旁上方的下拉式清單中選取&#x200B;**配置**。 表單會以「版面」模式顯示。

   ![配置模式](assets/layout_mode_ic_new.png)

## 調整元件大小 {#resize-components}

1. 在「版面」模式中，選取要調整大小的元件。 藍點會顯示在回應式格線的開始和結尾。
1. 拖放藍點以定義元件在回應式格線中的位置。

   ![使用配置模式調整大小](assets/layout_mode_resize_new_updated1.png)

   點選元件後顯示的工具列包含下列選項：

   * **[!UICONTROL 父系]**：選取元件的父系。
   * **[!UICONTROL 回覆中斷點配置]**：復原所有調整大小的變更，並將預設配置套用至元件。
   * **[!UICONTROL 浮動到新行]**：如果同一行中有多個元件，請將元件移至下一行。

   您也可以在面板層級使用&#x200B;**[!UICONTROL 回覆中斷點配置]** （![回覆中斷點](assets/reverttopreviouslypublishedversion.png)）選項，以復原所有調整大小的變更。

   >[!NOTE]
   >
   >您無法使用「版面」模式調整表格欄、工具列、工具列按鈕和目標區域元件的大小。 使用「樣式」模式調整這些元件的大小。

### 範例 {#example}

**目標：**&#x200B;您想要插入表格元件和影像元件，並以最適化表單將它們彼此平行放置。

1. 在最適化表單中使用編輯模式插入表格和影像元件。 影像元件會顯示在表格元件之後。
1. 切換到佈局模式並選取表格元件。 要調整元件大小的藍點會顯示在欄1和12。
1. 將第12欄的藍色圓點拖放至回應式格線的第6欄。

   ![定義資料表的端點](assets/layout_mode_end_point_table_new.png)

1. 同樣地，選取影像元件，並將回應式格線第1欄的藍色圓點拖放至第7欄。 表格和影像元件彼此平行顯示。

   ![在版面配置模式中同時顯示表格和影像](assets/table_image_parallel_new.png)

   您可以選取影像元件，並選取工具列中可用的&#x200B;**浮動至新行**&#x200B;選項，以將影像元件移至下一行。

## 調整面板大小 {#resize-panels-layout-mode}

如果您想要調整整個面板而非個別元件的大小，請執行下列步驟：

1. 選取面板中您要調整大小的任何元件，選取![選取父項](assets/select_parent_icon.svg)，然後選取下拉式清單中的第一個選項（如果面板是元件的直接父項）。

   藍點會顯示在回應式格線的開始和結尾。

1. 拖放藍點以定義面板在回應式格線中的位置。
您可以重複步驟1和2，並選取![選取父項](assets/float_to_new_line_icon.svg)，將調整大小的面板移至下一行。

## 定義面板的多欄配置

執行以下步驟來定義面板的欄數：

1. 在&#x200B;**[!UICONTROL 編輯]**&#x200B;模式中，選取面板，選取![設定](assets/configure_icon.png)，然後從&#x200B;**[!UICONTROL 面板配置]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 回應式 — 頁面上所有不含導覽的]**&#x200B;選項。

1. 選取![儲存](assets/save_icon.svg)以儲存屬性。

1. 在&#x200B;**[!UICONTROL 配置]**&#x200B;模式中，選取面板中的任何元件，選取![選取父項](assets/select_parent_icon.svg)，然後選取面板。

1. 選取![多欄](assets/multi-column.svg)，並從下拉式清單中選取欄數。 欄數可以介於1到12之間。 面板會分成多欄配置。

![配置模式中的多欄](assets/multi-column-layout.png)

## 為舊的回應式版面配置啟用新的回應式格線 {#enableresponsivegrid}

為您使用AEM Forms 6.4或更低版本建立的表單啟用新的回應式格線，以調整元件大小。

>[!NOTE]
>
>切換至新的回應式格線會捨棄已為表單中使用的元件定義的版面配置屬性。

執行以下步驟以啟用新的回應式格線：

1. 從位於&#x200B;**預覽**&#x200B;選項旁上方的下拉式清單中選取&#x200B;**配置**。 隨即顯示啟用配置模式的確認訊息。
1. 選取&#x200B;**是**&#x200B;以啟用表單的&#x200B;**配置**&#x200B;模式。

### 以新回應式佈局將舊片段嵌入最適化表單中 {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

最適化表單的全新回應式佈局可讓您新增具有舊回應式佈局的最適化表單片段至表單。 不過，新版面會捨棄已針對片段中使用之元件定義的版面屬性。 您可以切換到佈局模式以定義片段中使用的元件的佈局屬性。

### 在舊的最適化表單中嵌入具有新回應式佈局的片段 {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

如果您使用舊回應式佈局在自適應表單中嵌入帶有新回應式佈局的片段，系統會提示您啟用表單的佈局模式並重新嵌入片段。

若要啟用[配置]模式，請從位於&#x200B;**預覽**&#x200B;選項旁上方的下拉式清單中選取&#x200B;**配置**，並選取&#x200B;**是**&#x200B;進行確認。 選取&#x200B;**編輯**&#x200B;模式以重新嵌入片段。

## 停用具有舊回應式佈局的表單的佈局模式 {#disable-layout-mode-for-forms-with-old-responsive-layout}

您可以編輯表單中所用範本的屬性，以停用具有舊回應式版面的表單版面模式。

執行以下步驟以停用「配置」模式：

1. 選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 範本]**，並以&#x200B;**[!UICONTROL 編輯]**&#x200B;模式開啟表單中使用的範本。
1. 在左窗格中選取[檔案容器]，然後選取[**[!UICONTROL 原則]。]**

   ![停用配置模式](assets/policy_disable_layout_mode.png)

1. 選取&#x200B;**[!UICONTROL 配置設定]**&#x200B;索引標籤，並選取&#x200B;**[!UICONTROL 停用配置模式]**。
1. 選取![儲存變更](assets/save_icon.png)以儲存範本屬性。
