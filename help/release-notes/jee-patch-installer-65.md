---
title: AEM Forms JEE修補程式安裝程式
description: 瞭解如何使用AEM Forms JEE修補程式安裝程式來修正AEM 6.5 Forms元件中的問題。
content-type: reference
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
hide: true
hidefromtoc: true
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 17%

---

# AEM Forms JEE修補程式安裝程式 {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[請連絡支援人員](https://experienceleague.adobe.com/zh-hant?support-solution=General&support-tab=home#support)以取得詳細資訊或修補程式。

## 關於修補程式安裝程式 {#about-the-patch-installer}

AEM 6.5 Forms JEE修補程式安裝程式包含此修補程式發行前，AEM 6.5 Forms JEE所有可用元件出現的所有已修正問題。 如需已修正問題的完整清單，請參閱最新[Service Pack發行說明](release-notes.md)。

## 安裝修補程式的先決條件 {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## 安裝和設定修補程式 {#installing-and-configuring-the-patch}

1. 備份&lt;*AEM_forms_root*>/deploy資料夾。 如果決定解除安裝快速修正，則此為必要操作。
1. 停止應用程式伺服器。
1. 將修補程式安裝程式封存檔案解壓縮至硬碟。
1. 在根據您使用的作業系統命名的目錄中：

   * **Windows**
導覽至安裝媒體上的適當目錄，或硬碟上您複製安裝程式的資料夾，然後按兩下aemforms65_cfp_install.exe檔案。

      * （Windows 32位元） `Windows\Disk1\InstData\VM`
      * （Windows 64位元） `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
導覽至適當的目錄，然後在命令提示字元中輸入`./aem65_cfp_install.bin`。

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   這會啟動安裝精靈，引導您完成安裝。

1. 在 Introduction 面板上，按一下 **[!UICONTROL Next]**。
1. 在「**選擇安裝資料夾**」畫面上，確認顯示的預設位置對您現有的安裝而言是正確的，或按一下「**[!UICONTROL 瀏覽]**」以選取安裝AEM表單的替代資料夾，然後按一下「**[!UICONTROL 下一步]**」。
1. 閱讀 Quick Fix Patch Summary 資訊，然後按一下 **[!UICONTROL Next]**。
1. 閱讀 Pre-Installation Summary 資訊，然後按一下 **[!UICONTROL Install]**。
1. 安裝後，按一下 **[!UICONTROL Next]**，將快速修正更新套用至已安裝的檔案。

1. **[僅適用於Windows]：**&#x200B;執行下列動作：
   * 取消選取&#x200B;**Start Configuration Manager**&#x200B;選項，再按一下&#x200B;**[!UICONTROL 完成]**。 使用&#x200B;**中的** ConfigurationManager.bat **檔案執行** Configuration Manager`[aem-forms root]\configurationManager\bin`。

   * 或取消選取&#x200B;**Start Configuration Manager**&#x200B;選項，再按一下&#x200B;**[!UICONTROL 完成]**。 在使用&#x200B;**ConfigurationManager.exe**&#x200B;或&#x200B;**ConfigurationManager_IPv6.exe**&#x200B;執行&#x200B;**Configuration Manager**&#x200B;之前，請瀏覽至&#x200B;*`<AEMForms_Install_Dir>\configurationManager\bin`*&#x200B;目錄，並以最新的&#x200B;**ConfigurationManager.lax**&#x200B;和&#x200B;**ConfigurationManager_IPV6.lax**&#x200B;檔案取代[ConfigurationManager.lax](/help/assets/ConfigurationManager.lax)和[ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax)，搜尋並取代在這兩個檔案中具有&#x200B;**軸 — 1.4.1.1.jar**&#x200B;的&#x200B;**軸 — 1.4.1.2.jar**。

   >[!NOTE]
   >
   >使用&#x200B;**ConfigurationManager.bat**&#x200B;檔案可協助您避免手動更新.lax檔案的名稱。
   >

1. **[僅適用於Unix型]：**

   * 預設會選取&#x200B;**啟動組態管理員**&#x200B;核取方塊。 按一下&#x200B;**[!UICONTROL 完成]**&#x200B;立即執行Configuration Manager，或稍後執行&#x200B;**組態管理員**，取消選取&#x200B;**啟動組態管理員**&#x200B;選項，然後再按一下&#x200B;**[!UICONTROL 完成]**。 您可以使用&#x200B;**目錄中的適當指令碼，稍後再啟動**&#x200B;組態管理員`[AEM_forms_root]/configurationManager/bin`。

1. 視您的應用程式伺服器而定，選擇下列其中一份檔案，然後依照&#x200B;*設定和部署AEM表單*&#x200B;區段中的指示操作。

   * [安裝和部署JBoss適用的AEM表單®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_tw)
   * [安裝和部署AEM Forms for WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_tw)

1. (僅限JBoss®)安裝修補程式並設定伺服器後，刪除JBoss®應用程式伺服器的tmp和工作目錄。

## 部署後設定 {#post-deployment-configurations}

### SAML設定 {#saml-configurations}

如果您已設定SAML驗證，且面臨大型IDP中繼資料的問題，請在安裝修補程式後執行下列動作：

1. 在應用程式伺服器中設定下列系統屬性：\
   `um.saml.enable.large.xml=true`
1. 重新啟動伺服器。
1. 刪除現有的SAML驗證提供者，並按照SAML設定中的說明，為現有的網域再次新增它們。

>[!NOTE]
>
> 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式），可能會導致AEM開發環境不一致。

## 受影響的模組 {#impacted-modules}

* 文件服務
* 文件安全性
* Foundation JEE

[連絡支援](https://experienceleague.adobe.com/zh-hant?support-solution=General&support-tab=home#support)
