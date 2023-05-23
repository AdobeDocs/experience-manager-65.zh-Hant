---
title: 排除AEM Forms應用的故障
seo-title: Troubleshoot AEM Forms app
description: 瞭解AEM Forms應用的常見問題以及如何解決這些問題。
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

# 排除AEM Forms應用的故障 {#troubleshoot-aem-forms-app}

本文介紹在構建AEM Forms應用時可能顯示的錯誤資訊以及解決這些錯誤的步驟。

本文的章節包括：

* [iOS用戶附件丟失](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [HTML用戶提交的5個表單草稿在門戶上不可見](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [HTML5個表單（未快取）無法在AEM Forms應用中載入](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms不在Windows上同步](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [不支援的Gradle版本](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Gradle和Android Gradle插件相容性問題](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## iOS用戶附件丟失 {#attachment-loss-for-ios-users}

AEM FormsiOS應用配置為在OSGi上與AEM Forms同步，只支援現場級附件。 所有附件必須具有唯一的名稱。 如果多個附件的名稱相同，則只保留一個附件，而所有具有相同名稱的附件都將丟失。 執行以下步驟以防止iOS設備上的用戶發生資料丟失：

1. 在連接的伺服器上，導航到 **Adobe Experience Manager>工具>操作> Web控制台**。
1. 查找並按一下 **[!UICONTROL 自適應形式與交互通信Web通道配置]**。
1. 在 [!UICONTROL 自適應形式與交互通信Web通道配置] 對話框，啟用 **使檔案名唯一**。

   如果 **使檔案名唯一** 設定被禁用，如果用戶嘗試提交具有多個附件的自適應表單，則會丟失資料。

1. 按一下「**儲存**」。

## HTML用戶提交的5個表單草稿在門戶上不可見 {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

對於在AEM Forms應用中啟用的HTML5表單 **另存為草稿** HTML呈現配置檔案，保存的草稿對工作區用戶不可見。 要查看門戶上工作區用戶提交的HTML5表單的已保存草稿，請執行以下步驟：

1. 開啟CRXDE並使用管理員憑據登錄。

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. 在CRXDE的根路徑中，在「訪問控制」下的「訪問控制清單」中，按一下 **+**。
1. 在 **添加新條目** 對話框，按一下「承擔者」(Principal)欄位中的組搜索按鈕。
1. 在「選擇承擔者」(Select Principal)對話框的「名稱」(Name)欄位中，鍵入 `PERM_WORKSPACE_USER` 按一下 **搜索**。
1. 選擇 `PERM_WORKSPACE_USER` 在「選擇承擔者」(Select Principal)對話框中，按一下 **確定**。
1. 在「添加新條目」對話框中， `PERM_WORKSPACE_USER` 在「承擔者」(Principal)欄位中選擇組。

   啟用 `jcr:read` 用戶組的權限。

1. 按一下&#x200B;**「確定」**。

## HTML5個表單（未快取）無法在AEM Forms應用中載入 {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

當AEM Forms應用連接到舊版本的AEM Forms伺服器時，未快取的HTML5表單無法載入到AEM Forms應用。

請執行以下步驟來解決問題：

1. 在作者實例中，導航到 **Adobe Experience Manager>工具>配置Workspace App離線服務>立即配置**。
1. 在 **Workspace應用離線服務** 的 **手動資源快取**。

   URL:https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. 在 **手動資源快取** 頁籤 **+** 按鈕來添加CRX路徑。
1. 在 **添加新資源** 欄位，類型：/etc.clientlibs/fd/xfaforms/I18N/en_US.js，按一下 **添加**。
1. 按一下「**儲存**」。

## AEM Forms不在Windows上同步 {#aem-forms-do-not-sync-on-windows}

在Windows上的AEM Forms應用程式中，如果表單的路徑或其任何資源包含的字元大於或等於256個，則表單不會與連接的伺服器同步。

修改表單的路徑及其資源，將字元數減少到少於256個字元。

## 不支援的Gradle版本 {#unsupported-version-of-gradle}

**錯誤消息：** 項目使用的Gradle版本不受支援。

在Android Studio中生成AEM Forms應用時，將顯示錯誤消息。 由於系統上支援的Gradle版本不受支援，導致出現問題。

**解決方案：** 按一下 **修復Gradle包裝並重新導入項目** 來解決問題。

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Gradle和Android Gradle插件相容性問題 {#gradle-and-android-gradle-plug-in-compatibility-issues}

**錯誤消息：** Android Gradle插件和Gradle的版本不相容。

當您選擇 **生成APK** 的 **生成** 菜單。

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**解決方案：** 開啟 **圖形指令碼** > **gradle-wrapper.properties** 檔案和編輯 **分發URL** 屬性。

例如，Android Studio控制台建議將Gradle版本降級為3.5。在中編輯版本 **分發URL**&#x200B;共&#x200B;**gradle-wrapper.properties** 的子菜單。

選擇 **生成** > **生成APK** 再次解決錯誤並生成.apk檔案。

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
