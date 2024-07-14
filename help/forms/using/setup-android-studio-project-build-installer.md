---
title: 設定Android&amp；trade； studio專案並建置Android&amp；trade；應用程式
description: 設定Android&amp；trade； Studio專案的步驟，以及建立Adobe Experience Manager (AEM) Forms應用程式的安裝程式
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
exl-id: 47d6af00-34d8-4e5d-8117-86fc1b6f58cb
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 2%

---

# 設定Android™ studio專案並建置Android™應用程式 {#set-up-the-android-studio-project-and-build-the-android-app}

本文章適用於建置AEM Forms應用程式6.3.1.1及更新版本。 若要從AEM Forms App 6.3的原始程式碼建置應用程式，請參閱[設定Eclipse專案並建置Android™應用程式](/help/forms/using/setup-eclipse-project-build-installer.md)。

AEM Forms提供AEM Forms應用程式的完整原始碼。 來源包含建立自訂AEM Forms應用程式的所有元件。 原始程式碼封存`adobe-lc-mobileworkspace-src-<version>.zip`是Software Distribution上`adobe-aemfd-forms-app-src-pkg-<version>.zip`套件的一部分。

若要取得AEM Forms應用程式來源，請執行以下步驟：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 選取標題功能表中可用的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL 篩選器]**&#x200B;區段中：
   1. 從&#x200B;**[!UICONTROL 解決方案]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms]**。
   2. 選取封裝的版本和型別。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 選取適用於您作業系統的封裝名稱，選取&#x200B;**[!UICONTROL 接受EULA條款]**，然後選取&#x200B;**[!UICONTROL 下載]**。
1. 開啟[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。
1. 選取封裝並按一下&#x200B;**[!UICONTROL 安裝]**。

下列影像顯示`adobe-lc-mobileworkspace-src-<version>.zip`的擷取內容。

![壓縮的Android™來源擷取的內容](assets/mws-content-1.png)

下列影像顯示`src`資料夾中`android`資料夾的目錄結構。

src](assets/android-folder.png)中Android資料夾的![目錄結構

## 建置標準AEM Forms應用程式 {#set-up-the-xcode-project}

1. 執行以下步驟，在Android™ Studio中設定專案並提供簽署身分：

   登入已安裝並設定Android™ Studio的電腦。

1. 將下載的`adobe-lc-mobileworkspace-src-<version>.zip`封存複製到：

   Mac使用者&#x200B;**的**： `[User_Home]/Projects`

   Windows®使用者&#x200B;**的**： `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >若為Windows®，建議您將Android™專案保留在系統磁碟機中。

1. 解壓縮下列目錄中的封存：

   Mac使用者&#x200B;**的**： `[User_Home]/Projects/[your-project]`

   Windows®使用者&#x200B;**的**： `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >建議您將專案匯入Android™ Studio之前，將擷取的Android專案保留在系統磁碟機中。

1. 啟動Android™ Studio。

   **若為Mac使用者**：更新`[User_Home]/Projects/[your-project]/android`資料夾中存在的`local.properties`檔案，並將`sdk.dir`變數指向案頭上的`SDK`位置。

   **Windows®使用者**：更新`%HOMEPATH%\Projects\[your-project]\android`資料夾中的`local.properties`檔案，並將`sdk.dir`變數指向案頭上的`SDK`位置。

1. 按一下&#x200B;**[!UICONTROL 完成]**&#x200B;以建置專案。

   您可以在ADT Project Explorer中取得專案。

   建置應用程式後![eclipse專案](assets/eclipsebuildmws.png)

1. 在Android™ Studio中，選取&#x200B;**[!UICONTROL 匯入專案（Eclipse ADT、Gradle等）]**。
1. 在專案總管中，選取您要在&#x200B;**根目錄**&#x200B;文字方塊中建立的專案根目錄：

   **適用於Mac使用者：** [User_Home]/Projects/MobileWorkspace/src/android

   Windows®使用者的&#x200B;**：** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. 匯入專案後，快顯視窗中會顯示更新Android™外掛程式Gradle的選項。 視您的需求按一下適當的按鈕。

   ![dontremindmeagainforthisproject](assets/dontremindmeagainforthisproject.png)

1. 成功建置Gradle後，畫面如下。 將適當的裝置或模擬器連線至系統，然後按一下[執行Android] **[!UICONTROL ™]**。

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ Studio會顯示連線的裝置和可用的模擬器。 選取您要執行應用程式的裝置，然後按一下[確定]。****

   ![connecteddevice](assets/connecteddevice.png)

建立專案後，您可以選擇使用Android™Debug Bridge或Android™ Studio安裝應用程式。

### 使用Android™ Debug Bridge {#andriod-debug-bridge}

您可以使用下列命令，透過[Android™ Debug Bridge](https://developer.android.com/tools/adb)在Android™裝置上安裝應用程式：

Mac使用者&#x200B;**的**： `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

Windows®使用者&#x200B;**的**： `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
