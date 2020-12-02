---
title: 設定Visual Studio專案並建立Windows應用程式
seo-title: 設定Visual Studio專案並建立Windows應用程式
description: 瞭解如何設定Visual Studio專案以建立AEM Forms Windows行動裝置應用程式。
seo-description: 瞭解如何設定Visual Studio專案以建立AEM Forms Windows行動裝置應用程式。
uuid: 9559e584-2a40-4740-a29a-d7ad66220224
topic-tags: forms-app
discoiquuid: c71c2a17-54f9-4c95-a90a-3c89d6d45721
docset: aem65
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---


# 設定Visual Studio專案並建立Windows應用程式{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms提供AEM Forms應用程式的完整原始碼。 來源包含建立自訂工作區應用程式的所有元件。 原始碼存檔`adobe-lc-mobileworkspace-src-<version>.zip`是軟體分發上`adobe-aemfd-forms-app-src-pkg-<version>.zip`軟體包的一部分。

若要取得AEM Forms應用程式來源，請執行下列步驟：

1. 開啟[軟體分發](https://experience.adobe.com/downloads)。 您必須有Adobe ID才能登入「軟體散發」。
1. 點選頁首功能表中的「Adobe Experience Manager **[!UICONTROL 」。]**
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;區段中：
   1. 從&#x200B;**[!UICONTROL Solution]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL Forms]**。
   2. 選擇包的版本和類型。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，選取「**[!UICONTROL 接受EULA條款]**」，然後點選「**[!UICONTROL 下載]**」。
1. 開啟[包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) ，然後按一下&#x200B;**[!UICONTROL 上載包]**&#x200B;來上載包。
1. 選擇軟體包並按一下&#x200B;**[!UICONTROL Install]**。

1. 若要下載原始碼封存檔，請在您的瀏覽器中開啟`https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip`。\
   來源套件會下載在您的裝置上。

下圖顯示`adobe-lc-mobileworkspace-src-<version>.zip`的提取內容。

![mws-content-1](assets/mws-content-1.png)

下圖顯示`src`資料夾中`windows`資料夾的目錄結構。

![win-dir](assets/win-dir.png)

## 設定環境{#setting-up-the-environment}

對於Windows設備，您需要：

* Microsoft Windows 8.1或Windows 10
* Microsoft Visual Studio 2015
* 適用於Apache Cordova的Microsoft Visual Studio工具

## 為AEM Forms應用程式設定Visual Studio專案{#setting-up-visual-studio-project-for-aem-forms-app}

執行下列步驟，在Visual Studio中設定AEM Forms應用程式專案。

1. 將`adobe-lc-mobileworkspace-src-<version>.zip`封存檔複製到安裝並設定Visual Studio 2015的Windows 8.1或Windows 10裝置的`%HOMEPATH%\Projects`檔案夾。
1. 在`%HOMEPATH%\Projects\MobileWorkspace`目錄中解壓縮歸檔檔案。
1. 導覽至`%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows`目錄。
1. 使用Visual Studio 2015開啟`CordovaApp.sln`檔案，然後繼續建立AEM Forms應用程式。

## 建立AEM Forms應用程式{#build-aem-forms-app}

執行下列步驟以建立和部署AEM Forms應用程式。

>[!NOTE]
>
>儲存在AEM Forms應用程式Windows檔案系統的資料不會加密。 建議您使用像Windows BitLocker Drive Encryption這樣的協力廠商工具來加密磁碟資料。

1. 在Visual Studio標準工具欄中，從構建模式的下拉式清單中選擇&#x200B;**Release**。

1. 根據您的平台選擇Windows-AnyCPU、Windows-x64或Windows-x86。 建議使用Windows-AnyCPU。
1. 在Visual Studio解決方案總管中，以滑鼠右鍵按一下專案&#x200B;**CordovaApp.Windows**，然後選取「商店>建立AppPackages **」。**

   ![createapppackages](assets/createapppackages.png)

   此時會顯示「建立應用程式套件」精靈。

   CordovaApp.Windows_3.0.2.0_anycpu.appx安裝程式檔案是在platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test目錄中建立。

   如果遇到`Retarget to windows 8.1 required`錯誤，請按一下右鍵該錯誤，然後在彈出菜單中選擇&#x200B;**重定位到Windows 8.1**。

   ![重新定位解決方案](assets/retarget-solution.png)

1. 在「建立應用程式套件」精靈中，選取您是否要將應用程式上傳至Windows市集的氣象條件，然後按一下「下一步」。****

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. 視需要變更參數，例如應用程式組建版本的版本和輸出位置。

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. 建立專案後，您可以使用下列方式安裝應用程式：

   * Windows PowerShell
   * Visual Studio

   `.appx`套件需要以下項目才能成功安裝：

   1. WinJS程式庫
   1. 請確定套件隨附自簽證書，或受信任的授權機構簽署公共憑證，例如VeriSign。
   1. 開發人員授權

   Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test目錄包含其中的四個主要元件：

   1. `.appx` 檔案
   1. 憑證（目前為Apache Cordova自行簽署的憑證）
   1. 相依性資料夾
   1. PowerShell檔案（.ps1副檔名）



## 使用Windows PowerShell {#deploying-an-app-using-windows-powershell}部署應用程式

在Windows裝置上安裝應用程式有兩種方式。

### 取得開發人員授權{#by-acquiring-the-developer-license}

1. 按一下右鍵PowerShell檔案(`Add-AppDevPackage.ps1)`，然後選擇「使用PowerShell運行」。****

1. 此設定會提示您取得開發人員授權。 使用Microsoft帳戶認證來取得開發人員授權。\
   本授權有效期為30天，您可免費續約。
1. 當您取得開發人員授權時，安裝程式會在系統上安裝自簽證書，而應用程式會成功安裝。

### 使用企業擁有的設備{#by-using-enterprise-owned-devices}

對於加入至企業網域的企業擁有的裝置，則不需要取得開發人員授權。

企業擁有的裝置使用Windows的專業版和企業版。

Microsoft建議您安裝受信任的授權機構核發的公共憑證，例如VeriSign。

若要部署應用程式：

* 確保設備已加入企業域。
* 啟用組策略設定。

**要啟用組策略設定，請執行以下操作：**

1. 在您的裝置中，執行`gpedit.msc`。
1. 導覽至「**電腦設定>管理範本> Windows元件>應用程式套件部署**」。
1. 在&#x200B;**上按一下滑鼠右鍵，允許所有受信任的應用程式安裝**。
1. 按一下&#x200B;**編輯**&#x200B;並選擇&#x200B;**啟用**。

1. 按一下&#x200B;**「確定」**。

編輯Visual Studio生成的PowerShell指令碼，以阻止它獲取開發人員許可證。

在PowerShell指令碼中，設定變數：`$NeedDeveloperLicense = $false`。

對於未加入網域的裝置，則需要側載產品啟動金鑰。 您可向Windows經銷商購買。

對於Windows 8.1首頁版，沒有群組原則，不允許企業側載，而且您無法將它與企業網域加入。 使用開發人員授權，將應用程式部署在Windows 8.1 Home Edition裝置上。

如需詳細資訊，請按一下[這裡](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx)。

## 使用Visual Studio {#deploying-an-app-using-visual-studio}部署應用程式

若要使用Visual Studio在Windows上安裝應用程式：

1. 使用遠端除錯程式連接裝置。\
   如需詳細資訊，請參閱「在遠端機器上執行Windows市集應用程式」](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine)。[

1. 在Visual Studio中開啟您的應用程式時，從「解決方案平台」清單中選擇Windows-x64、Windows-x86或Windows-AnyCPU，然後選取「遠端機器」****。
1. 您的應用程式已部署在遠端機器上。

