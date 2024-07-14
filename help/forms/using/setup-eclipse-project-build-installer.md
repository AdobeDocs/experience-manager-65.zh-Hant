---
title: 建立AEM Forms Android應用程式
description: 為Android的Android應用程式設定AEM Forms Studio專案和建置.apk檔案的步驟
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 3fb069cf-d3ed-47b0-b6bf-82e110b3b059
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 2%

---

# 建立AEM Forms Android應用程式 {#build-the-aem-forms-android-app}

若要建置適用於AEM Forms的Android應用程式，請依照建議的順序執行下列步驟。

1. [下載AEM Forms應用程式Source程式碼套件](#download-android-zip)
1. [設定環境變數](#set-environment-variable-android)
1. [建置標準AEM Forms應用程式](#set-up-the-xcode-project)

## 下載AEM Forms應用程式Source程式碼套件 {#download-android-zip}

AEM Forms應用程式Source程式碼套件參考`adobe-lc-mobileworkspace-src-<version>.zip`封存。 此封存包含建置自訂AEM Forms應用程式所需的原始程式碼。 封存包含在Software Distribution可用的`adobe-aemfd-forms-app-src-pkg-<version>.zip`套件中。

若要下載`adobe-aemfd-forms-app-src-pkg-<version>.zip`檔案，請執行下列步驟：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 選取標題功能表中可用的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL 篩選器]**&#x200B;區段中：
   1. 從&#x200B;**[!UICONTROL 解決方案]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms]**。
   2. 選取封裝的版本和型別。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 選取適用於您作業系統的封裝名稱，選取&#x200B;**[!UICONTROL 接受EULA條款]**，然後選取&#x200B;**[!UICONTROL 下載]**。
1. 開啟[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。
1. 選取封裝並按一下&#x200B;**[!UICONTROL 安裝]**。
1. 若要下載原始程式碼封存，請在瀏覽器中開啟&#x200B;**https://&lt;server>：&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip**。 已在您的裝置上下載Android應用程式.zip檔案。
1. 將.zip檔案的內容解壓縮至本機檔案系統上的資料夾。 例如，*C:\&lt;資料夾結構>\adobe-lc-mobileworkspace-src-2.4.20*

下列影像顯示`adobe-lc-mobileworkspace-src-<version>.zip\android`資料夾的結構。

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 設定環境變數 {#set-environment-variable-android}

在開始AEM Forms應用程式的建置流程之前，請設定下列環境變數：

* 將JAVA_HOME環境變數設定為本機檔案系統上JDK軟體的位置。 例如，C:\Program Files\Java\jdk1.8.0_181
* 將`ANDROID_SDK_ROOT`系統環境變數設定為Android的SDK位置。 例如， C:\Users\&amp;amp；lt；username>\AppData\Local\Android\Sdk
* 設定`Path`系統環境變數，以包含Android的平台工具和工具資料夾位置。 例如，C:\Users\&amp;amp；lt；username>\AppData\Local\Android\Sdk\platform-tools和C:\Users\&amp;amp；lt；username>\AppData\Local\Android\Sdk\tools。

## 建置標準AEM Forms應用程式 {#set-up-the-xcode-project}

將adobe-lc-mobileworkspace-src-&lt;version>.zip檔案儲存在本機檔案系統並設定環境變數後，請使用下列任一選項建置標準AEM Forms Android應用程式：

* [使用Android Studio建置AEM Forms應用程式](#using-android-studio)
* [使用Android Studio產生.apk檔案](#generate-apk-android-studio)

### 使用Android Studio建置AEM Forms應用程式 {#using-android-studio}

若要使用Android Studio建置AEM Forms應用程式，請執行下列步驟：

1. 在您的電腦上啟動Android Studio應用程式。
1. 按一下&#x200B;**開啟現有的Android Studio專案**。 如果開啟現有專案的對話方塊未自動顯示，請選取&#x200B;**檔案** > **開啟**。
1. 在本機檔案系統上瀏覽至&#x200B;*adobe-lc-mobileworkspace-src-&lt;version>.zip/android*，然後按一下&#x200B;**確定**。

   **android**&#x200B;選項會顯示在左窗格中。

   ![android_folder_studio](assets/android_folder_studio.png)

1. 從左窗格選取&#x200B;**android**，然後按一下&#x200B;**執行** > **執行&#39;android&#39;**。
1. 從選取部署目標對話方塊中的連線裝置區段選取Android裝置，然後按一下確定。

   成功建立開發環境後，您現在可以在應用程式上套用自訂。 使用下列文章來自訂應用程式：

   * [品牌自訂](/help/forms/using/branding-customization.md)
   * [佈景主題自訂](/help/forms/using/theme-customization.md)
   * [手勢自訂](/help/forms/using/gesture-customization.md)

   將適當的自訂套用至應用程式後，您就可以產生.apk檔案來分發。

### 使用Android Studio產生.apk檔案 {#generate-apk-android-studio}

若要使用Android Studio產生.apk檔案，請執行下列動作：

1. 在您的電腦上啟動Android Studio應用程式。
1. 選取&#x200B;**開啟現有的Android Studio專案**。 如果開啟現有專案的對話方塊未自動顯示，請選取&#x200B;**檔案** > **開啟**。
1. 在本機檔案系統上瀏覽至&#x200B;*adobe-lc-mobileworkspace-src-&lt;version>.zip/android*，然後按一下&#x200B;**確定**。

   Android選項會顯示在左窗格中。

1. 若要產生.apk檔案，請選取&#x200B;**建置** > **建置APK**。

   選擇性地選取&#x200B;**建置** > **產生已簽署的APK**，以產生[已簽署的版本](https://developer.android.com/studio/publish/app-signing)的.apk檔案。

## 使用Android Debug Bridge {#build-android-debug-bridge}

產生.apk檔案後，請使用[Android Debug Bridge](https://developer.android.com/tools/adb)執行以下命令，在Android裝置上安裝應用程式。

**Windows使用者：** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Mac使用者：** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
