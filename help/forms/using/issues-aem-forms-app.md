---
title: 疑難排解AEM Forms應用程式
seo-title: Troubleshoot AEM Forms app
description: 了解AEM Forms應用程式的常見問題及疑難排解方法。
seo-description: Learn about common issues with AEM Forms app and how to troubleshoot them.
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
exl-id: caec5fc3-db52-4bf5-8eb2-17e5189ab819
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 1%

---

# 疑難排解AEM Forms應用程式 {#troubleshoot-aem-forms-app}

本文說明建置AEM Forms應用程式時可能顯示的錯誤訊息，以及解決這些錯誤的步驟。

本文章的章節包括：

* [iOS使用者的附件遺失](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [HTML工作區使用者提交的5份表單草稿不會顯示在入口網站上](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [HTML5表單（未快取）無法在AEM Forms應用程式中載入](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms不在Windows上同步](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [不支援的Gradle版本](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Gradle和Android Gradle外掛程式相容性問題](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## iOS使用者的附件遺失 {#attachment-loss-for-ios-users}

AEM Forms app for iOS已設定為在OSGi上與AEM Forms同步，僅支援欄位層級的附件。 所有附件的名稱都必須唯一。 如果多個附件的名稱相同，則只會保留一個附件，而所有其他名稱相同的附件都將丟失。 執行下列步驟來防止iOS裝置上的使用者發生資料遺失：

1. 在連接的伺服器上，導航到 **Adobe Experience Manager >工具>操作> Web Console**.
1. 尋找並按一下 **[!UICONTROL 最適化表單與互動式通訊Web通道設定]**.
1. 在 [!UICONTROL 最適化表單與互動式通訊Web通道設定] 對話框，啟用 **使檔案名稱唯一**.

   若 **使檔案名稱唯一** 設定已停用，如果使用者嘗試提交包含多個附件的適用性表單，會發生資料遺失的情況。

1. 按一下「**儲存**」。

## HTML工作區使用者提交的5份表單草稿不會顯示在入口網站上 {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

針對HTML5表單，在AEM Forms應用程式中啟用 **另存為草稿** HTML呈現設定檔，工作區使用者看不到儲存的草稿。 要在門戶上查看工作區用戶提交的HTML5表單的已保存草稿，請執行以下步驟：

1. 開啟CRXDE並使用管理員憑證登入。

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. 在CRXDE的根路徑中，在「訪問控制」下的「訪問控制清單」中，按一下 **+**.
1. 在 **新增參加項目** 對話框，按一下「承擔者」(Principal)欄位中的「組搜索」(group search)按鈕。
1. 在「選擇承擔者」(Select Principal)對話框的「名稱」(Name)欄位中，鍵入 `PERM_WORKSPACE_USER` 按一下 **搜尋**.
1. 選擇 `PERM_WORKSPACE_USER` 組(在「選擇承擔者」(Select Principal)對話框中)，然後按一下 **確定**.
1. 在「添加新條目」對話框中， `PERM_WORKSPACE_USER` 在「主體」(Principal)欄位中選擇了組。

   啟用 `jcr:read` 使用者群組的權限。

1. 按一下&#x200B;**「確定」**。

## HTML5表單（未快取）無法在AEM Forms應用程式中載入 {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

AEM Forms應用程式連線至舊版AEM Forms伺服器時，非快取的HTML5表單無法載入AEM Forms應用程式。

執行下列步驟以解決問題：

1. 在製作例項中，導覽至 **Adobe Experience Manager >工具>設定Workspace應用程式離線服務>立即設定**.
1. 在 **Workspace應用程式離線服務** 頁面，按一下 **手動資源快取**.

   URL:https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. 在 **手動資源快取** ，按一下 **+** 按鈕以新增CRX路徑。
1. 在 **新增資源** 欄位，類型：/etc.clientlibs/fd/xfaforms/I18N/en_US.js **新增**.
1. 按一下「**儲存**」。

## AEM Forms不在Windows上同步 {#aem-forms-do-not-sync-on-windows}

在Windows上的AEM Forms應用程式中，如果表單的路徑或其任何資源包含大於或等於256個字元，表單就不會與連線的伺服器同步。

修改表單的路徑及其資源，將字元數減少至256個字元以下。

## 不支援的Gradle版本 {#unsupported-version-of-gradle}

**錯誤訊息：** 專案使用的Gradle版本不支援。

在Android Studio中建置AEM Forms應用程式時，會顯示錯誤訊息。 由於系統上支援的Gradle版本不受支援，因此會發生問題。

**解決方法：** 按一下 **修正Gradle包裝函式並重新匯入專案** 以解決問題。

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Gradle和Android Gradle外掛程式相容性問題 {#gradle-and-android-gradle-plug-in-compatibility-issues}

**錯誤訊息：** Android Gradle外掛程式和Gradle的版本不相容。

選取「 」時，會顯示錯誤訊息 **建置APK** 選項 **建置** 功能表。

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**解決方法：** 開啟 **Gradle指令碼** > **gradle-wrapper.properties** 檔案和編輯 **distributionUrl** 屬性。

例如，Android Studio控制台建議將Gradle版本降級為3.5。在中編輯版本 **distributionUrl** of **gradle-wrapper.properties** 檔案。

選擇 **建置** > **建置APK** 再次，以解決錯誤並產生.apk檔案。

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
