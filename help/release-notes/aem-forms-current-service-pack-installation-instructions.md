---
title: AEM FormsAEM Forms補丁程式安裝說明
description: AEM FormsService Pack安裝OSGi和JEE環境說明
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: 01bf12ec46966ab2c78e2e825840230ea1bd3395
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 8%

---

# AEM 6.5FormsService Pack安裝說明 {#aem-form-patch-installation-instructions}

## 發行資訊

| 產品 | Adobe Experience Manager6.5Forms |
|---|---|
| 版本 | 6.5.16.0 |
| 類型 | Service Pack版本 |
| 日期 | 2023年3月2日 |
| 下載 URL | [最新AEM Forms發佈](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) |

>[!NOTE]
>
>查看最新 [《 AEM Service Pack發行說明》](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html) 清單。

## Experience Manager Forms六點五包含的內容

Adobe Experience Manager(AEM)Forms服務包包括新的和升級的功能，如客戶要求的關鍵增強功能、效能、穩定性和安全性改進。 AEM Forms定期發佈服務包，以提供最新功能和改進。 根據您的堆棧，選擇以下路徑之一以在您的環境中下載並安裝Service Pack:

* [在JEE環境的表單上AEM下載和安裝Service Pack](#download-and-install-for-jee-service-pack)
* [在OSGi環境的表單AEM上下載並安裝Service Pack](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> Adobe每第6個Service Pack發佈一個完整安裝程式。 AEM JEE上的6.5FormsService Pack 12(6.5.12.0)是最後一個完整安裝程式。 完整安裝程式為新平台提供支援，而常規Service Pack安裝程式包含新功能、修復錯誤和一般改進。 如果您正在執行全新安裝或計畫在JEE環境中為AEM6.5Forms使用最新軟體，Adobe建議在2022年3月3日發佈的JEE完整安裝程式上使用AEM6.5.12.0Forms，而不是在2019年4月8日發佈的AEM6.5Forms安裝程式。 使用完整安裝程式後，請安裝最新的Service Pack。

## 在JEE環境的表單上AEM下載和安裝Service Pack {#download-and-install-for-jee-service-pack}

![JEE安裝](/help/forms/using/assets/jeeinstallation.png)

+++1. 備份您的現有環境：

1. 備份 [CRX儲存庫、資料庫架構和GDS（全局文檔儲存）](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html)。
1. 備份&lt;*AEM_表單_根*>/deploy資料夾。

>[!NOTE]
>
> 運行Service AEM Pack安裝程式之前，請確保您對安裝目錄具有寫訪問AEM權限。

+++

+++2.下載所需軟體：

* [AEM FormsJEE Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
* [Forms 附加元件套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [片段Servlet](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

+++

+++3. 在JEE Service Pack上安裝AEM Forms:

1. 停止應用程式伺服器。
1. 提取 **AEM FormsJEE Service Pack安裝程式存檔** 到硬碟：

   * **窗口**
導航至硬碟上安裝介質或資料夾中相應的目錄，然後按兩下 
`aemforms65_cfp_install.exe` 的子菜單。

      * （Windows 32位） `Windows\Disk1\InstData\VM`
      * （Windows 64位） `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux®**
導航到相應的目錄，並從shell和類型 
`./aem65_cfp_install.bin`。

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   這會啟動安裝精靈，引導您完成安裝。

1. 在 Introduction 面板上，按一下 **[!UICONTROL Next]**。
1. 在 **選擇安裝資料夾** 螢幕中，驗證顯示的預設位置是否正確，或者按一下 **[!UICONTROL 瀏覽]** 選擇安裝表單的備AEM用資料夾，然後按一下 **[!UICONTROL 下一個]**。
1. 閱讀Service Pack摘要資訊，然後按一下 **[!UICONTROL 下一個]**。
1. 閱讀 Pre-Installation Summary 資訊，然後按一下 **[!UICONTROL Install]**。
1. 安裝後，按一下 **[!UICONTROL Next]**，將快速修正更新套用至已安裝的檔案。
1. **[僅適用於Windows]:** 執行以下步驟之一：

   * 取消選擇 **啟動Configuration Manager** 選項 **[!UICONTROL 完成]**。 運行 **配置管理器** 使用 **ConfigurationManager.bat** 檔案位於 `[aem-forms root]\configurationManager\bin`。

   * 或取消選擇 **啟動Configuration Manager** 選項 **[!UICONTROL 完成]**。 運行前 **配置管理器** 使用 **ConfigurationManager.exe** 或 **ConfigurationManager_IPv6.exe**，導航 *`<AEMForms_Install_Dir>\configurationManager\bin`* 目錄和替換 [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) 和 [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) 的子菜單。

      >[!NOTE]
      >
      >* 更新或替換 **ConfigurationManager.bat** 檔案可幫助您避免手動更新.lax檔案。


1. **[僅適用於基於Unix]:** 的 **啟動Configuration Manager** 複選框。 按一下 **[!UICONTROL 完成]** 即時運行Configuration Manager或運行 **配置管理器** 稍後，取消選擇 **啟動Configuration Manager** 選項 **[!UICONTROL 完成]**。 你可以開始 **配置管理器** 稍後使用 `[AEM_forms_root]/configurationManager/bin` 的子菜單。

1. 根據您的應用程式伺服器，選擇以下文檔之一併按照 *配置和部署表AEM單* 的子菜單。

   * [安裝和部AEM署JBoss®表單](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [安裝和部AEM署WebSphere®表單](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)
   * [安裝和部署用於WebLogic的AEM Forms](https://www.adobe.com/go/learn_aemforms_installWebLogic_65)
   * [為JBoss®群AEM集安裝和部署表單](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [安裝和部AEM署WebSphere®群集的表單](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [安裝和部署用於WebLogic群集的AEM Forms](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
> 在JEE Service Pack上安裝AEM Forms後，您需要從中刪除Forms附加軟體包 `crx-repository\install` 資料夾。 從下載最新的Forms載入項包 [軟體分發門戶](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。

+++

+++4. 安裝Servlet片段

>[!NOTE]
>
> * 以防您從 **AEM Service Pack 6.5.15.0**，無需安裝 **Servlet片段**。 如果您從早於 **AEM Service Pack 6.5.15.0**，必須安裝 **Servlet片段**。
> * 必須安裝 **Servlet片段** 除運行於 **JBoss® EAP 7.4.0**。



要下載並安裝Servlet片段：

1. 如果尚未下載該片段，請從 [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)。

1. 啟動應用程式伺服器，等待日誌穩定並檢查捆綁狀態。

1. 開啟Web控制台捆綁包。 預設URL為 `http://[Server]:[Port]/system/console/bundles`。

1. 按一下「Install/Update（安裝/更新）」。 選擇下載的片段， `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`。 按一下 **安裝** 或 **更新**。 等待應用程式伺服器穩定

1. 停止應用程式伺服器。

+++

+++5. 安裝 AEM Service Pack

1. 如果實例處於更新模式（當實例從早期版本更新時），請在安裝前重新啟動該實例。 Adobe建議在實例的當前正常運行時間較長時重新啟動。
1. 在安裝之前，請拍攝快照或新備份 [!DNL Experience Manager] 實例。
1. 從下載Service Pack [軟體分發](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。 <!-- UPDATE FOR EACH NEW RELEASE -->
1. 開啟包管理器，然後選擇 **[!UICONTROL 上載包]** 上載包。 要瞭解更多資訊，請參閱 [包管理器](/help/sites-administering/package-manager.md)。
1. 選擇包，然後選擇 **[!UICONTROL 安裝]**。

**自動安裝**

有兩種方法可用於自動安裝 [!DNL ExperienceManager] 服務包。<!--       UPDATE FOR EACH NEW RELEASE -->

* 將包放入 `../crx-quickstart/install` 資料夾。
軟體包將自動安裝。

* 使用 [包管理器中的HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)。 使用  `cmd=install&recursive=true` 以便安裝嵌套的軟體包。

   >[!NOTE]
   Experience Manager服務包不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

   **驗證安裝**

   要瞭解經認證可與此版本配合使用的平台，請參閱 [技術要求](/help/sites-deploying/technical-requirements.md)。

   1. 產品資訊頁面(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (spversion)` 在 [!UICONTROL 已安裝的產品]。<!-- UPDATE FOR EACH NEW RELEASE -->
   1. 所有OSGi捆綁包 **[!UICONTROL 活動]** 或 **[!UICONTROL 片段]** 在OSGi控制台(使用Web控制台： `/system/console/bundles`)。
   1. OSGi捆綁 `org.apache.jackrabbit.oak-core` 版本1.22.14或更高版本(使用WebConsole: `/system/console/     bundles`)。

+++

+++6. 安AEM裝Experience Manager Forms載入項包

1. 確保已安裝 [!DNL Experience Manager] 服務包。
1. 下載適用於您作業系統的 [AEM Forms 發行版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)所列出的對應 Forms 附加套件。
1. 按中所述安裝Forms附加程式包 [安裝AEM Forms附加軟體包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。
1. 如果在Forms6.5Experience Manager中使用字母，請安裝 [最新的AEMFD相容性包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。

+++

## 在OSGi環境的表單AEM上下載並安裝Service Pack {#download-and-install-for-osgi-service-pack}

![OSGi安裝步驟](/help/forms/using/assets/osgiinstallation.png)


+++1. 備份您的現有環境：

1. 備份 [CRX儲存庫和資料庫架構](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html)。

>[!NOTE]
如果為關係資料庫安裝AEM Forms服務包，則必須備份DB_schema。

+++

+++2.下載所需軟體：

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html)
* [Forms 附加元件套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)

+++

+++3. 安裝 AEM Service Pack

1. 如果實例處於更新模式（當實例從早期版本更新時），請在安裝前重新啟動該實例。 Adobe建議在實例的當前正常運行時間較長時重新啟動。
1. 在安裝之前，請拍攝快照或新備份 [!DNL Experience Manager] 實例。
1. 從下載Service Pack [軟體分發](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。 <!-- UPDATE FOR EACH NEW RELEASE -->
1. 開啟包管理器，然後選擇 **[!UICONTROL 上載包]** 上載包。 要瞭解更多資訊，請參閱 [包管理器](/help/sites-administering/package-manager.md)。
1. 選擇包，然後選擇 **[!UICONTROL 安裝]**。

**自動安裝**

有兩種方法可用於自動安裝 [!DNL Experience Manager] 服務包。<!--  UPDATE FOR EACH NEW RELEASE -->

* 將包放入 `../crx-quickstart/install` 資料夾。 軟體包將自動安裝。
* 使用 [包管理器中的HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)。 使用 `cmd=install&recursive=true` 以便安裝嵌套的軟體包。

   >[!NOTE]
   Experience Manager服務包不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

   **驗證安裝**

   要瞭解經認證可與此版本配合使用的平台，請參閱 [技術要求](/help/sites-deploying/technical-requirements.md)。

   1. 產品資訊頁面(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (spversion)` 在 [!UICONTROL 已安裝的產品]。 <!-- UPDATE FOR EACH NEW RELEASE -->

   1. 所有OSGi捆綁包 **[!UICONTROL 活動]** 或 **[!UICONTROL 片段]** 在OSGi控制台(使用Web控制台： `/system/console/bundles`)。

      1. OSGi捆綁 `org.apache.jackrabbit.oak-core` 版本1.22.14或更高版本(使用Web控制台： `/system/console/bundles`)。

+++

+++4. 安AEM裝Experience Manager Forms載入項包

1. 確保已安裝 [!DNL Experience Manager] 服務包。
1. 下載適用於您作業系統的 [AEM Forms 發行版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)所列出的對應 Forms 附加套件。
1. 按中所述安裝Forms附加程式包 [安裝AEM Forms附加軟體包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。
1. 如果在Forms6.5Experience Manager中使用字母，請安裝 [最新的AEMFD相容性包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。

+++

## 疑難排解

* 如果 **包管理器UI上的對話框** 在安裝Service Pack期間退出，等待錯誤日誌穩定後再訪問部署。 請等待與卸載更新程式包相關的特定日誌，然後確保安裝成功。 通常，此問題在Safari瀏覽器中發生，但在任何瀏覽器上都可能間歇性地發生。

* 安裝完成後，檢查任何活動的監視器日誌(error.log)。 等待幾分鐘，直到日誌中沒有活動。 重新啟動AEM實例。

* 以防你 **服務不可用錯誤** 安裝AEM Forms6.5.15.0服務包後， [安裝servlet片段和捆綁包](/help/forms/using/aem-service-pack-installation-solution.md) 來修復錯誤。
