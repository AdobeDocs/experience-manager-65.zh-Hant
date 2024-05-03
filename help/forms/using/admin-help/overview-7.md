---
title: 設定表單的基本概念
description: 瞭解各種可幫助您建立互動式資料擷取應用程式的表單服務。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 設定表單的基本概念 {#basics-of-configuring-forms}

Forms服務可讓您建立互動式資料擷取使用者端應用程式，以驗證、處理、轉換及傳遞通常在Designer中建立的表單。 表單作者會開發單一表單設計，Forms服務會以各種格式呈現：

* 作為Adobe Reader或瀏覽器中的PDF
* 做為各種瀏覽器環境中的HTML，包括相容的XHTML 1.0轉譯
* 在支援AdobeFlash Player的各種瀏覽器環境中作為表單指南。

如需Forms服務的詳細資訊，請參閱 [服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

使用Administration Console中的Forms頁面，您可以設定Forms服務的行為。 這些設定會套用至服務的所有呼叫。 任何透過AEM Forms SDK傳送的引數都會覆寫在管理控制檯中設定的設定；但是，這些引數只會影響該特定引動。

在管理主控台中變更Forms設定後，按一下儲存。 您不需要重新啟動伺服器即可讓變更生效。 不過，在設定快取模式設定時，您可能需要停止並重新啟動Forms服務。 (請參閱 [啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
