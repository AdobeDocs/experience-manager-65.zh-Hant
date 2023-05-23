---
title: 透過延遲載入改善大型表單的效能
seo-title: Improve performance of large forms with lazy loading
description: 延遲載入通過延遲形式片段的初始化和載入直到它們可見，顯著改善了大型和複雜自適應形式的效能。
seo-description: Lazy loading significantly improves the performance of large and complex adaptive forms by deferring initialization and loading of form fragments until they are visible.
uuid: 6be3d2f0-1b2a-4090-af66-2b08487c31bc
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: a20736b7-f7b4-4da1-aa32-2408049b1209
docset: aem65
feature: Adaptive Forms
exl-id: f7e3e2cd-0cbe-4b26-9e55-7afc6dc3af63
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 1%

---

# 透過延遲載入改善大型表單的效能{#improve-performance-of-large-forms-with-lazy-loading}

## 懶散載入簡介 {#introduction-to-lazy-loading}

當表單在成百上千個欄位中變得龐大而複雜時，最終用戶在運行時呈現表單時會經歷較長的響應時間。 為了將響應時間減到最小，自適應表單允許您將表單分解為邏輯片段，並配置以延遲片段的初始化或載入，直到片段需要可見。 這被稱為懶散載入。 此外，一旦用戶導航到窗體中的其它部分，並且碎片不再可見，則卸載配置用於緩慢載入的碎片。

在配置懶散載入之前，我們先瞭解要求和準備步驟。

## 準備配置延遲載入 {#preparing-to-configure-lazy-loading}

在以自適應形式配置片段的延遲載入之前，必須定義策略以建立片段、標識指令碼中使用的值或其他片段中引用的值，以及定義規則以控制延遲載入片段中欄位的可見性。

* **標識和建立片段**
您只能配置適應的表單片段，以便緩慢載入。 片段是駐留在自適應窗體外並可跨窗體重複使用的獨立段。 因此，實現緩慢載入的第一步是識別形式的邏輯部分並將其轉換為片段。 您可以從頭建立片段或將現有窗體面板另存為片段。

   有關建立片段的詳細資訊，請參見 [自適應形式片段](../../forms/using/adaptive-form-fragments.md)。

* **標識和標籤全局值**
基於Forms的交易涉及動態元素以從用戶處獲取相關資料並處理這些資料，以簡化填表體驗。 例如，表單的片段X中有欄位A，其值決定了另一個片段中欄位B的有效性。 在這種情況下，如果將片段X標籤為延遲載入，則即使未載入片段X，欄位A的值也必須可用於驗證欄位B。 要達到此目的，可以將欄位A標籤為全局欄位，這可確保在未載入片段X時，其值可用於驗證欄位B。

   有關如何使欄位值全局化的資訊，請參見 [配置延遲載入](../../forms/using/lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p)。

* **寫入規則以控制欄位的可見性**
Forms包含一些不適用於所有用戶和所有條件的欄位和部分。 Forms的作者和開發者使用可見性或show-hide規則根據用戶輸入來控制他們的可見性。 例如，「辦公地址」欄位不會顯示給在表單中「就業狀態」欄位中選擇「失業」的用戶。 有關編寫規則的詳細資訊，請參見 [使用規則編輯器](../../forms/using/rule-editor.md)。

   您可以利用延遲載入的片段中的可見性規則，以便僅在需要條件欄位時才顯示條件欄位。 此外，將條件欄位標籤為全局，以在延遲載入的片段的可見性表達式中引用它。

## 配置延遲載入 {#configuring-lazy-loading}

執行以下步驟以啟用自適應表單片段上的延遲載入：

1. 在創作模式下開啟自適應窗體，該窗體包含要啟用的片段，以便進行緩慢載入。
1. 選擇自適應表單片段並點擊 ![招商](assets/cmppr.png)。
1. 在提要欄中，啟用 **[!UICONTROL 懶散載入碎片]** 點擊 **完成**。

   ![為自適應表單片段啟用延遲載入](assets/lazy-loading-fragment.png)

   現在，已啟用片段以進行緩慢載入。

您可以將延遲載入的片段中對象的值標籤為全局值，以便在未載入包含的片段時，這些值可用於指令碼中。 請執行下列動作：

1. 在創作模式下開啟自適應表單片段。
1. 按一下要將其值標籤為全局的欄位，然後按一下 ![招商](assets/cmppr.png)。
1. 在提要欄中，啟用 **延遲載入期間使用值**。

   ![邊欄中的延遲載入欄位](assets/enable-lazy-loading.png)

   該值現在被標籤為全局值，即使在卸載包含的片段時也可用於指令碼中。

## 配置懶散載入的注意事項和最佳做法 {#considerations-and-best-practices-for-configuring-lazy-loading}

在處理懶散載入時，需要注意的一些限制、建議和要點如下：

* 建議在基於XFA的自適應表單上使用基於XSD架構的自適應表單，以在大型表單上配置延遲載入。 在基於XFA的自適應形式中由於延遲載入實現而產生的效能增益相對小於在基於XSD的自適應形式中的增益。
* 不要在使用的自適應格式中配置片段的延遲載入 **[!UICONTROL 響應 — 無需導航即可在一頁上完成所有任務]** 根面板的佈局。 作為響應佈局配置的結果，所有片段以自適應形式同時載入。 它還會導致效能下降。
* 建議不要以自適應形式在第一段上配置延遲載入。
* 建議不要在載入自適應表單時呈現的第一個面板中的片段上配置延遲載入。
* 在片段層次中，最多支援兩個級別的延遲載入。
* 確保標籤為全局的欄位在自適應表單中是唯一的。
* 考慮根據條件為應顯示或隱藏的片段編寫可見性規則。 例如，您可以根據用戶指定的婚姻狀態顯示或隱藏「配偶詳細資訊」片段。
* 延遲載入的片段不支援檔案附件和條款和條件元件。

### 編寫配置延遲載入的最佳實踐指令碼 {#scripting-best-practices-for-configuring-lazy-loading}

在開發懶散載入面板的指令碼時，要注意的要點如下：

* 確保初始化和計算在懶散載入片段的欄位上使用的指令碼本質上是冪等的。 冪等指令碼是那些即使在多次執行後也具有相同效果的指令碼。
* 使用欄位的全局可用屬性使位於延遲載入面板中的欄位值可用於表單的所有其他面板。
* 不要轉發懶散面板內欄位的引用值，而不管是否在分段中全局標籤欄位。
* 使用面板重置功能，使用以下按一下表達式重置面板上所有可見的內容。\
   guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;):&quot;navigablePanel&quot;})。resetData()
