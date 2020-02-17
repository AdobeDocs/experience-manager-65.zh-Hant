---
title: 設定表單的基本資訊
seo-title: 設定表單的基本資訊
description: 瞭解各種表單服務，協助您建立互動式資料擷取應用程式。
seo-description: 瞭解各種表單服務，協助您建立互動式資料擷取應用程式。
uuid: f495c170-2d17-45b0-b09d-22cce101131e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e87c7379-28ed-4fda-aef1-970d2b54f30d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定表單的基本資訊 {#basics-of-configuring-forms}

Forms服務可讓您建立互動式資料擷取用戶端應用程式，以驗證、處理、轉換和傳送通常在設計人員中建立的表單。 表單製作者會開發單一表單設計，Forms服務會以各種格式呈現：

* 在Adobe reader或瀏覽器中以PDF格式顯示
* 在各種瀏覽器環境（包括相容的XHTML 1.0轉換）中以HTML格式顯示
* 在支援Adobe Flash player的各種瀏覽器環境中當做表單指南。

如需Forms服務的詳細資訊，請參閱服 [務參考](https://www.adobe.com/go/learn_aemforms_services_63)。

使用管理控制台中的「表單」頁面，您可以設定Forms服務的行為。 這些設定適用於服務的所有調用。 任何透過AEM表單SDK傳送的參數都會覆寫管理控制台中設定的設定；但是，它們只影響到這一特定的援引。

變更管理控制台中的「表單」設定後，按一下「儲存」。 您不需要重新啟動伺服器，更改才會生效。 不過，在設定快取模式設定時，您可能需要停止並重新啟動Forms服務。 (請參 [閱啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)。)
