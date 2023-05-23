---
title: 配置表單的基本資訊
seo-title: Basics of configuring forms
description: 瞭解幫助您建立互動式資料捕獲應用程式的各種表單服務。
seo-description: Learn about the various forms services that help you create interactive data capture applications.
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 配置表單的基本資訊 {#basics-of-configuring-forms}

Forms服務使您能夠建立互動式資料捕獲客戶端應用程式，這些應用程式驗證、處理、轉換和傳遞通常在設計器中建立的表單。 表格作者開發一種Forms服務以各種格式呈現的單一表格設計：

* 作為PDF在Adobe Reader或瀏覽器
* HTML，包括相容的XHTML 1.0呈現
* 在支援AdobeFlash Player的各種瀏覽器環境中作為表單指南。

有關Forms服務的其他資訊，請參見 [服務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

使用管理控制台中的Forms頁，可以配置Forms服務的行為。 這些設定適用於服務的所有調用。 通過表單SDK發送AEM的任何參數都會覆蓋管理控制台中設定的設定；但是，它們只影響該特定調用。

在管理控制台中更改Forms設定後，按一下「保存」。 您不需要重新啟動伺服器，更改才能生效。 但是，在配置快取模式設定時，可能需要停止並重新啟動Forms服務。 (請參閱 [啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)。)
