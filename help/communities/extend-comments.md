---
title: 擴充註解元件
description: 擴充Comments元件以改變其外觀或特定用途的行為
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 擴充註解元件  {#extend-comments-component}

意圖 [延伸](client-customize.md#extensions) 預設元件是針對特定用途變更元件的外觀或行為。

元件的路徑是唯一的，且會參照預設元件作為超級資源型別。 與元件覆蓋的整個範圍相比，範圍是有限的，因此風險較低。

>[!NOTE]
>
>擴充 [重疊](client-customize.md#overlays) 元件不受支援。

## 範例 {#example}

假設註解元件的標頭必須以替代外觀顯示在AEM例證的一個網站上，而以預設顯示出現在另一個網站上。 取代覆蓋預設註解（會變更所有執行個體的註解元件）的更好的解決方案是確保有多個註解元件可用於各種網站。

若要實作此解決方案，請建立擴充（覆寫）現有元件的元件，並修改Handlebars指令碼。 使用新註解的網站區域可使用延伸區域，而使用預設外觀的網站則不受影響。

註解元件實際上是構成註解系統的兩個元件之一。 因此，有兩個元件需要擴充： *評論* 和 *評論*. 要編輯的指令碼位於 *評論* 元件的 `header.hbs` 檔案，而父系 *評論* 元件（註解系統）是作者實際新增至頁面的專案。

若要擴充註解，您必須：

1. [建立元件](extend-create-components.md)
1. [新增註解至範例頁面](extend-sample-page.md)
1. [變更外觀](extend-alter-appearance.md)
