---
title: 建立HTML5表單的自訂設定檔
seo-title: 建立HTML5表單的自訂設定檔
description: HTML5表單設定檔是Apache Sling中的資源節點。 它代表HTML5表單呈現服務的自訂版本。
seo-description: HTML5表單設定檔是Apache Sling中的資源節點。 它代表HTML5表單呈現服務的自訂版本。
uuid: b9938280-a92c-4dde-b465-04372db3ca8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: 行動表單
exl-id: cf86c810-c466-4894-acc2-d4faf49754cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# 建立HTML5表單的自訂設定檔{#creating-a-custom-profile-for-html-forms}

設定檔是[Apache Sling](https://sling.apache.org/)中的資源節點。 它代表HTML5表單轉譯服務的自訂版本。 您可以使用HTML5表單轉譯服務來自訂HTML5表單的外觀、行為和互動。 JCR儲存庫的`/content`資料夾中存在配置檔案節點。 您可以將節點直接放在`/content`資料夾或`/content`資料夾的任何子資料夾下。

設定檔節點具有&#x200B;**sling:resourceSuperType**&#x200B;屬性，預設值為&#x200B;**xfaforms/profile**。 節點的呈現指令碼位於/libs/xfaforms/profile。

Sling指令碼是JSP指令碼。 這些JSP指令碼用作容器，用於將請求表單的HTML和所需的JS/CSS對象放在一起。 這些Sling指令碼也稱為&#x200B;**描述檔轉譯器指令碼**。 描述檔轉譯器會呼叫Forms OSGi服務，以轉譯請求的表單。

描述檔指令碼位於html.jsp和html.POST.jsp中，用於GET和POST請求。 您可以複製和修改一或多個檔案以覆寫和新增您的自訂項目。 不要進行任何就地更改，修補程式更新將覆蓋此類更改。

設定檔包含各種模組。 這些模組包括formRuntime.jsp、config.jsp、toolbar.jsp、formBody.jsp、nav_footer.jsp和footer.jsp。

## formRuntime.jsp {#formruntime-jsp-br}

formRuntime.jsp模組包含客戶端庫的引用。 它也描述了從請求中擷取地區設定資訊的方法，以及在請求中包含本地化的訊息。 您可以在formRuntime.jsp中包含自己的customJavaScriptlib或樣式。

## config.jsp {#config-jsp}

config.jsp模組包含各種配置，如日誌記錄、代理服務和行為版本。 您可以將自己的配置和Widget自定義添加到config.jsp模組中。 您也可以將設定（如自訂Widget註冊）新增至config.jsp模組。

## 工具欄.jsp {#toolbar-jsp}

toolbar.jsp包含用於建立彩色工具欄的代碼。 要刪除工具欄，請從HTML.jsp中刪除toolbar.jsp

## formBody.jsp {#formbody-jsp}

formBody.jsp模組用於XFA表單的HTML表示。

## nav_footer.jsp {#nav-footer-jsp}

起初，HTML5表單只會轉譯表單的第一頁。 當使用者捲動表單時，其餘的表單即會載入。 這可讓載入體驗更快。 nav_footer.jsp元件包含所有樣式和所需元素，以便在捲動時載入頁面。

## footer.jsp {#footer-jsp}

footer.jsp模組為空。 它可讓您新增僅用於使用者互動的指令碼。

## 建立自定義配置式{#creating-custom-profiles}

若要建立自訂設定檔，請執行下列步驟：

### 建立配置檔案節點{#create-profile-node}

1. 導覽至URL的CRX DE介面：`https://'[server]:[port]'/crx/de` ，並使用管理員憑證登入介面。

1. 在左窗格中，導覽至&#x200B;*/content/xfaforms/profiles*&#x200B;位置。

1. 複製節點預設值，並將節點貼到名稱為&#x200B;*hrform*&#x200B;的不同資料夾(*/content/profiles*)中。

1. 選取新節點&#x200B;*hrform*，然後新增字串屬性：*sling:resourceType*，值為：*hrform/demo*。

1. 按一下工具列功能表中的「全部儲存」 ，以儲存變更。

### 建立配置式呈現器指令碼{#create-the-profile-renderer-script}

建立自訂設定檔後，將轉譯資訊新增至此設定檔。 CRX在接收到對新配置檔案的請求時，將驗證要呈現的JSP頁是否存在/apps資料夾。 在/apps資料夾中建立JSP頁。

1. 在左窗格中，導覽至`/apps`資料夾。
1. 按一下右鍵`/apps`資料夾，然後選擇建立名為&#x200B;**hrform**&#x200B;的資料夾。
1. 在&#x200B;**hrform**&#x200B;資料夾內，建立名為&#x200B;**demo**&#x200B;的資料夾。
1. 按一下&#x200B;**全部保存**&#x200B;按鈕。
1. 導覽至`/libs/xfaforms/profile/html.jsp`並複製節點&#x200B;**html.jsp**。
1. 將&#x200B;**html.jsp**&#x200B;節點貼入上面以相同名稱&#x200B;**html.jsp**&#x200B;建立的`/apps/hrform/demo`資料夾，然後按一下&#x200B;**儲存**。
1. 如果您有設定檔指令碼的任何其他元件，請依照步驟1至6複製/apps/hrform/demo資料夾中的元件。

1. 若要確認已建立設定檔，請開啟URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

若要驗證表單，請[將表單](/help/forms/using/get-xdp-pdf-documents-aem.md)從本機檔案系統匯入至AEM Forms，並在AEM伺服器製作例項上預覽表單](/help/forms/using/previewing-forms.md)。[
