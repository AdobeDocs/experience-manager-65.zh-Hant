---
title: 擴充注釋元件
seo-title: 擴充注釋元件
description: 延伸「注釋」元件，以變更其外觀或行為以供特定用途使用
seo-description: 延伸「注釋」元件，以變更其外觀或行為以供特定用途使用
uuid: 6f439097-b1d0-4e7d-afcf-01d8f43aa866
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a07a4690-0e47-4a76-84cb-96abdc70b835
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# 擴展注釋元件{#extend-comments-component}

[extending](client-customize.md#extensions)預設元件的用意是改變元件的外觀或行為以用於特定用途。

元件的路徑是唯一的，並將預設元件作為超級資源類型引用。 與元件覆蓋的全域範圍相比，範圍有限，因此風險較低。

>[!NOTE]
>
>不支援延伸[覆蓋](client-customize.md#overlays)元件。

## 範例 {#example}

假設注釋元件的標題必須在AEM例項的某個網站上顯示替代外觀，而在另一個網站上顯示預設顯示。 與其覆蓋預設注釋（這會變更所有例項的注釋元件），更好的解決方案是確保有多個注釋元件可供各網站使用。

若要實作此解決方案，請建立可延伸（覆寫）現有元件並修改Handlebars指令碼的新元件。 使用新注釋的網站區域可以使用擴充的注釋，而使用預設外觀的網站則不受影響。

注釋元件實際上是構成注釋系統的兩個元件之一。 因此，需要擴展兩個元件：*comments*&#x200B;和&#x200B;*comment*。 要編輯的指令碼位於&#x200B;*comment*&#x200B;元件的`header.hbs`檔案中，而父&#x200B;*comments*&#x200B;元件（注釋系統）是作者實際添加到頁面的內容。

若要延伸意見，您必須：

1. [建立元件](extend-create-components.md)
1. [新增註解至範例頁面](extend-sample-page.md)
1. [改變外觀](extend-alter-appearance.md)

