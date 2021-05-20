---
title: 設定Visual Studio項目並構建Windows應用程式
seo-title: 設定Visual Studio項目並構建Windows應用程式
description: 了解如何設定Visual Studio專案以建置AEM Forms Windows行動裝置應用程式。
seo-description: 了解如何設定Visual Studio專案以建置AEM Forms Windows行動裝置應用程式。
uuid: 9559e584-2a40-4740-a29a-d7ad66220224
topic-tags: forms-app
discoiquuid: c71c2a17-54f9-4c95-a90a-3c89d6d45721
docset: aem65
exl-id: ae7340c8-38cc-4b2b-ba17-22011471fd7d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 5%

---

# 設定Visual Studio項目並構建Windows應用程式{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms提供AEM Forms應用程式的完整原始碼。 源包含構建自定義工作區應用程式的所有元件。 原始碼存檔`adobe-lc-mobileworkspace-src-<version>.zip`是Software Distribution上`adobe-aemfd-forms-app-src-pkg-<version>.zip`包的一部分。

若要取得AEM Forms應用程式來源，請執行下列步驟：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;部分：
   1. 從&#x200B;**[!UICONTROL Solution]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms]**。
   2. 選取套件的版本和類型。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，選取「**[!UICONTROL 接受EULA條款]**」，然後點選「**[!UICONTROL 下載]**」。
1. 開啟[套件管理器](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選擇包，然後按一下&#x200B;**[!UICONTROL Install]**。

1. 若要下載原始碼存檔，請在瀏覽器中開啟`https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip`。\
   源包已下載到您的設備上。

下圖顯示提取的`adobe-lc-mobileworkspace-src-<version>.zip`內容。

![mws-content-1](assets/mws-content-1.png)

下圖顯示`src`資料夾中`windows`資料夾的目錄結構。

![win-dir](assets/win-dir.png)

## 設定環境{#setting-up-the-environment}

對於Windows設備，您需要：

* Microsoft Windows 8.1或Windows 10
* Microsoft Visual Studio 2015
* 適用於Apache Cordova的Microsoft Visual Studio Tools

## 設定AEM Forms應用程式的Visual Studio專案{#setting-up-visual-studio-project-for-aem-forms-app}

執行下列步驟以在Visual Studio中設定AEM Forms應用程式專案。

1. 將`adobe-lc-mobileworkspace-src-<version>.zip`歸檔檔案複製到安裝並配置了Visual Studio 2015的Windows 8.1或Windows 10設備中的`%HOMEPATH%\Projects`資料夾。
1. 解壓縮`%HOMEPATH%\Projects\MobileWorkspace`目錄中的封存。
1. 導覽至`%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows`目錄。
1. 使用Visual Studio 2015開啟`CordovaApp.sln`檔案，然後繼續建立AEM Forms應用程式。

## 建立AEM Forms應用程式{#build-aem-forms-app}

執行下列步驟來建置和部署AEM Forms應用程式。

>[!NOTE]
>
>儲存在AEM Forms應用程式的Windows檔案系統上的資料未加密。 建議您使用第三方工具（如Windows BitLocker驅動器加密）來加密磁碟資料。

1. 在Visual Studio Standard工具欄中，從生成模式的下拉清單中選擇&#x200B;**Release**。

1. 根據您的平台選擇Windows-AnyCPU、Windows-x64或Windows-x86。 建議使用Windows-AnyCPU。
1. 在「Visual Studio解決方案資源管理器」中，按一下右鍵項目&#x200B;**CordovaApp.Windows**&#x200B;並選擇&#x200B;**商店>建立AppPackages**。

   ![createapppackages](assets/createapppackages.png)

   此時會出現「建立應用程式套件」精靈。

   CordovaApp.Windows_3.0.2.0_anycpu.appx安裝程式檔案是在platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test目錄中建立的。

   如果遇到錯誤`Retarget to windows 8.1 required`，請按一下右鍵該錯誤，然後在彈出菜單中，選擇&#x200B;**重新定位到Windows 8.1**。

   ![重新定位解決方案](assets/retarget-solution.png)

1. 在「建立應用程式套件」精靈中，選取您是否要將應用程式上傳至windows應用程式商店，然後按一下&#x200B;**Next**。

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. 視需要在參數中進行變更，例如應用程式組建的版本和輸出位置。

   ![createapppackeswizard2](assets/createapppackageswizard2.png)

1. 建置專案後，您可以使用以下項目安裝應用程式：

   * Windows PowerShell
   * Visual Studio

   `.appx`軟體包需要以下項目才能成功安裝：

   1. WinJS程式庫
   1. 確保包附帶自簽名證書，或由受信任機構簽名的公共證書，如VeriSign。
   1. 開發人員授權

   目錄Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test包含其中的四個主要元件：

   1. `.appx` 檔案
   1. 憑證（目前是Apache Cordova自行簽署的憑證）
   1. 相依性資料夾
   1. PowerShell檔案（.ps1副檔名）



## 使用Windows PowerShell {#deploying-an-app-using-windows-powershell}部署應用程式

在Windows設備上安裝應用程式有兩種方式。

### 取得開發人員授權{#by-acquiring-the-developer-license}

1. 按一下右鍵PowerShell檔案(`Add-AppDevPackage.ps1)`，然後選擇&#x200B;**使用PowerShell**&#x200B;運行。

1. 安裝程式會提示您取得開發人員授權。 使用Microsoft帳戶憑證來取得開發人員授權。\
   此授權的有效期為30天，您可以免費續約。
1. 當您取得開發人員授權時，安裝程式會在系統上安裝自簽名憑證，並成功安裝應用程式。

### 使用企業擁有的設備{#by-using-enterprise-owned-devices}

若為加入企業網域的企業擁有裝置，則不需要取得開發人員授權。

企業擁有的設備使用Windows的專業版和企業版。

Microsoft建議您安裝頒發公共證書（如VeriSign）的受信任機構。

部署應用程式：

* 確保設備已加入企業域。
* 啟用組策略設定。

**要啟用組策略設定，請執行以下操作：**

1. 在您的設備中，運行`gpedit.msc`。
1. 導覽至「**電腦配置>管理模板> Windows元件>應用程式包部署**」。
1. 按一下右鍵&#x200B;**允許所有受信任的應用安裝**。
1. 按一下「**編輯**」並選擇「**啟用**」。

1. 按一下&#x200B;**「確定」**。

編輯Visual Studio生成的PowerShell指令碼，以阻止其獲取開發人員許可證。

在PowerShell指令碼中，設定變數：`$NeedDeveloperLicense = $false`。

對於未加入網域的裝置，需要側載產品啟動金鑰。 您可以向Windows經銷商購買。

對於Windows 8.1首頁，沒有組策略，不允許企業側載入，並且不能將其與企業域連接。 使用開發人員許可證在Windows 8.1家庭版設備上部署應用。

如需詳細資訊，請按一下[這裡](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx)。

## 使用Visual Studio {#deploying-an-app-using-visual-studio}部署應用程式

要使用Visual Studio在Windows上安裝應用程式，請執行以下操作：

1. 使用遠程調試器連接設備。\
   有關詳細資訊，請參閱[在遠程電腦上運行Windows應用商店應用](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine)。

1. 在Visual Studio中開啟您的應用程式後，從「解決方案平台」清單中選擇Windows-x64、Windows-x86或Windows-AnyCPU，然後選擇&#x200B;**遠程電腦**。
1. 您的應用程式部署在遠端電腦上。
