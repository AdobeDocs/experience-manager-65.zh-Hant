---
title: 編輯頁面時的註解
seo-title: Annotations when Editing a Page
description: 將內容新增至網站的頁面通常要經過實際發佈前的討論。 為此，許多與內容直接相關的元件允許您添加註釋。
seo-description: Adding content to the pages of your website is often subject to discussions prior to it actually being published. To aid this, many components directly related to content allow you to add an annotation.
page-status-flag: de-activated
uuid: d8d6ba76-f2aa-4044-98bf-5d506742d90d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9bee0197-f275-49cc-922d-62cba826c4e5
exl-id: d60e9601-d15b-4378-a33e-e90961f63195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# 編輯頁面時的註解{#annotations-when-editing-a-page}

將內容新增至網站的頁面通常要經過實際發佈前的討論。 為此，許多與內容直接相關的元件（例如，與版面相對）允許您添加註釋。

附註會在頁面上放置一個彩色標籤/便箋。 註解可讓您（或其他使用者）為其他作者/審核者留下意見和/或問題。

>[!NOTE]
>
>單個元件類型的定義確定是否可在該元件的實例上添加註釋。

>[!NOTE]
>
>傳統UI中建立的註解也會顯示在觸控最佳化UI中。 不過，草繪是UI專用的，只顯示在建立它們的UI中。

>[!CAUTION]
>
>刪除資源（例如，段落）會刪除附加到該資源的所有注釋和草圖；無論其在整個頁面上的位置。

>[!NOTE]
>
>您也可以根據您的需求開發工作流程，以在新增、更新或刪除註解時傳送通知。

## 註解 {#annotations}

根據段落設計，注釋可作為上下文菜單上的選項（通常是在所需段落上滑鼠右鍵）或作為段落編輯欄上的按鈕使用。

無論是哪種情況，請選擇 **注釋**. 將對段落應用彩色註解，您將立即處於「編輯」模式，允許您直接添加文本：

![chlimage_1-137](assets/chlimage_1-137.png)

您可以將註解移動到頁面上的新位置。 按一下頂部邊框區域，然後按住並同時將注釋拖動到新位置。 這可以在頁面上的任何位置，但以某種方式將其連接到段落通常都是有意義的。

注釋（包括相關草圖）也包含在附加在段落上執行的任何複製、剪切或刪除操作中；對於複製或剪切操作，注釋（和相關草繪）的位置將保留其與原始段落的位置。

通過拖動右下角，也可以增加或減小注釋的大小。

為了追蹤目的，頁尾行會指出建立附註和日期的使用者。 後續作者可以編輯相同的注釋（將更新頁尾），或為相同段落建立新注釋。

當您選擇刪除注釋時，將請求確認（刪除注釋也會刪除附加到該注釋的所有草繪）。

左上角的三個表徵圖允許您最小化注釋（連同任何相關草繪）、更改顏色並添加草繪。

>[!NOTE]
>
>註解只會顯示在製作環境的「編輯」模式中。
>
>它們不會顯示在發佈環境中，也不會顯示在製作環境中可用的預覽或設計模式中。

>[!NOTE]
>
>註解無法添加到已被其他用戶鎖定的頁面。

## 注釋草繪 {#annotation-sketches}

>[!NOTE]
>
>草圖在Internet Explorer中不可用，因此：
>
>* 將不會顯示圖示。
>* 將不顯示在其他瀏覽器中建立的現有草繪。
>


草繪是注釋的一種特徵，允許您在瀏覽器窗口（可見部分）上的任意位置建立簡單的線圖形：

![chlimage_1-138](assets/chlimage_1-138.png)

* 當處於草繪模式時，游標將更改為交叉線。 可以繪製多條不同的線。
* 草繪線反映注釋顏色，可以是：

   * 凍手

      預設模式；完成時釋放滑鼠按鈕。

   * 直線：

      按住 `ALT` 按一下起點和終點；按兩下即可完成。

* 退出草繪方式後，可以按一下草繪線以選取該草繪。
* 通過選取草繪，然後將其拖動到所需位置來移動草繪。
* 草圖會覆蓋內容。 這表示在草繪的4個角內，不能按一下基礎段落；例如，如果您需要編輯或存取連結。 如果這成為問題（例如，您有一個草圖覆蓋了頁面的很大區域），則將適當的注釋最小化，因為這也會使所有相關草圖最小化，從而允許您訪問基礎區域。
* 要刪除單個草繪 — 選取所需草繪，然後按 **刪除** 鍵(**fn**-**空格** 在MAC上)。

* 如果移動或複製段落，則任何相關注釋及其草繪也將移動或複製；他們對該款的立場將保持不變。
* 如果刪除注釋，則附加到該注釋的所有草繪也將被刪除。
