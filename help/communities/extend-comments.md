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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 擴充注釋元件 {#extend-comments-component}

擴展缺 [省元件](client-customize.md#extensions) (Extending a default component)的意圖是改變元件的外觀或行為以用於特定用途。

元件的路徑是唯一的，並將預設元件作為超級資源類型引用。 與元件覆蓋的全域範圍相比，範圍有限，因此風險較低。

>[!NOTE]
>
>不支 [持延伸](client-customize.md#overlays) 覆蓋元件。

## 例如 {#example}

假設注釋元件的標題必須在AEM例項的某個網站上顯示替代外觀，而在另一個網站上顯示預設顯示。 與其覆蓋預設注釋（這會變更所有例項的注釋元件），更好的解決方案是確保有多個注釋元件可供各網站使用。

若要實作此解決方案，請建立可延伸（覆寫）現有元件並修改Handlebars指令碼的新元件。 使用新注釋的網站區域可以使用擴充的注釋，而使用預設外觀的網站則不受影響。

注釋元件實際上是構成注釋系統的兩個元件之一。 因此，需要擴展兩個元件：留 *言**和留言*。 要編輯的指令碼位於*comment * `header.hbs` component的檔案中，而父 *comments* component（注釋系統）則是作者實際新增至頁面的內容。

若要延伸意見，您必須：

1. [建立元件](extend-create-components.md)
1. [新增註解至範例頁面](extend-sample-page.md)
1. [改變外觀](extend-alter-appearance.md)

