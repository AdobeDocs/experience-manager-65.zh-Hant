---
title: 建立HTML5表單的自訂描述檔
seo-title: 建立HTML5表單的自訂描述檔
description: HTML5表單描述檔是Apache Sling中的資源節點。 它代表自訂版本的HTML5 Forms Render服務。
seo-description: HTML5表單描述檔是Apache Sling中的資源節點。 它代表自訂版本的HTML5 Forms Render服務。
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
translation-type: tm+mt
source-git-commit: 19299fb5fc764d0e71c0ea3a5ec2286183dd6861

---


# 建立HTML5表單的自訂描述檔 {#creating-a-custom-profile-for-html-forms}

描述檔是 [Apache Sling中的資源節點](https://sling.apache.org/)。 它代表HTML5表單轉譯服務的自訂版本。 您可以使用HTML5表單轉譯服務來自訂HTML5表單的外觀、行為和互動。 JCR儲存庫中的文 `/content` 件夾中存在配置檔案節點。 您可以將節點直接放在資料夾或 `/content` 資料夾的任何子資料夾 `/content` 下。

描述檔節點具 **有sling:resourceSuperType** 屬性，預設值為 **xfaforms/profile**。 節點的演算指令碼位於/libs/xfaforms/profile。

Sling指令碼是JSP指令碼。 這些JSP指令碼可當成容器，用來將要求表單的HTML和必要的JS / CSS工件組合在一起。 這些Sling指令碼也稱為 **Profile Renderer指令碼**。 描述檔轉譯器會呼叫Forms OSGi服務，以轉譯要求的表單。

描述檔指令碼位於html.jsp和html.POST.jsp中，以處理GET和POST要求。 您可以複製並修改一或多個檔案，以覆寫並新增自訂設定。 不要進行任何就地更改，修補程式更新將覆蓋此類更改。

配置檔案包含各種模組。 這些模組包括formRuntime.jsp、config.jsp、toolbar.jsp、formBody.jsp、nav_footer.jsp和footer.jsp。

## formRuntime.jsp {#formruntime-jsp-br}

formRuntime.jsp模組包含客戶端庫的引用。 它還描述了從請求中提取地區資訊並將本地化消息包含在請求中的方法。 您可以在formRuntime.jsp中加入自訂的javascript libs或樣式。

## config.jsp {#config-jsp}

config.jsp模組包含各種配置，如日誌、代理服務和行為版本。 您可以將自己的配置和Widget自定義添加到config.jsp模組中。 您也可以將自訂介面工具集註冊等組態新增至config.jsp模組。

## toolbar.jsp {#toolbar-jsp}

toolbar.jsp包含用於建立彩色工具欄的代碼。 若要移除工具列，請從HTML.jsp移除toolbar.jsp

## formBody.jsp {#formbody-jsp}

formBody.jsp模組用於XFA表單的HTML表示。

## nav_footer.jsp {#nav-footer-jsp}

一開始，HTML5表格只會轉譯表格的第一頁。 當使用者捲動表格時，會載入其餘的表格。 它讓載入體驗更快速。 nav_footer.jsp元件包含所有樣式和所需元素，以方便在捲動時載入頁面。

## footer.jsp {#footer-jsp}

footer.jsp模組為空。 它允許您添加僅用於用戶交互的指令碼。

## 建立自訂描述檔 {#creating-custom-profiles}

要建立自定義配置檔案，請執行以下步驟：

### 建立配置檔案節點 {#create-profile-node}

1. 導覽至URL上的CRX DE介面：並 `https://[server]:[port]/crx/de` 使用管理員憑據登錄到介面。

1. 在左窗格中，導覽至位置/ *內容/xfaforms/描述檔*。

1. 複製節點預設值，並將節點貼到名稱為hrform的不&#x200B;*同資料夾(/content/profiles*) *中*。

1. 選擇新節點、 *hrform*，然後添加字串屬性： *sling:resourceType* with value:hrform/ *demo*。

1. 按一下工具列選單中的「全部儲存」以儲存變更。

### 建立描述檔轉譯器指令碼 {#create-the-profile-renderer-script}

在建立自訂描述檔後，將演算資訊新增至此描述檔。 在收到對新配置檔案的請求時，CRX將驗證是否存在要呈現的JSP頁的/apps資料夾。 在/apps資料夾中建立JSP頁。

1. 在左窗格中，導覽至資料 `/apps` 夾。
1. 按一下右鍵該文 `/apps` 件夾並選擇建立名為hrform的 **資料夾**。
1. 在hrform資料 **夾內** ，建立名為demo的資料 **夾**。
1. 按一下「 **全部儲存** 」按鈕。
1. 導覽至 `/libs/xfaforms/profile/html.jsp` 並複製節 **點html.jsp**。
1. 將 **html.jsp** 節點貼上到上面以相同名稱 `/apps/hrform/demo` html.jsp建立的資料夾中 **，然後按一下「保** 存」 ****。
1. 如果您有任何其他描述檔指令碼元件，請依照步驟1-6複製/apps/hrform/demo檔案夾中的元件。

1. 若要確認已建立描述檔，請開啟URL `https://[server]:[port]/content/xfaforms/profiles/hrform.html`

若要驗證您的表單，請 [將表單從您的本機檔案系統匯入](/help/forms/using/get-xdp-pdf-documents-aem.md) ，並在AEM伺服器 [作者例項上預覽表單](/help/forms/using/previewing-forms.md) 。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
