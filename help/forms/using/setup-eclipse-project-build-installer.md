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


# 建立AEM Forms Android應用程式{#build-the-aem-forms-android-app}

在建議的序列中執行下列步驟，以建立AEM Forms的Android應用程式。

1. [下載AEM Forms App原始程式碼套件](#download-android-zip)
1. [設定環境變數](#set-environment-variable-android)
1. [建立標準AEM Forms應用程式](#set-up-the-xcode-project)

## 下載AEM Forms App Source Code Package {#download-android-zip}

AEM Forms App Source Code Package是指`adobe-lc-mobileworkspace-src-<version>.zip`封存檔。 此封存包含建立自訂AEM Forms應用程式所需的原始碼。 該存檔包含在「軟體分發」上的`adobe-aemfd-forms-app-src-pkg-<version>.zip`軟體包中。

執行以下步驟下載`adobe-aemfd-forms-app-src-pkg-<version>.zip`檔案：

1. 開啟[軟體分發](https://experience.adobe.com/downloads)。 您必須有Adobe ID才能登入「軟體散發」。
1. 點選頁首功能表中的「Adobe Experience Manager **[!UICONTROL 」。]**
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;區段中：
   1. 從&#x200B;**[!UICONTROL Solution]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL Forms]**。
   2. 選擇包的版本和類型。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，選取「**[!UICONTROL 接受EULA條款]**」，然後點選「**[!UICONTROL 下載]**」。
1. 開啟[包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) ，然後按一下&#x200B;**[!UICONTROL 上載包]**&#x200B;來上載包。
1. 選擇軟體包並按一下&#x200B;**[!UICONTROL Install]**。
1. 若要下載原始碼封存檔，請在您的瀏覽器中開啟&#x200B;**https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip**。 Android應用程式。zip檔案會下載到您的裝置上。
1. 將。zip檔案的內容解壓縮至您本機檔案系統上的檔案夾。 例如，*C:\&lt;資料夾結構>\adobe-lc-mobileworkspace-src-2.4.20*

下圖顯示`adobe-lc-mobileworkspace-src-<version>.zip\android`資料夾的結構。

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 設定環境變數{#set-environment-variable-android}

在開始AEM Forms應用程式的建立程式之前，請先設定下列環境變數：

* 將JAVA_HOME環境變數設定為本地檔案系統上JDK軟體的位置。 例如，C:\Program Files\Java\jdk1.8.0_181
* 將`ANDROID_SDK_ROOT`系統環境變數設為Android的SDK位置。 例如，C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* 設定`Path`系統環境變數，以包含Android的平台工具和工具資料夾位置。 例如，C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools。

## 建立標準AEM Forms應用程式{#set-up-the-xcode-project}

在本機檔案系統上儲存adobe-lc-mobileworkspace-src-&lt;version>.zip檔案並設定環境變數後，請使用下列任一選項建立標準AEM Forms Android應用程式：

* [使用Android Studio建立AEM Forms應用程式](#using-android-studio)
* [使用Android Studio產生。apk檔案](#generate-apk-android-studio)

### 使用Android Studio {#using-android-studio}建立AEM Forms應用程式

執行下列步驟，以使用Android Studio建立AEM Forms應用程式：

1. 在您的電腦上啟動Android Studio應用程式。
1. 按一下「**開啟現有的Android Studio專案**」。 如果開啟現有項目的對話框未自動顯示，請選擇&#x200B;**檔案** > **開啟**。
1. 導覽至本機檔案系統上的&#x200B;*adobe-lc-mobileworkspace-src-&lt;version>.zip/android*，然後按一下「確定」**。**

   **android**&#x200B;選項會顯示在左窗格中。

   ![android_folder_studio](assets/android_folder_studio.png)

1. 從左窗格選擇&#x200B;**android**，然後按一下「執行&#x200B;**** > **執行&#39;android&#39;**」。
1. 從「選擇部署目標」對話方塊的「已連線裝置」區段中選取Android裝置，然後按一下「確定」。

   成功建立開發環境後，您現在可以在應用程式上套用自訂設定。 使用下列文章自訂應用程式：

   * [品牌自訂](/help/forms/using/branding-customization.md)
   * [主題自訂](/help/forms/using/theme-customization.md)
   * [手勢自訂](/help/forms/using/gesture-customization.md)

   將適當的自訂項目套用至您的應用程式後，您就可以產生。apk檔案以進行散發。

### 使用Android Studio {#generate-apk-android-studio}產生。apk檔案

請執行下列步驟，以使用Android Studio產生。apk檔案：

1. 在您的電腦上啟動Android Studio應用程式。
1. 選擇「**開啟現有的Android Studio專案**」。 如果開啟現有項目的對話框未自動顯示，請選擇&#x200B;**檔案** > **開啟**。
1. 導覽至本機檔案系統上的&#x200B;*adobe-lc-mobileworkspace-src-&lt;version>.zip/android*，然後按一下「確定」**。**

   android選項會顯示在左窗格中。

1. 選擇&#x200B;**Build** > **Build APK**&#x200B;以產生。apk檔案。

   或者，選擇「**Build** > **生成已簽名的APK**」以生成。apk檔案的[已簽名的版本](https://developer.android.com/studio/publish/app-signing)。

## 使用Android Debug Bridge {#build-android-debug-bridge}

產生。apk檔案後，請執行下列命令，使用[Android Debug Bridge](https://developer.android.com/tools/help/adb.html)在Android裝置上安裝應用程式。

**Windows使用者：** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**MAC使用者：** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
