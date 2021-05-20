---
title: 疑難排解AEM Forms應用程式
seo-title: 疑難排解AEM Forms應用程式
description: 了解AEM Forms應用程式的常見問題及疑難排解方法。
seo-description: 了解AEM Forms應用程式的常見問題及疑難排解方法。
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
exl-id: caec5fc3-db52-4bf5-8eb2-17e5189ab819
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---

# 疑難排解AEM Forms應用程式{#troubleshoot-aem-forms-app}

本文說明建置AEM Forms應用程式時可能顯示的錯誤訊息，以及解決這些錯誤的步驟。

本文章的章節包括：

* [iOS使用者的附件遺失](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [工作區使用者提交的HTML5表單草稿不會顯示在入口網站上](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [HTML5表單（未快取）無法載入AEM Forms應用程式](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms不在Windows上同步](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [不支援的Gradle版本](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Gradle和Android Gradle外掛程式相容性問題](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## iOS用戶的附件丟失{#attachment-loss-for-ios-users}

iOS適用的AEM Forms應用程式已設定為在OSGi上與AEM Forms同步，僅支援欄位層級的附件。 所有附件的名稱都必須唯一。 如果多個附件的名稱相同，則只會保留一個附件，而所有其他名稱相同的附件都將丟失。 執行下列步驟來防止iOS裝置上的使用者發生資料遺失：

1. 在連接的伺服器上，導航至&#x200B;**Adobe Experience Manager >工具>操作> Web Console**。
1. 查找並按一下&#x200B;**[!UICONTROL 自適應表單和互動式通信Web通道配置]**。
1. 在[!UICONTROL 適用性表單和互動式通信Web通道配置]對話框中，啟用&#x200B;**使檔案名稱唯一**。

   如果&#x200B;**將檔案名稱設為唯一**&#x200B;設定停用，如果使用者嘗試提交包含多個附件的適用性表單，便會發生資料遺失。

1. 按一下「**儲存**」。

## 工作區使用者提交的HTML5表單草稿不會顯示在入口網站{#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}上

若為在具有&#x200B;**另存為草稿** HTML轉譯設定檔的AEM Forms應用程式中啟用的HTML5表單，工作區使用者看不到儲存的草稿。 若要檢視入口網站上工作區使用者提交之HTML5表單的已儲存草稿，請執行下列步驟：

1. 開啟CRXDE並使用管理員憑證登入。

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. 在CRXDE的根路徑中，在「訪問控制」下的「訪問控制清單」中，按一下&#x200B;**+**。
1. 在&#x200B;**添加新條目**&#x200B;對話框中，按一下「承擔者」欄位中的組搜索按鈕。
1. 在「選擇主體」對話框的「名稱」欄位中，鍵入`PERM_WORKSPACE_USER`，然後按一下&#x200B;**Search**。
1. 在「選擇主體」對話框中選擇`PERM_WORKSPACE_USER`組，然後按一下「**確定**」。
1. 在「添加新條目」(Add New Entry)對話框中，在「主體」(Principal)欄位中選擇了`PERM_WORKSPACE_USER`組。

   為用戶組啟用`jcr:read`權限。

1. 按一下&#x200B;**「確定」**。

## AEM Forms應用程式{#html-forms-not-cached-fail-to-load-in-aem-forms-app}中無法載入HTML5表單（未快取）

AEM Forms應用程式連線至舊版AEM Forms伺服器時，非快取的HTML5表單無法在AEM Forms應用程式中載入。

執行下列步驟以解決問題：

1. 在製作例項中，導覽至「**Adobe Experience Manager >工具>設定Workspace應用程式離線服務>立即設定**」。
1. 在&#x200B;**Workspace App Offline Service**&#x200B;頁面中，按一下&#x200B;**手動資源快取**。

   URL:https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. 在&#x200B;**手動資源快取**&#x200B;標籤中，按一下&#x200B;**+**&#x200B;按鈕以新增CRX路徑。
1. 在&#x200B;**Add a New Resource**&#x200B;欄位中，鍵入：/etc.clientlibs/fd/xfaforms/I18N/en_US.js ，然後按一下&#x200B;**Add**。
1. 按一下「**儲存**」。

## AEM Forms不在Windows上同步{#aem-forms-do-not-sync-on-windows}

在Windows上的AEM Forms應用程式中，如果表單的路徑或其任何資源包含大於或等於256個字元，表單就不會與連線的伺服器同步。

修改表單的路徑及其資源，將字元數減少至256個字元以下。

## 不支援的Gradle {#unsupported-version-of-gradle}版本

**錯誤訊息：** 專案使用的Gradle版本不支援。

在Android Studio中建置AEM Forms應用程式時，會顯示錯誤訊息。 由於系統上支援的Gradle版本不受支援，因此會發生問題。

**解決方法：** 按一 **下「修正Gradle包裝函式」並重新匯** 入專案以解決問題。

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Gradle和Android Gradle外掛程式相容性問題{#gradle-and-android-gradle-plug-in-compatibility-issues}

**錯誤訊息：** Android Gradle外掛程式和Gradle的版本不相容。

當您從Android Studio使用者介面的&#x200B;**Build**&#x200B;選單中選取&#x200B;**Build APK**&#x200B;選項時，會顯示錯誤訊息。

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**解決方法：** 開 **啟Gradle指令碼**  >  **Gradle-wrapper.** propertyfiles並編輯 **** distributionUrlproperty。

例如，Android Studio控制台建議將Gradle版本降級為3.5。在&#x200B;**gradle-wrapper.properties**&#x200B;檔案的&#x200B;**distributionUrl**&#x200B;中編輯版本。

再次選擇&#x200B;**Build** > **Build APK**&#x200B;以解決錯誤並產生.apk檔案。

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
