---
title: 建立HTML5表單的自訂設定檔
description: HTML5表單設定檔是Apache Sling中的資源節點。 它代表HTML5表單轉譯器服務的自訂版本。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: HTML5 Forms,Mobile Forms
exl-id: cf86c810-c466-4894-acc2-d4faf49754cc
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# 建立HTML5表單的自訂設定檔 {#creating-a-custom-profile-for-html-forms}

設定檔是[Apache Sling](https://sling.apache.org/)中的資源節點。 它代表HTML5表單轉譯服務的自訂版本。 您可以使用HTML5表單轉譯服務來自訂HTML5表單的外觀、行為和互動。 設定檔節點存在於JCR存放庫的`/content`資料夾中。 您可以直接將節點放在`/content`資料夾或`/content`資料夾的任何子資料夾下。

設定檔節點具有&#x200B;**sling：resourceSuperType**&#x200B;屬性，預設值為&#x200B;**xfaforms/profile**。 節點的轉譯器指令碼位於/libs/xfaforms/profile。

Sling指令碼是JSP指令碼。 這些JSP指令碼可當作容器，用來將請求表單的HTML與必要的JS / CSS成品放在一起。 這些Sling指令碼也稱為&#x200B;**設定檔轉譯器指令碼**。 設定檔轉譯器會呼叫Forms OSGi服務來轉譯請求的表單。

針對GET和POST要求，設定檔指令碼位於html.jsp和html.POST.jsp中。 您可以複製和修改一或多個檔案，以覆寫和新增自訂。 請勿進行任何就地變更，修補程式更新會覆寫此類變更。

設定檔包含各種模組。 這些模組是formRuntime.jsp、config.jsp、toolbar.jsp、formBody.jsp、nav_footer.jsp和footer.jsp。

## formRuntime.jsp {#formruntime-jsp-br}

formRuntime.jsp模組包含使用者端程式庫的參照。 它也會說明從要求中擷取地區設定資訊的方法，並在要求中包含當地語系化的訊息。 您可以在formRuntime.jsp中包含自己的customJavaScript程式庫或樣式。

## config.jsp {#config-jsp}

config.jsp模組包含各種設定，例如記錄、Proxy服務和行為版本。 您可以將自己的設定和Widget自訂新增到config.jsp模組。 您也可以將設定（例如自訂Widget註冊）新增到config.jsp模組。

## toolbar.jsp {#toolbar-jsp}

toolbar.jsp包含建立彩色工具列的程式碼。 若要移除工具列，請從HTML.jsp中移除toolbar.jsp

## formBody.jsp {#formbody-jsp}

formBody.jsp模組用於XFA表單的HTML表示。

## nav_footer.jsp {#nav-footer-jsp}

最初，HTML5表單只會呈現表單的第一頁。 當使用者捲動表單時，則會載入其餘表單。 這可讓載入體驗更快。 nav_footer.jsp元件包含所有樣式和必要元素，以便在捲動時載入頁面。

## footer.jsp {#footer-jsp}

footer.jsp模組是空的。 它可讓您新增僅用於使用者互動的指令碼。

## 建立自訂設定檔 {#creating-custom-profiles}

若要建立自訂設定檔，請執行下列步驟：

### 建立設定檔節點 {#create-profile-node}

1. 導覽至URL為`https://'[server]:[port]'/crx/de`的CRX DE介面，並使用系統管理員認證登入介面。

1. 在左窗格中，導覽至位置&#x200B;*/content/xfaforms/profiles*。

1. 複製節點預設值，並將節點貼到名稱為&#x200B;*hrform*&#x200B;的不同資料夾(*/content/profiles*)中。

1. 選取新節點&#x200B;*hrform*，然後新增字串屬性： *sling：resourceType*，值為： *hrform/demo*。

1. 按一下工具列功能表中的「儲存全部」以儲存變更。

### 建立設定檔轉譯器指令碼 {#create-the-profile-renderer-script}

建立自訂設定檔後，將轉譯器資訊新增到此設定檔。 在收到新設定檔的請求時，CRX會驗證/apps資料夾是否存在，以便JSP頁面進行轉譯。 在/apps資料夾中建立JSP頁面。

1. 在左窗格中，導覽至`/apps`資料夾。
1. 在`/apps`資料夾上按一下滑鼠右鍵，然後選擇建立名稱為&#x200B;**hrform**&#x200B;的資料夾。
1. **hrform**&#x200B;資料夾的內部人員建立名為&#x200B;**demo**&#x200B;的資料夾。
1. 按一下&#x200B;**儲存全部**&#x200B;按鈕。
1. 導覽至`/libs/xfaforms/profile/html.jsp`並複製節點&#x200B;**html.jsp**。
1. 將&#x200B;**html.jsp**&#x200B;節點貼到上面建立的`/apps/hrform/demo`資料夾中（具有相同名稱&#x200B;**html.jsp**），然後按一下&#x200B;**儲存**。
1. 如果您有任何其他設定檔指令碼元件，請依照步驟1-6複製/apps/hrform/demo資料夾中的元件。

1. 若要確認設定檔已建立，請開啟URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

若要驗證您的表單，請[將表單從本機檔案系統匯入](/help/forms/using/get-xdp-pdf-documents-aem.md)到AEM Forms，並在AEM伺服器作者執行個體上[預覽表單](/help/forms/using/previewing-forms.md)。
