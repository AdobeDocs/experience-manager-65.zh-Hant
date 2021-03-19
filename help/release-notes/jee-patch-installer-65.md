---
title: AEM FormsJEE修補程式安裝程式
description: AEM FormsJEE修補程式安裝程式
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 28%

---


# AEM FormsJEE修補程式安裝程式{#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[如需詳](https://www.adobe.com/tw/account/sign-in.supportportal.html) 細資訊或取得修補程式，請洽詢支援。

## 關於修補程式安裝程式{#about-the-patch-installer}

6.AEM5FormsJEE修補程式安裝程式包含6.5FormsJEE所有元件的所有已修AEM正問題，直到本修補程式發行為止。 有關已修復問題的完整清單，請參閱最新的[Service Pack發行說明](sp-release-notes.md)。

## 安裝修補程式{#prerequisites-to-installing-the-patch}的先決條件

* AEM 6.5Forms

## 安裝和配置修補程式{#installing-and-configuring-the-patch}

1. 備份&lt;*AEM_forms_root*/deploy資料夾。 如果決定解除安裝快速修正，則此為必要操作。
1. 停止應用程式伺服器。
1. 將修補程式安裝程式封存檔案解壓縮至硬碟。
1. 在根據您使用的作業系統命名的目錄中：

   * **Windows**
導覽至您複製安裝程式之硬碟上安裝媒體或資料夾的適當目錄，然後按兩下aemforms65_cfp_install.exe檔案。

      * （Windows 32位元）`Windows\Disk1\InstData\VM`
      * （Windows 64位元）`Windows_64Bit`\ `Disk1\InstData\VM`
   * ****
Linux導覽至適當的目錄，然後從命令提示符鍵入 
`./aem65_cfp_install.bin`。

      * (Linux) `Linux/Disk1/InstData/NoVM`

   這會啟動安裝精靈，引導您完成安裝。

1. 在 Introduction 面板上，按一下 **[!UICONTROL Next]**。
1. 在「選擇安裝資料夾」螢幕上，驗證顯示的預設位置是否適用於現有安裝，或按一下&#x200B;**[!UICONTROL Browse]**&#x200B;選擇安裝表單的備用資料夾，然後按一下AEM **[!UICONTROL Next]**。
1. 閱讀 Quick Fix Patch Summary 資訊，然後按一下 **[!UICONTROL Next]**。
1. 閱讀 Pre-Installation Summary 資訊，然後按一下 **[!UICONTROL Install]**。
1. 安裝後，按一下 **[!UICONTROL Next]**，將快速修正更新套用至已安裝的檔案。

1. 在按一下「完成」之前，請取消選擇「啟動配置管理器」選項。 在使用&#x200B;**ConfigurationManager.exe或** ConfigurationManager_IPv6.exe **運行配置管理器之前，請導航至&#x200B;*&lt;AEMForms_Install_Dir>\configurationManager\bin*目錄，並將** axis.jar **軸更新為**-1.4.1.1.jar **，在以下檔案中：**

   * ConfigurationManager.lax
   * ConfigurationManager_IPv6.lax

1. 預設情況下，「啟動配置管理器」(Start Configuration Manager)複選框處於選中狀態。 按一下 **[!UICONTROL Done]**，執行 Configuration Manager。

1. 若要稍後執行 Configuration Manager，請取消選取 Start Configuration Manager 選項，再按一下 Done。您稍後可以使用`[AEM_forms_root]/configurationManager/bin`目錄中的相應指令碼啟動Configuration Manager。

1. 根據您的應用程式伺服器，選擇下列其中一份檔案，並依照&#x200B;*設定和部署表AEM單*&#x200B;一節中的指示進行。

   * [安裝和部AEM署JBoss表單](http://www.adobe.com/go/learn_aemforms_installJBoss_65_tw)
   * [安裝和部AEM署WebSphere表單](http://www.adobe.com/go/learn_aemforms_installWebSphere_65_tw)

1. （僅限JBoss）安裝修補程式並配置伺服器後，刪除JBoss應用程式伺服器的tmp和工作目錄。

## 部署後配置{#post-deployment-configurations}

### SAML組態{#saml-configurations}

如果您已設定SAML驗證，並且遇到大型IDP中繼資料的問題，請在安裝修補程式後執行下列動作：

1. 在應用程式伺服器中設定以下系統屬性：\
   `um.saml.enable.large.xml=true`
1. 重新啟動伺服器。
1. 刪除現有的SAML驗證提供者，並依SAML設定中所述，重新新增現有網域的提供者。

## 受影響的模組{#impacted-modules}

* 文件服務
* Document Security
* Foundation JEE

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
