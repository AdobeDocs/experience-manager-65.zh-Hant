---
title: 設定Visual Studio專案並建置Windows應用程式
description: 瞭解如何設定Visual Studio專案以建置AEM Forms Windows行動裝置應用程式。
topic-tags: forms-app
docset: aem65
exl-id: ae7340c8-38cc-4b2b-ba17-22011471fd7d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 2%

---

# 設定Visual Studio專案並建置Windows應用程式{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms提供AEM Forms應用程式的完整原始碼。 來源包含建立自訂Workspace應用程式的所有元件。 原始程式碼封存`adobe-lc-mobileworkspace-src-<version>.zip`是Software Distribution上`adobe-aemfd-forms-app-src-pkg-<version>.zip`套件的一部分。

若要取得AEM Forms應用程式來源，請執行以下步驟：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 選取標題功能表中可用的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL 篩選器]**&#x200B;區段中：
   1. 從&#x200B;**[!UICONTROL 解決方案]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms]**。
   2. 選取封裝的版本和型別。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 選取適用於您作業系統的封裝名稱，選取&#x200B;**[!UICONTROL 接受EULA條款]**，然後選取&#x200B;**[!UICONTROL 下載]**。
1. 開啟[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant)，然後按一下&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。
1. 選取封裝並按一下&#x200B;**[!UICONTROL 安裝]**。

1. 若要下載原始程式碼封存，請在瀏覽器中開啟`https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip`。\
   來源套件會下載到您的裝置上。

下列影像顯示`adobe-lc-mobileworkspace-src-<version>.zip`的擷取內容。

![mws-content-1](assets/mws-content-1.png)

下列影像顯示`src`資料夾中`windows`資料夾的目錄結構。

![win-dir](assets/win-dir.png)

## 設定環境 {#setting-up-the-environment}

若是Windows裝置，您需要：

* Microsoft Windows 8.1或Windows 10
* Microsoft Visual Studio 2015
* Microsoft Visual Studio Tools for Apache Cordova

## 設定適用於AEM Forms應用程式的Visual Studio專案 {#setting-up-visual-studio-project-for-aem-forms-app}

執行以下步驟，在Visual Studio中設定AEM Forms應用程式專案。

1. 將`adobe-lc-mobileworkspace-src-<version>.zip`封存複製到Windows 8.1或安裝並設定Visual Studio 2015的Windows 10裝置中的`%HOMEPATH%\Projects`資料夾。
1. 擷取`%HOMEPATH%\Projects\MobileWorkspace`目錄中的封存。
1. 導覽至`%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows`目錄。
1. 使用Visual Studio 2015開啟`CordovaApp.sln`檔案，然後繼續建置AEM Forms應用程式。

## 建立AEM Forms應用程式 {#build-aem-forms-app}

執行以下步驟來建立和部署AEM Forms應用程式。

>[!NOTE]
>
>儲存在AEM Forms應用程式之Windows檔案系統上的資料未加密。 建議您使用協力廠商工具（例如Windows BitLocker磁碟機加密）來加密磁碟資料。

1. 在Visual Studio Standard工具列中，從組建模式的下拉式清單中選取&#x200B;**版本**。

1. 根據您的平台選取Windows-AnyCPU、Windows-x64或Windows-x86。 建議使用Windows-AnyCPU。
1. 在Visual Studio方案總管中，以滑鼠右鍵按一下專案&#x200B;**CordovaApp.Windows**，然後選取&#x200B;**市集>建立AppPackages**。

   ![createapppackages](assets/createapppackages.png)

   便會顯示「建立應用程式套件」精靈。

   CordovaApp.Windows_3.0.2.0_anycpu.appx安裝程式檔案是在platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test目錄中建立。

   如果您遇到錯誤`Retarget to windows 8.1 required`，請用滑鼠右鍵按一下該錯誤，然後在快顯功能表中選取&#x200B;**重新鎖定目標到Windows 8.1**。

   ![重新鎖定目標 — 解決方案](assets/retarget-solution.png)

1. 在[建立應用程式封裝]精靈中，選取您是否要上傳應用程式至Windows市集，然後按一下[下一步]&#x200B;**&#x200B;**。

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. 視需要在引數中進行變更，例如應用程式組建的版本和輸出位置。

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. 建立專案後，您可以使用以下方式安裝應用程式：

   * Windows PowerShell
   * Visual Studio

   `.appx`封裝需要下列專案才能成功安裝：

   1. WinJS資料庫
   1. 確保套件隨附自我簽署憑證，或隨附受信任機構簽署的公開憑證（例如VeriSign）。
   1. 開發人員授權

   目錄Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test包含四個主要元件：

   1. `.appx`檔案
   1. 憑證（目前是Apache Cordova的自簽憑證）
   1. 相依性資料夾
   1. PowerShell檔案（.ps1副檔名）

## 使用Windows PowerShell部署應用程式 {#deploying-an-app-using-windows-powershell}

在Windows裝置上安裝應用程式有兩種方式。

### 透過取得開發人員授權 {#by-acquiring-the-developer-license}

1. 以滑鼠右鍵按一下PowerShell檔案( `Add-AppDevPackage.ps1)`，然後選擇&#x200B;**使用PowerShell執行**。

1. 安裝程式會提示您取得開發人員授權。 使用Microsoft帳戶憑證取得開發人員授權。\
   此授權的有效期為30天，您可以免費續約。
1. 當您取得開發人員授權時，安裝程式會在系統上安裝自我簽署憑證，並成功安裝應用程式。

### 透過使用企業擁有的裝置 {#by-using-enterprise-owned-devices}

對於已加入企業網域的企業擁有裝置，不需要取得開發人員授權。

企業擁有的裝置使用Professional和Enterprise版本的Windows。

Microsoft建議您安裝受信任的授權單位，如VeriSign，核發公開憑證。

若要部署應用程式：

* 確定裝置已加入企業的網域。
* 啟用群組原則設定。

**若要啟用群組原則設定：**

1. 在您的裝置上，執行`gpedit.msc`。
1. 瀏覽至&#x200B;**電腦設定>系統管理範本> Windows元件>應用程式套件部署**。
1. 用滑鼠右鍵按一下&#x200B;**允許所有信任的應用程式安裝**。
1. 按一下&#x200B;**編輯**&#x200B;並選取&#x200B;**已啟用**。

1. 按一下&#x200B;**「確定」**。

編輯Visual Studio產生的PowerShell指令碼，以停止其取得開發人員授權。

在PowerShell指令碼中，設定變數： `$NeedDeveloperLicense = $false`。

對於未加入網域的裝置，需要側載產品啟用金鑰。 您可以向Windows經銷商購買。

對於Windows 8.1 Home Edition，沒有群組原則，不允許企業端載入，而且您無法將其加入企業網域。 使用開發人員授權在Windows 8.1 Home Edition裝置上部署應用程式。

如需詳細資訊，請按一下[這裡](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx)。

## 使用Visual Studio部署應用程式 {#deploying-an-app-using-visual-studio}

若要使用Visual Studio在Windows上安裝應用程式：

1. 使用遠端偵錯工具連線裝置。\
   如需詳細資訊，請參閱[在遠端電腦上執行Windows市集應用程式](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine)。

1. 在Visual Studio中開啟應用程式後，從[方案平台]清單中選擇Windows-x64、Windows-x86或Windows-AnyCPU，然後選取&#x200B;**遠端電腦**。
1. 您的應用程式已部署在遠端電腦上。
