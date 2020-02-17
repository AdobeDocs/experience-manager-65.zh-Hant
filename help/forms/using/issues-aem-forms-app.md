---
title: 疑難排解AEM Forms應用程式
seo-title: 疑難排解AEM Forms應用程式
description: 瞭解AEM Forms應用程式的常見問題，以及如何疑難排解。
seo-description: 瞭解AEM Forms應用程式的常見問題，以及如何疑難排解。
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 疑難排解AEM Forms應用程式 {#troubleshoot-aem-forms-app}

本文說明在建立AEM Forms應用程式時可能顯示的錯誤訊息，以及解決這些錯誤的步驟。

本文章的章節包括：

* [iOS使用者的附件遺失](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [工作區使用者提交的HTML5表單草稿不會顯示在入口網站上](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [AEM Forms應用程式無法載入HTML5表格（未快取）](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms不會在Windows上同步](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [不支援的Gradle版本](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Gradle和Android Gradle外掛程式相容性問題](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## iOS使用者的附件遺失 {#attachment-loss-for-ios-users}

AEM Forms for iOS應用程式已設定為在OSGi上與AEM Forms同步，僅支援欄位層級的附件。 所有附件都必須具有唯一的名稱。 如果多個附件的名稱相同，則僅保留一個附件，而所有其它具有相同名稱的附件都將丟失。 請執行下列步驟，以防止iOS裝置上的使用者發生資料遺失：

1. 在連線的伺服器上，導覽至 **Adobe Experience Manager >工具>作業> Web Console**。
1. 查找並按一下 **Adaptive Form Configuration Service**。
1. 在「最適化表單配置服務」對話框中，啟用「使 **檔案名唯一」**。

   如果 **停用「使檔案名稱唯一** 」設定，當使用者嘗試提交具有多個附件的最適化表單時，會發生資料遺失。

1. 按一下&#x200B;**「儲存」**。

## 工作區使用者提交的HTML5表單草稿不會顯示在入口網站上 {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

對於在「另存為草稿 **** HTML演算描述檔」的AEM Forms應用程式中啟用的HTML5表格，工作區使用者看不到儲存的草稿。 若要檢視Portal上工作區使用者提交之HTML5表單的已儲存草稿，請執行下列步驟：

1. 開啟CRXDE並使用管理員認證登入。

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. 在CRXDE的根路徑中，在「訪問控制」下的「訪問控制清單」中，按一下 **+**。
1. 在「添 **加新條目** 」對話框中，按一下「承擔者」(Principal)欄位中的組搜索按鈕。
1. 在「選擇承擔者」(Select Principal)對話框的「名稱」(Name)欄位中，鍵入並 `PERM_WORKSPACE_USER` 按一下「搜 **索」(Search**)。
1. 在「選 `PERM_WORKSPACE_USER` 擇承擔者」(Select Principal)對話框中選擇組，然後按一下「確 **定」(OK**)。
1. 在「添加新條目」(Add New Entry)對 `PERM_WORKSPACE_USER` 話框中，「承擔者」(Principal)欄位中選擇了組。

   啟用 `jcr:read` 使用者群組的權限。

1. 按一下 **確定**。

## AEM Forms應用程式無法載入HTML5表格（未快取） {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

當AEM Forms應用程式連線至舊版AEM Forms伺服器時，未快取的HTML5表單無法載入AEM Forms應用程式。

執行下列步驟以解決問題：

1. 在作者例項中，導覽至「 **Adobe Experience Manager >工具>設定Workspace App Offline Service >立即設定」**。
1. 在「工 **作區應用程式離線服務** 」頁面中，按一 **下「手動資源快取」**。

   URL:https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. 在「手 **動資源快取** 」頁籤中，按一下 **** +按鈕以添加CRX路徑。
1. 在「添 **加新資源」欄位中** ，鍵入：/etc.clientlibs/fd/xfaforms/I18N/en_US.js，然後按一下「 **新增」**。
1. 按一下&#x200B;**「儲存」**。

## AEM Forms不會在Windows上同步 {#aem-forms-do-not-sync-on-windows}

在Windows上的AEM Forms應用程式中，如果表單的路徑或其任何資源包含大於或等於256個字元，表單就不會與連線的伺服器同步。

修改表單的路徑及其資源，將字元數減少到256個字元以下。

## 不支援的Gradle版本 {#unsupported-version-of-gradle}

**** 錯誤訊息：專案使用不支援的Gradle版本。

當您在Android studio中建立AEM Forms應用程式時，會顯示錯誤訊息。 由於系統上支援的Gradle版本不受支援，因此出現問題。

**** 解析度：按一 **下「修正Gradle包裝函式」並重新匯入專案** ，以解決問題。

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Gradle和Android Gradle外掛程式相容性問題 {#gradle-and-android-gradle-plug-in-compatibility-issues}

**** 錯誤訊息：Android Gradle外掛程式和Gradle版本不相容。

當您從Android studio使用者介面的「建立」選 **單中選取「建立APK****** 」選項時，會顯示錯誤訊息。

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**** 解析度：開啟 **Gradle Scripts** > **gradle-wrapper.properties** 檔案並編輯 **distributionUrl屬性** 。

例如，Android studio控制台建議將Gradle版本降級為3.5。編輯gradle-wrapper. **properties檔**&#x200B;案的&#x200B;**distributionUrl中的版本** 。

請 **再次選** 取「建立 **>建立APK** 」，以解決錯誤並產生。apk檔案。

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)

