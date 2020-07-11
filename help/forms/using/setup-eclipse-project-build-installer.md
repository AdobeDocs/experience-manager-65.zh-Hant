---
title: 建立AEM Forms Android應用程式
seo-title: 建立AEM Forms Android應用程式
description: 設定Android Studio專案並建立適用於Android的AEM Forms應用程式。apk檔案的步驟
seo-description: 設定Android Studio專案並建立適用於Android的AEM Forms應用程式。apk檔案的步驟
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---


# 建立AEM Forms Android應用程式 {#build-the-aem-forms-android-app}

在建議的序列中執行下列步驟，以建立AEM Forms的Android應用程式。

1. [下載AEM Forms App原始程式碼套件](#download-android-zip)
1. [設定環境變數](#set-environment-variable-android)
1. [建立標準AEM Forms應用程式](#set-up-the-xcode-project)

## 下載AEM Forms App原始程式碼套件 {#download-android-zip}

AEM Forms App Source Code Package會參照封存 `adobe-lc-mobileworkspace-src-<version>.zip` 檔。 此封存包含建立自訂AEM Forms應用程式所需的原始碼。 此封存檔包含在「軟 `adobe-aemfd-forms-app-src-pkg-<version>.zip`體散發」上的套件中。

請執行下列步驟以下載檔 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 案：

1. 開放 [軟體散發](https://experience.adobe.com/downloads)。 您必須有Adobe ID才能登入「軟體散發」。
1. 點選 **[!UICONTROL 頁首選單中的]** 「Adobe Experience Manager」。
1. 在「篩 **[!UICONTROL 選器]** 」區段：
   1. 從「 **[!UICONTROL 解決方]** 案 **[!UICONTROL 」下拉式清單中選]** 取「表單」。
   2. 選擇包的版本和類型。 您也可以使用「搜尋 **[!UICONTROL 下載」選項]** ，來篩選結果。
1. 點選適用於您作業系統的套件名稱，選取「 **[!UICONTROL Accept EULA Terms]**」，然後點選「 **[!UICONTROL Download]**」。
1. 開啟「 [套件管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) 」，然後按一 **[!UICONTROL 下「上傳套件]** 」以上傳套件。
1. 選擇軟體包，然後按一下 **[!UICONTROL 安裝]**。
1. 若要下載原始碼封存檔，請在您的瀏覽器中開啟 **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** 。 Android應用程式。zip檔案會下載在您的裝置上。
1. 將。zip檔案的內容解壓縮至您本機檔案系統上的檔案夾。 例如， *C:\&lt;Folder Structure>\adobe-lc-mobileworkspace-src-2.4.20*

下圖顯示資料夾的 `adobe-lc-mobileworkspace-src-<version>.zip\android`結構。

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 設定環境變數 {#set-environment-variable-android}

在開始AEM Forms應用程式的建立程式之前，請先設定下列環境變數：

* 將JAVA_HOME環境變數設定為本地檔案系統上JDK軟體的位置。 例如，C:\Program Files\Java\jdk1.8.0_181
* 將系統 `ANDROID_SDK_ROOT` 環境變數設為Android的SDK位置。 例如，C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* 設定系 `Path` 統環境變數，以包含Android的平台工具和工具檔案夾位置。 例如，C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools。

## 建立標準AEM Forms應用程式 {#set-up-the-xcode-project}

在本機檔案系統上儲存adobe-lc-mobileworkspace-src-&lt;version>.zip檔案並設定環境變數後，請使用下列任一選項建立標準AEM Forms Android應用程式：

* [使用Android Studio建立AEM Forms應用程式](#using-android-studio)
* [使用Android Studio產生。apk檔案](#generate-apk-android-studio)

### 使用Android Studio建立AEM Forms應用程式 {#using-android-studio}

執行下列步驟，以使用Android Studio建立AEM Forms應用程式：

1. 在您的電腦上啟動Android Studio應用程式。
1. 按一 **下「開啟現有的Android Studio專案」**。 如果開啟現有項目的對話框未自動顯示，請選擇「文 **件** 」>「 **開啟」**。
1. 導覽至 *本機檔案系統上的adobe-lc-mobileworkspace-src-&lt;version>.zip/android* ，然後按一下「 **確定」**。

   左 **窗格中** ，會顯示android選項。

   ![android_folder_studio](assets/android_folder_studio.png)

1. 從左 **窗格選取** 「android」，然後按一 **下「執行** > **執行&#39;android&#39;」**。
1. 從「選擇部署目標」對話方塊的「已連線裝置」區段中選取Android裝置，然後按一下「確定」。

   成功建立開發環境後，您現在可以在應用程式上套用自訂設定。 使用下列文章自訂應用程式：

   * [品牌自訂](/help/forms/using/branding-customization.md)
   * [主題自訂](/help/forms/using/theme-customization.md)
   * [手勢自訂](/help/forms/using/gesture-customization.md)

   將適當的自訂項目套用至您的應用程式後，您就可以產生。apk檔案以進行散發。

### 使用Android Studio產生。apk檔案 {#generate-apk-android-studio}

請執行下列步驟，以使用Android Studio產生。apk檔案：

1. 在您的電腦上啟動Android Studio應用程式。
1. 選取「 **開啟現有的Android Studio專案」**。 如果開啟現有項目的對話框未自動顯示，請選擇「文 **件** 」>「 **開啟」**。
1. 導覽至 *本機檔案系統上的adobe-lc-mobileworkspace-src-&lt;version>.zip/android* ，然後按一下「 **確定」**。

   android選項會顯示在左窗格中。

1. 選 **取「建立** >建 **立APK** 」以產生。apk檔案。

   （可選）選 **擇「建置** 」>「 **產生已簽署的APK** 」, [以產生。apk檔案的已簽署版本](https://developer.android.com/studio/publish/app-signing) 。

## 使用Android Debug Bridge {#build-android-debug-bridge}

產生。apk檔案後，請執行下列命令，使用 [Android Debug Bridge在Android裝置上安裝應用程式](https://developer.android.com/tools/help/adb.html)。

**Windows使用者：** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**MAC使用者：** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
