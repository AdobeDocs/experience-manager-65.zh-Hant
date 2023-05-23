---
title: 擴展注釋元件
seo-title: Extend Comments Component
description: 擴展「注釋」元件以更改其外觀或行為以用於特定用途
seo-description: Extend the Comments component to alter its appearance or behavior for specific uses
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
exl-id: e57198cb-8fd9-43e2-b416-e40e462561c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# 擴展注釋元件  {#extend-comments-component}

意圖 [延伸](client-customize.md#extensions) 預設元件用於改變特定用途的元件的外觀或行為。

該元件的路徑是唯一的，並將預設元件作為超級資源類型引用。 與元件覆蓋的全局範圍相比，該範圍有限，因此風險較小。

>[!NOTE]
>
>擴展 [覆蓋](client-customize.md#overlays) 不支援元件。

## 範例 {#example}

假設注釋元件的標題必須在實例的一個站點上以替代外觀顯示AEM，而在另一個站點上以預設顯示顯示。 與其覆蓋預設注釋（更改所有實例的注釋元件），更好的解決方案是確保有多個注釋元件可供在不同站點上使用。

要實現此解決方案，請建立一個新元件，該元件將擴展（覆蓋）現有元件並修改Handlebars指令碼。 使用新注釋的站點區域可以使用擴展注釋，而使用預設外觀的站點不受影響。

注釋元件實際上是構成注釋系統的兩個元件之一。 因此，有兩個要擴展的元件： *評論* 和 *注釋*。 要編輯的指令碼位於 *注釋* 元件 `header.hbs` 檔案，而父級 *評論* 元件（注釋系統）是作者實際添加到頁面的內容。

要擴展注釋，您需要：

1. [建立元件](extend-create-components.md)
1. [將注釋添加到示例頁](extend-sample-page.md)
1. [更改外觀](extend-alter-appearance.md)
