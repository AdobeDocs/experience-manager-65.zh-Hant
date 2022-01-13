---
title: AEM Forms JEE修補程式安裝程式
description: AEM Forms JEE修補程式安裝程式
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 29%

---

# AEM Forms JEE修補程式安裝程式 {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[聯絡支援](https://www.adobe.com/tw/account/sign-in.supportportal.html) 以獲取更多資訊或獲取修補程式。

## 關於修補程式安裝程式 {#about-the-patch-installer}

AEM 6.5 Forms JEE修補程式安裝程式包含在此修補程式發行前，AEM 6.5 Forms JEE所有元件的所有已修正問題。 查看最新  [Service Pack發行說明](release-notes.md) 以取得已修正問題的完整清單。

## 安裝修補程式的必要條件 {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## 安裝和配置修補程式 {#installing-and-configuring-the-patch}

1. 備份&lt;*AEM_forms_root*>/部署資料夾。 如果決定解除安裝快速修正，則此為必要操作。
1. 停止應用程式伺服器。
1. 將修補程式安裝程式封存檔案解壓縮至硬碟。
1. 在根據您使用的作業系統命名的目錄中：

   * **Windows**
導覽至硬碟上複製安裝程式之安裝媒體或資料夾的適當目錄，然後按兩下aemforms65_cfp_install.exe檔案。

      * （Windows 32位元） `Windows\Disk1\InstData\VM`
      * （Windows 64位元） `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux**
導覽至適當的目錄，然後在命令提示字元中輸入 
`./aem65_cfp_install.bin`。

      * (Linux) `Linux/Disk1/InstData/NoVM`

   這會啟動安裝精靈，引導您完成安裝。

1. 在 Introduction 面板上，按一下 **[!UICONTROL Next]**。
1. 在「選擇安裝資料夾」螢幕上，驗證針對現有安裝顯示的預設位置是否正確，或按一下 **[!UICONTROL 瀏覽]** 要選擇安裝AEM表單的替代資料夾，請按一下 **[!UICONTROL 下一個]**.
1. 閱讀 Quick Fix Patch Summary 資訊，然後按一下 **[!UICONTROL Next]**。
1. 閱讀 Pre-Installation Summary 資訊，然後按一下 **[!UICONTROL Install]**。
1. 安裝後，按一下 **[!UICONTROL Next]**，將快速修正更新套用至已安裝的檔案。

1. 在按一下「完成」之前，取消選擇「啟動配置管理器」選項。 在運行配置管理器之前，使用 **ConfigurationManager.exe** 或 **ConfigurationManager_IPv6.exe**，導覽至 *&lt;aemforms_install_dir>\configurationManager\bin* 目錄和更新 `ConfigurationManager.lax` 和 `ConfigurationManager_IPv6.lax` 具有以下更名操作的檔案：

   * `axis.jar` 至 `axis-1.4.1.1.jar`
   * `serializer-2.7.1.jar` 至 `serializer-2.7.2.jar`
   * `xalan-2.7.1.jar` 至 `xalan-2.7.2.jar`
   * `xercesImpl-2.9.1.jar` 至 `xercesImpl-2.12.0.jar`
   * `xml-apis-2.7.1.jar` 至 `xml-apis-2.7.2.jar`

1. 預設會選取「啟動設定管理器」核取方塊。 按一下 **[!UICONTROL Done]**，執行 Configuration Manager。

1. 若要稍後執行 Configuration Manager，請取消選取 Start Configuration Manager 選項，再按一下 Done。您稍後可以使用 `[AEM_forms_root]/configurationManager/bin` 目錄。

1. 根據您的應用程式伺服器，選擇以下文檔之一，然後按照 *設定和部署AEM表單* 區段。

   * [安裝和部署適用於JBoss的AEM表單](http://www.adobe.com/go/learn_aemforms_installJBoss_65_tw)
   * [安裝和部署AEM forms for WebSphere](http://www.adobe.com/go/learn_aemforms_installWebSphere_65_tw)

1. （僅限JBoss）安裝修補程式並配置伺服器後，刪除JBoss應用程式伺服器的tmp和工作目錄。

## 部署後配置 {#post-deployment-configurations}

### SAML設定 {#saml-configurations}

如果您已設定SAML驗證，且遇到大型IDP中繼資料的問題，安裝修補程式後請執行下列作業：

1. 在應用程式伺服器中設定以下系統屬性：\
   `um.saml.enable.large.xml=true`
1. 重新啟動伺服器。
1. 刪除現有的SAML驗證提供者，並如SAML設定所述，為現有網域再次新增這些提供者。

## 受影響的模組 {#impacted-modules}

* 文件服務
* 文件安全性
* Foundation JEE

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
