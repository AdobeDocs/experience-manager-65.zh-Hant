---
title: 建立AEM Forms Android應用程式
seo-title: Build the AEM Forms Android app
description: 設定Android Studio專案和為Android適用的AEM Forms應用程式建置.apk檔案的步驟
seo-description: Steps to set up the Android Studio project and build the .apk file for the AEM Forms app for Android
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
exl-id: 3fb069cf-d3ed-47b0-b6bf-82e110b3b059
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 5%

---

# 建立AEM Forms Android應用程式 {#build-the-aem-forms-android-app}

以建議的順序執行下列步驟，為AEM Forms建置Android應用程式。

1. [下載AEM Forms應用程式原始碼套件](#download-android-zip)
1. [設定環境變數](#set-environment-variable-android)
1. [建立標準AEM Forms應用程式](#set-up-the-xcode-project)

## 下載AEM Forms應用程式原始碼套件 {#download-android-zip}

AEM Forms應用程式原始碼套件是指 `adobe-lc-mobileworkspace-src-<version>.zip` 封存。 此封存包含建置自訂AEM Forms應用程式所需的原始碼。 封存包含在 `adobe-aemfd-forms-app-src-pkg-<version>.zip`軟體發佈上可用的套件。

執行下列步驟來下載 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 檔案：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 小節：
   1. 選擇 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 下拉式清單。
   2. 選取套件的版本和類型。 您也可以使用 **[!UICONTROL 搜尋下載]** 選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，然後選取 **[!UICONTROL 接受EULA條款]**，然後點選 **[!UICONTROL 下載]**.
1. 開啟[套件管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選取套件，然後按一下 **[!UICONTROL 安裝]**.
1. 若要下載原始碼封存檔，請開啟 **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** 在瀏覽器中。 裝置上會下載Android應用程式.zip檔案。
1. 將.zip檔案的內容解壓縮至本機檔案系統上的資料夾。 例如， *C:\&lt;folder structure=&quot;&quot;>\adobe-lc-mobileworkspace-src-2.4.20*

下圖顯示 `adobe-lc-mobileworkspace-src-<version>.zip\android`檔案夾。

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 設定環境變數 {#set-environment-variable-android}

開始AEM Forms應用程式的建置程式之前，請設定下列環境變數：

* 將JAVA_HOME環境變數設定為本地檔案系統上JDK軟體的位置。 例如， C:\Program Files\Java\jdk1.8.0_181
* 設定 `ANDROID_SDK_ROOT` 系統環境變數至Android適用的SDK位置。 例如， C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* 設定 `Path` 系統環境變數包含Android的平台工具和工具資料夾位置。 例如， C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools。

## 建立標準AEM Forms應用程式 {#set-up-the-xcode-project}

儲存adobe-lc-mobileworkspace-src後 — &lt;version>.zip檔案，並設定環境變數，使用下列任一選項建立標準AEM Forms Android應用程式：

* [使用Android Studio建立AEM Forms應用程式](#using-android-studio)
* [使用Android Studio產生.apk檔案](#generate-apk-android-studio)

### 使用Android Studio建立AEM Forms應用程式 {#using-android-studio}

執行下列步驟以使用Android Studio建立AEM Forms應用程式：

1. 在電腦上啟動Android Studio應用程式。
1. 按一下 **開啟現有的Android Studio專案**. 如果開啟現有專案的對話方塊未自動顯示，請選取 **檔案** > **開啟**.
1. 導覽至 *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* 在本地檔案系統上，然後按一下 **確定**.

   此 **android** 選項。

   ![android_folder_studio](assets/android_folder_studio.png)

1. 選擇 **android** 按一下左窗格中的 **執行** > **執行&#39;android&#39;**.
1. 從「選擇部署目標」對話框的「已連接設備」部分中選擇Android設備，然後按一下「確定」。

   成功建立開發環境後，您現在可以在應用程式上套用自訂。 使用下列文章來自訂應用程式：

   * [品牌自訂](/help/forms/using/branding-customization.md)
   * [主題自訂](/help/forms/using/theme-customization.md)
   * [手勢自訂](/help/forms/using/gesture-customization.md)

   將適當的自訂套用至您的應用程式後，您可以產生.apk檔案以進行分送。

### 使用Android Studio產生.apk檔案 {#generate-apk-android-studio}

執行下列步驟以使用Android Studio產生.apk檔案：

1. 在電腦上啟動Android Studio應用程式。
1. 選擇 **開啟現有的Android Studio專案**. 如果開啟現有專案的對話方塊未自動顯示，請選取 **檔案** > **開啟**.
1. 導覽至 *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* 在本地檔案系統上，然後按一下 **確定**.

   android選項會顯示在左窗格中。

1. 選擇 **建置** > **建置APK** 來產生.apk檔案。

   （可選）選擇 **建置** > **生成簽名的APK** 生成 [簽名版本](https://developer.android.com/studio/publish/app-signing) .apk檔案的URL。

## 使用Android Debug Bridge {#build-android-debug-bridge}

產生.apk檔案後，請執行下列命令，使用在Android裝置上安裝應用程式 [Android Debug Bridge](https://developer.android.com/tools/help/adb.html).

**Windows用戶：** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Mac使用者：** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
