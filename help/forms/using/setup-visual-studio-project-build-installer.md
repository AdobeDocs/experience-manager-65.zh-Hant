---
title: 設定Visual studio專案並建立Windows應用程式
seo-title: 設定Visual studio專案並建立Windows應用程式
description: 瞭解如何設定Visual studio專案以建立AEM Forms windows行動裝置應用程式。
seo-description: 瞭解如何設定Visual studio專案以建立AEM Forms windows行動裝置應用程式。
uuid: 9559e584-2a40-4740-a29a-d7ad66220224
topic-tags: forms-app
discoiquuid: c71c2a17-54f9-4c95-a90a-3c89d6d45721
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 設定Visual studio專案並建立Windows應用程式{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms提供AEM Forms應用程式的完整原始碼。 來源包含建立自訂工作區應用程式的所有元件。 原始碼存檔是包 `adobe-lc-mobileworkspace-src-<version>.zip`共用上包的 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 一部分。

若要取得AEM Forms應用程式來源，請執行下列步驟：

1. 導覽至封裝共用\
   URL: `https://<server>:<port>/crx/packageshare`.

1. 下載來源套件。 當您下載套件時，它會新增至您的AEM Forms套件管理員。
1. 下載後，導覽至：和 `https://<server>:<port>/crx/packmgr/index.jsp`安裝 `adobe-aemfd-forms-app-src-pkg-<version>.zip`。

1. 若要下載原始碼封存，請在您的瀏 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 覽器中開啟。\
   來源套件會下載在您的裝置上。

下圖顯示提取的內容 `adobe-lc-mobileworkspace-src-<version>.zip`。

![mws-content-1](assets/mws-content-1.png)

下圖顯示資料夾中資料夾 `windows` 的目錄結 `src` 構。

![win-dir](assets/win-dir.png)

## 設定環境 {#setting-up-the-environment}

對於Windows設備，您需要：

* Microsoft Windows 8.1或Windows 10
* Microsoft Visual Studio 2015
* 適用於Apache Cordova的Microsoft Visual studio工具

## 為AEM Forms應用程式設定Visual studio專案 {#setting-up-visual-studio-project-for-aem-forms-app}

執行下列步驟，在Visual studio中設定AEM Forms應用程式專案。

1. 將封 `adobe-lc-mobileworkspace-src-<version>.zip` 存檔復 `%HOMEPATH%\Projects` 制至已安裝並設定Visual Studio 2015的Windows 8.1或Windows 10裝置的檔案夾。
1. 解壓目錄中的存 `%HOMEPATH%\Projects\MobileWorkspace` 檔。
1. 導覽至目 `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows` 錄。
1. 使用 `CordovaApp.sln` Visual Studio 2015開啟檔案，然後繼續建立AEM Forms應用程式。

## 建立AEM Forms應用程式 {#build-aem-forms-app}

執行下列步驟以建立和部署AEM Forms應用程式。

>[!NOTE]
>
>儲存在AEM Forms應用程式Windows檔案系統的資料不會加密。 建議您使用像Windows bitLocker Drive Encryption這樣的協力廠商工具來加密磁碟資料。

1. 在Visual Studio標準工具列中，從下拉式清 **單中** ，選擇「釋放」以建立模式。

1. 根據您的平台選擇Windows-AnyCPU、Windows-x64或Windows-x86。 建議使用Windows-AnyCPU。
1. 在Visual studio解決方案總管中，以滑鼠右鍵按一下專案 **CordovaApp.Windows** ，然後選 **取「商店」>「建立AppPackages」**。

   ![createapppackages](assets/createapppackages.png)

   此時會顯示「建立應用程式套件」精靈。

   CordovaApp.Windows_3.0.2.0_anycpu.appx安裝程式檔案是在platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test目錄中建立。

   如果您遇到錯 `Retarget to windows 8.1 required`誤，請按一下右鍵該錯誤，然後在彈出式菜單中，選擇「將目 **標重新定位到Windows 8.1**」。

   ![重新定位解決方案](assets/retarget-solution.png)

1. 在「建立應用程式套件」精靈中，選取您是否要將應用程式上傳至Windows市集的天氣，然後按一下「下 **一步**」。

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. 視需要變更參數，例如應用程式組建版本的版本和輸出位置。

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. 建立專案後，您可以使用下列方式安裝應用程式：

   * Windows powerShell
   * Visual Studio
   套件 `.appx` 需要下列項目才能成功安裝：

   1. WinJS程式庫
   1. 請確定套件隨附自簽證書，或受信任的授權機構簽署公共憑證，例如VeriSign。
   1. 開發人員授權
   Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test目錄包含其中的四個主要元件：

   1. `.appx` 檔案
   1. 憑證（目前為Apache Cordova自行簽署的憑證）
   1. 相依性資料夾
   1. PowerShell檔案（.ps1副檔名）



## 使用Windows powerShell部署應用程式 {#deploying-an-app-using-windows-powershell}

在Windows裝置上安裝應用程式有兩種方式。

### 透過取得開發人員授權 {#by-acquiring-the-developer-license}

1. 按一下右鍵PowerShell檔案(, `Add-AppDevPackage.ps1)`然後選擇「 **Run with powerShell**」。

1. 此設定會提示您取得開發人員授權。 使用Microsoft帳戶認證來取得開發人員授權。\
   本授權有效期為30天，您可免費續約。
1. 當您取得開發人員授權時，安裝程式會在系統上安裝自簽證書，而應用程式會成功安裝。

### 使用企業擁有的裝置 {#by-using-enterprise-owned-devices}

對於加入至企業網域的企業擁有的裝置，則不需要取得開發人員授權。

企業擁有的裝置使用Windows的專業版和企業版。

Microsoft建議您安裝受信任的授權機構核發的公共憑證，例如VeriSign。

若要部署應用程式：

* 確保設備已加入企業域。
* 啟用組策略設定。

**要啟用組策略設定，請執行以下操作：**

1. 在您的裝置中，執行 `gpedit.msc`。
1. 導覽至「 **電腦設定>管理範本> windows元件>應用程式套件部署」**。
1. 以滑鼠右鍵按一下「 **允許所有受信任的應用程式安裝**」。
1. 按一 **下「編輯** 」並選 **取「啟用**」。

1. 按一下 **確定**。

編輯Visual studio生成的PowerShell指令碼，以阻止它獲取開發人員許可證。

在PowerShell指令碼中，設定變數： `$NeedDeveloperLicense = $false`。

對於未加入網域的裝置，則需要側載產品啟動金鑰。 您可向Windows經銷商購買。

對於Windows 8.1首頁版，沒有群組原則，不允許企業側載，而且您無法將它與企業網域加入。 使用開發人員授權，將應用程式部署在Windows 8.1 Home Edition裝置上。

如需詳細資訊，請按一 [下這裡](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx)。

## 使用Visual studio部署應用程式 {#deploying-an-app-using-visual-studio}

若要使用Visual studio在Windows上安裝應用程式：

1. 使用遠端除錯程式連接裝置。\
   如需詳細資訊，請參 [閱在遠端機器上執行Windows市集應用程式](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine)。

1. 在Visual studio中開啟您的應用程式時，從「解決方案平台」清單中選擇Windows-x64、Windows-x86或Windows-AnyCPU，然後選取「遠端 **機器」**。
1. 您的應用程式已部署在遠端機器上。

