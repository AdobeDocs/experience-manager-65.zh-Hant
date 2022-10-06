---
title: 透過延遲載入改善大型表單的效能
seo-title: Improve performance of large forms with lazy loading
description: 延遲載入會延遲表單片段的初始化和載入，直到顯示為止，大幅改善大型且複雜的最適化表單的效能。
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

## 延遲載入簡介 {#introduction-to-lazy-loading}

當表單變得龐大而複雜，包含數百個和數千個欄位時，使用者在執行階段轉譯表單時會遇到很長的回應時間。 為了將回應時間減到最少，適用性表單可讓您將表單分割為邏輯片段，並設定將片段的初始化或載入延遲到需要顯示片段為止。 這稱為延遲載入。 此外，當使用者導覽至表單中的其他區段，且片段不再顯示時，就會取消載入為延遲載入所設定的片段。

先了解需求和準備步驟，再設定延遲載入。

## 準備配置延遲載入 {#preparing-to-configure-lazy-loading}

在您設定最適化表單中片段的延遲載入前，請務必定義策略以建立片段、識別指令碼中使用或其他片段中參考的值，以及定義規則以控制延遲載入片段中欄位的可見性。

* **識別和建立片段**
您只能為延遲載入設定最適化表單片段。 片段是獨立的區段，駐留在最適化表單之外，並可跨表單重複使用。 因此，實作延遲載入的第一步，是識別表單中的邏輯區段，並將其轉換為片段。 您可以從草稿建立片段，或將現有表單面板儲存為片段。

   如需建立片段的詳細資訊，請參閱 [最適化表單片段](../../forms/using/adaptive-form-fragments.md).

* **識別和標籤全域值**
Forms型交易包含動態元素，可從使用者擷取相關資料，並加以處理以簡化表單填寫體驗。 例如，您的表單在片段X中有欄位A，其值決定了另一個片段中欄位B的有效性。 在此情況下，如果片段X標示為延遲載入，則欄位A的值必須可用於驗證欄位B，即使片段X未載入亦然。 要實現此目的，您可以將欄位A標示為全域，以確保其值可在片段X未載入時用於驗證欄位B。

   如需如何讓欄位值變成全域的相關資訊，請參閱 [配置延遲載入](../../forms/using/lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p).

* **編寫規則以控制欄位的可見性**
Forms包含某些欄位和區段，這些欄位和區段不適用於所有使用者和所有條件。 Forms作者和開發人員使用可見性或顯示隱藏規則，根據使用者輸入控制其可見性。 例如，在表單的「就業狀態」欄位中選擇「失業」的用戶不會顯示「辦公室地址」欄位。 如需撰寫規則的詳細資訊，請參閱 [使用規則編輯器](../../forms/using/rule-editor.md).

   您可以在懶惰載入的片段中運用可見性規則，讓條件欄位只在需要時才顯示。 此外，將條件欄位標示為全域，以便在延遲載入片段的可見性運算式中參照它。

## 配置延遲載入 {#configuring-lazy-loading}

執行下列步驟以在最適化表單片段上啟用延遲載入：

1. 以製作模式開啟最適化表單，其中包含您要啟用以延遲載入的片段。
1. 選取最適化表單片段並點選 ![cppr](assets/cmppr.png).
1. 在側欄中，啟用 **[!UICONTROL 懶惰載入片段]** 點選 **完成**.

   ![為最適化表單片段啟用延遲載入](assets/lazy-loading-fragment.png)

   片段現在已啟用為延遲載入。

您可以將延遲載入片段中物件的值標示為全域，以便在未載入包含片段時，這些值可用於指令碼中。 請執行下列動作：

1. 在製作模式中開啟最適化表單片段。
1. 點選您要將其值標示為全域的欄位，然後點選 ![cppr](assets/cmppr.png).
1. 在側欄中，啟用 **在延遲載入期間使用值**.

   ![側欄中的延遲載入欄位](assets/enable-lazy-loading.png)

   該值現在已標示為全域，且即使載入片段已卸載，亦可在指令碼中使用。

## 配置延遲載入的考量事項和最佳實務 {#considerations-and-best-practices-for-configuring-lazy-loading}

處理延遲載入時應留意的一些限制、建議和重要點如下：

* 建議您使用XSD結構式適用性表單，而非XFA型適用性表單，以設定大型表單上的延遲載入。 XFA型適用性表單中延遲載入實作所帶來的效能增益，相對而言小於XSD型適用性表單中的增益。
* 請勿在使用的最適化表單中設定片段延遲載入 **[!UICONTROL 回應 — 不進行導覽的單一頁面上的所有內容]** 根面板的版面配置。 回應式版面配置的結果，所有片段會以最適化表單同時載入。 這也會導致效能降低。
* 建議不要在最適化表單的第一個片段上設定延遲載入。
* 建議不要在第一個面板中針對呈現載入最適化表單的片段設定延遲載入。
* 片段階層最多支援兩個層級的延遲載入。
* 確保在最適化表單中，標示為全域的欄位是唯一的。
* 請考慮針對應根據條件顯示或隱藏的片段撰寫可見性規則。 例如，您可以根據使用者指定的婚姻狀態來顯示或隱藏「配偶詳細資訊」片段。
* 懶惰載入片段不支援檔案附件和條款與條件元件。

### 為配置延遲載入編寫指令碼的最佳做法 {#scripting-best-practices-for-configuring-lazy-loading}

為延遲載入面板開發指令碼時請謹記的重要事項如下：

* 請確定在延遲載入片段的欄位上使用的初始化和計算指令碼在本質上為等冪。 等冪指令碼即使執行多次，也會有相同效果。
* 使用欄位的全域可用屬性，讓位於延遲載入面板中的欄位值可供表單的所有其他面板使用。
* 無論欄位是否跨片段全域標示，請勿轉送延遲面板內欄位的參考值。
* 使用面板重設功能，透過下列點擊運算式重設面板上可見的所有內容。\
   guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;:&quot;navigablePanel&quot;})。resetData()
