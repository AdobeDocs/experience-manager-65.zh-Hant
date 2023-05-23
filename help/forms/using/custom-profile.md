---
title: 為HTML5窗體建立自定義配置檔案
seo-title: Creating a custom profile for HTML5 forms
description: HTML5表單配置檔案是Apache Sling中的資源節點。 它表示HTML5表單呈現服務的自定義版本。
seo-description: A HTML5 forms profile is a resource node in Apache Sling. It represents a customized version of HTML5 forms Render service.
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: Mobile Forms
exl-id: cf86c810-c466-4894-acc2-d4faf49754cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# 為HTML5窗體建立自定義配置檔案 {#creating-a-custom-profile-for-html-forms}

配置檔案是中的資源節點 [阿帕奇斯林](https://sling.apache.org/)。 它表示HTML5表單格式副本服務的自定義版本。 您可以使用HTML5表單格式副本服務來自定義HTML5表單的外觀、行為和交互。 配置檔案節點存在於 `/content` 資料夾。 可以將節點直接放在 `/content` 資料夾或其任何子資料夾 `/content` 的子菜單。

配置檔案節點具有 **sling:resourceSuperType** 屬性，預設值為 **xfaforms/profile**。 節點的呈現指令碼位於/libs/xfaforms/profile。

Sling指令碼是JSP指令碼。 這些JSP指令碼用作容器，用於將請求的表單和所需的JS/CSS對象的HTML組合在一起。 這些Sling指令碼也稱為 **配置檔案呈現器指令碼**。 配置檔案呈現器調用FormsOSGi服務來呈現所請求的表單。

配置檔案指令碼位於html.jsp和html.POST.jsp中，用於GET和POST請求。 您可以複製和修改一個或多個檔案以覆蓋和添加您的自定義項。 不要進行任何就地更改，修補程式更新會覆蓋此類更改。

配置檔案包含各種模組。 模組包括formRuntime.jsp、config.jsp、toolbar.jsp、formBody.jsp、nav_footer.jsp和footer.jsp。

## formRuntime.jsp {#formruntime-jsp-br}

formRuntime.jsp模組包含客戶端庫的引用。 它還描述了從請求中提取語言環境資訊並在請求中包括本地化消息的方法。 您可以在formRuntime.jsp中包含自己的customJavaScriptlib或樣式。

## config.jsp {#config-jsp}

config.jsp模組包含各種配置，如日誌記錄、代理服務和行為版本。 您可以將自己的配置和小部件定制添加到config.jsp模組中。 您還可以將自定義小部件註冊等配置添加到config.jsp模組。

## toolbar.jsp {#toolbar-jsp}

toolbar.jsp包含用於建立彩色工具欄的代碼。 要刪除工具欄，請從HTML.jsp中刪除toolbar.jsp

## formBody.jsp {#formbody-jsp}

formBody.jsp模組用於XFA表單的HTML表示。

## nav_footer_jsp {#nav-footer-jsp}

首先，HTML5窗體只呈現窗體的第一頁。 當用戶滾動表單時，將載入其餘表單。 它使裝載體驗更快。 nav_footer.jsp元件包含所有樣式和必需元素，以便於在滾動上載入頁面。

## footer.jsp {#footer-jsp}

footer.jsp模組為空。 它允許您添加僅用於用戶交互的指令碼。

## 建立自定義配置檔案 {#creating-custom-profiles}

要建立自定義配置檔案，請執行以下步驟：

### 建立配置檔案節點 {#create-profile-node}

1. 導航到URL上的CRX DE介面： `https://'[server]:[port]'/crx/de` 並使用管理員憑據登錄到介面。

1. 在左窗格中，導航到該位置 */content/xfaforms/profiles*。

1. 複製節點預設值，並將節點貼上到不同的資料夾(*/內容/配置檔案*) *形*。

1. 選擇新節點， *形*，並添加字串屬性： *sling:resourceType* 值： *hrform/demo*。

1. 按一下「在工具欄中全部保存」(Save All in toolbar)菜單以保存更改。

### 建立配置檔案呈現器指令碼 {#create-the-profile-renderer-script}

建立自定義配置檔案後，將呈現資訊添加到此配置檔案。 在收到對新配置檔案的請求時，CRX將驗證要呈現的JSP頁的/apps資料夾是否存在。 在/apps資料夾中建立JSP頁。

1. 在左窗格中，導航到 `/apps` 的子菜單。
1. 按一下右鍵 `/apps` 資料夾，並選擇建立具有名稱的資料夾 **形**。
1. 瞭解 **形** 資料夾建立名為 **演示**。
1. 按一下 **全部保存** 按鈕
1. 導航到 `/libs/xfaforms/profile/html.jsp` 複製節點 **html.jsp**。
1. 貼上 **html.jsp** 節點到 `/apps/hrform/demo` 在上面建立的資料夾同名 **html.jsp** 按一下 **保存**。
1. 如果您有配置檔案指令碼的任何其他元件，請按照步驟1-6在/apps/hrform/demo資料夾中複製這些元件。

1. 要驗證配置檔案是否已建立，請開啟URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

要驗證您的表單， [導入表單](/help/forms/using/get-xdp-pdf-documents-aem.md) 從本地檔案系統到AEM Forms [預覽窗體](/help/forms/using/previewing-forms.md) 伺服器AEM作者實例。
