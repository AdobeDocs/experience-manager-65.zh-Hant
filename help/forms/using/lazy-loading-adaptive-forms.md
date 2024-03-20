---
title: 透過延遲載入改善大型表單的效能
description: 延遲載入會透過延遲表單片段的初始化和載入直到片段顯示為止，大幅改善大型和複雜調適型表單的效能。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: f7e3e2cd-0cbe-4b26-9e55-7afc6dc3af63
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 7%

---

# 透過延遲載入改善大型表單的效能{#improve-performance-of-large-forms-with-lazy-loading}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/lazy-loading-adaptive-forms.html) |
| AEM 6.5 | 本文章 |

## 延遲載入簡介 {#introduction-to-lazy-loading}

當表單變得龐大而複雜，並包含數百個及數千個欄位時，一般使用者在執行階段轉譯表單時會經歷漫長的回應時間。 為了將回應時間縮到最短，調適型表單可讓您將表單分成邏輯片段，並設定為延遲初始化或載入片段，直到需要看到片段為止。 這稱為延遲載入。 此外，一旦使用者導覽到表單中的其他區段並且片段不再可見，則會解除安裝為延遲載入設定的片段。

在設定延遲載入之前，請先瞭解需求和準備步驟。

## 正在準備設定延遲載入 {#preparing-to-configure-lazy-loading}

在配置最適化表單中的片段延遲載入之前，請務必定義策略以建立片段、識別指令碼中使用或用於其他片段中的值，以及定義規則以控制延遲載入片段中欄位的可見度。

* **識別並建立片段**
您只能為延遲載入設定最適化表單片段。 片段是位於最適化表單之外的獨立區段，可跨表單重複使用。 因此，實施延遲載入的第一步是識別表單中的邏輯區段，並將其轉換為片段。 您可以從頭開始建立片段，或將現有的表單面板儲存為片段。

  如需建立片段的詳細資訊，請參閱 [最適化表單片段](../../forms/using/adaptive-form-fragments.md).

* **識別並標籤全域值**
Forms型交易涉及動態元素，可從使用者擷取相關資料並進行處理，以簡化表單填寫體驗。 例如，您的表單在片段X中有欄位A，其值決定了另一個片段中欄位B的有效性。 在此案例中，如果片段X標示為延遲載入，則欄位A的值必須可用於驗證欄位B，即使未載入片段X。 為此，您可以將欄位A標示為全域，以確保其值可在未載入片段X時用於驗證欄位B。

  如需有關如何將欄位值設為全域值的資訊，請參閱 [設定延遲載入](../../forms/using/lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p).

* **撰寫規則以控制欄位的可見度**
Forms包含某些欄位和區段，不適用於所有使用者和所有條件。 Forms作者和開發人員可使用可見度或顯示隱藏規則，根據使用者輸入控制其可見度。 例如，在表單的「就業狀態」欄位中選擇「失業」的使用者不會看到「辦公室地址」欄位。 如需撰寫規則的詳細資訊，請參閱 [使用規則編輯器](../../forms/using/rule-editor.md).

  您可以在緩慢載入的片段中使用可見性規則，讓條件欄位只在需要時顯示。 此外，將條件欄位標示為全域，以在延遲載入片段的可見度運算式中參照它。

## 設定延遲載入 {#configuring-lazy-loading}

執行以下步驟，啟用最適化表單片段的延遲載入：

1. 以製作模式開啟最適化表單，其中包含您要啟用以延遲載入的片段。
1. 選取最適化表單片段，然後選取 ![cmppr](assets/cmppr.png).
1. 在側邊欄中，啟用 **[!UICONTROL 緩慢地載入片段]** 並選取 **完成**.

   ![啟用最適化表單片段的延遲載入](assets/lazy-loading-fragment.png)

   片段現在可啟用延遲載入。

您可以將延遲載入片段中物件的值標示為全域，以便在未載入包含片段時可以在指令碼中使用。 請執行下列動作：

1. 在製作模式中開啟最適化表單片段。
1. 選取您要將其值標示為全域值的欄位，然後選取 ![cmppr](assets/cmppr.png).
1. 在側邊欄中，啟用 **在緩慢載入時使用值**.

   ![側欄中的延遲載入欄位](assets/enable-lazy-loading.png)

   此值現在標籤為全域，並且即使在包含片段解除安裝時也可用於指令碼。

## 設定延遲載入的考量事項和最佳作法 {#considerations-and-best-practices-for-configuring-lazy-loading}

處理延遲載入時應留意的一些限制、建議和重要事項如下：

* 在XFA型調適型表單上使用XSD結構描述型調適型表單，以設定大型表單上的延遲載入。 由於XFA型調適型表單中延遲載入實作造成的效能增益，相對而言小於XSD型調適型表單中的增益。
* 請勿在使用的最適化表單中設定片段延遲載入 **[!UICONTROL 回應式 — 全部於單頁無需導覽]** 根面板的配置。 作為回應式佈局設定的結果，所有片段都會以自適應表單同時載入。 這也會導致效能降低。
* 建議不要在最適化表單的第一個片段上設定延遲載入。
* 建議不要在載入最適化表單時轉譯的第一個面板中設定片段延遲載入。
* 片段階層中最多支援兩個層級的延遲載入。
* 確保在最適化表單中標示為全域的欄位是唯一的。
* 請考慮為應根據條件顯示或隱藏的片段寫入可見性規則。 例如，您可以根據使用者指定的婚姻狀況顯示或隱藏「配偶詳細資訊」片段。
* 延遲載入的片段不支援檔案附件和條款與條件元件。

### 設定延遲載入的指令碼最佳作法 {#scripting-best-practices-for-configuring-lazy-loading}

開發用於延遲載入面板的指令碼時，請謹記以下重要事項：

* 確保用於延遲載入片段欄位上的初始化和計算指令碼本質上為等冪。 等冪指令碼是指即使在多個執行後具有相同效果的指令碼。
* 使用欄位全域可用的屬性，讓延遲載入面板中的欄位值可供表單的所有其他面板使用。
* 無論欄位是否跨片段標示為全域，請勿轉寄延遲面板內欄位的參考值。
* 使用面板重設功能，透過下列按一下運算式重設面板上的所有可見專案。\
  guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;： &quot;navigablePanel&quot;}))。resetData()
