---
title: AEM FormsJEE修補程式安裝程式
description: AEM FormsJEE修補程式安裝程式
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: 2c2277f43fe12c4d4fa655c0666519e3608ba3f9
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 29%

---

# AEM FormsJEE修補程式安裝程式 {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[聯繫支援](https://www.adobe.com/tw/account/sign-in.supportportal.html) 的子菜單。

## 關於修補程式安裝程式 {#about-the-patch-installer}

6.AEM5FormsJEE修補程式安裝程式包括在發佈此修補程式之前可用AEM的6.5FormsJEE的所有元件的所有已修復問題。 查看最新  [Service Pack發行說明](release-notes.md) 清單。

## 安裝修補程式的先決條件 {#prerequisites-to-installing-the-patch}

* AEM 6.5Forms

## 安裝和配置修補程式 {#installing-and-configuring-the-patch}

1. 備份&lt;*AEM_表單_根*>/deploy資料夾。 如果決定解除安裝快速修正，則此為必要操作。
1. 停止應用程式伺服器。
1. 將修補程式安裝程式封存檔案解壓縮至硬碟。
1. 在根據您使用的作業系統命名的目錄中：

   * **Windows**
導航到硬碟上安裝介質或資料夾中相應的目錄，在其中複製了安裝程式，然後按兩下aemforms65_cfp_install.exe檔案。

      * （Windows 32位） `Windows\Disk1\InstData\VM`
      * （Windows 64位） `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux**
導航到相應目錄，然後從命令提示符鍵入 
`./aem65_cfp_install.bin`。

      * (Linux) `Linux/Disk1/InstData/NoVM`

   這會啟動安裝精靈，引導您完成安裝。

1. 在 Introduction 面板上，按一下 **[!UICONTROL Next]**。
1. 在「Choose Install Folder（選擇安裝資料夾）」螢幕上，驗證顯示的預設位置是否適合您的現有安裝，或按一下 **[!UICONTROL 瀏覽]** 選擇安裝表單的備AEM用資料夾，然後按一下 **[!UICONTROL 下一個]**。
1. 閱讀 Quick Fix Patch Summary 資訊，然後按一下 **[!UICONTROL Next]**。
1. 閱讀 Pre-Installation Summary 資訊，然後按一下 **[!UICONTROL Install]**。
1. 安裝後，按一下 **[!UICONTROL Next]**，將快速修正更新套用至已安裝的檔案。

1. 按一下「完成」之前，請取消選擇「啟動配置管理器」選項。 在使用 **ConfigurationManager.exe** 或 **ConfigurationManager_IPv6.exe**，導航 *&lt;aemforms_install_dir>\configurationManager\bin* 目錄和更新 `ConfigurationManager.lax` 和 `ConfigurationManager_IPv6.lax` 具有以下更名操作的檔案：

   * `axis.jar` 至 `axis-1.4.1.1.jar`
   * `serializer-2.7.1.jar` 至 `serializer-2.7.2.jar`
   * `xalan-2.7.1.jar` 至 `xalan-2.7.2.jar`
   * `xercesImpl-2.9.1.jar` 至 `xercesImpl-2.12.0.jar`
   * `xml-apis-2.7.1.jar` 至 `xml-apis-2.7.2.jar`

1. 預設情況下，「啟動配置管理器」(Start Configuration Manager)複選框處於選中狀態。 按一下 **[!UICONTROL Done]**，執行 Configuration Manager。

1. 若要稍後執行 Configuration Manager，請取消選取 Start Configuration Manager 選項，再按一下 Done。以後可以使用中的相應指令碼啟動Configuration Manager `[AEM_forms_root]/configurationManager/bin` 的子菜單。

1. 根據您的應用程式伺服器，選擇以下文檔之一併按照 *配置和部署表AEM單* 的子菜單。

   * [安裝和部AEM署JBoss表單](http://www.adobe.com/go/learn_aemforms_installJBoss_65_tw)
   * [安裝和部AEM署WebSphere窗體](http://www.adobe.com/go/learn_aemforms_installWebSphere_65_tw)

1. （僅限JBoss）安裝修補程式並配置伺服器後，刪除JBoss應用程式伺服器的tmp和工作目錄。

>[!NOTE]
>啟動前 **配置管理器**，下載和替換 [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) 的子菜單。

## 部署後配置 {#post-deployment-configurations}

### SAML配置 {#saml-configurations}

如果配置了SAML身份驗證，並且遇到了大型IDP元資料的問題，請在安裝修補程式後執行以下操作：

1. 在應用程式伺服器中設定以下系統屬性：\
   `um.saml.enable.large.xml=true`
1. 重新啟動伺服器。
1. 刪除現有SAML驗證提供程式，並按SAML設定中所述為現有域重新添加它們。

## 受影響的模組 {#impacted-modules}

* 文件服務
* 文件安全性
* Foundation JEE

[聯繫支援](https://www.adobe.com/account/sign-in.supportportal.html)
