---
title: AEM Forms適用於AEM Forms的修補程式安裝指示
description: AEM Forms Service Pack安裝OSGi和JEE環境的指示
source-git-commit: a470627eb87735dd55edda93c3e2dac4a2c36752
workflow-type: tm+mt
source-wordcount: '1868'
ht-degree: 7%

---


# AEM 6.5 Forms Service Pack安裝指示 {#aem-form-patch-installation-instructions}

## 發行資訊

| 產品 | Adobe Experience Manager 6.5Forms |
|---|---|
| 版本 | 6.5.15.0 |
| 類型 | Service Pack發行 |
| 日期 | 2022 年 12 月 01 日 |
| 下載 URL | [最新AEM Forms版本](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) |

>[!NOTE]
>
>查看最新 [AEM Service Pack發行說明](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html#forms-6515) 以取得已修正問題的完整清單。

## Experience Manager Forms 6.5包含的內容

Adobe Experience Manager(AEM)Forms service pack包含新增和升級的功能，例如客戶要求的重要增強功能、效能、穩定性及安全性改善。 AEM Forms發行Service Pack會定期提供最新功能和改善項目。 根據您的堆疊，選擇以下路徑之一以在您的環境中下載並安裝Service Pack:

* [在JEE環境的AEM表單上下載和安裝Service Pack](#download-and-install-for-jee-service-pack)
* [在OSGi環境的AEM表單上下載和安裝Service Pack](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> Adobe會在每6個Service Pack後發行完整安裝程式。 JEE上的AEM 6.5 Forms Service Pack 12(6.5.12.0)是最後一個完整安裝程式。 完整安裝程式可支援新平台，而一般Service Pack安裝程式僅包含錯誤修正和一般改良。 若您要執行全新安裝或規劃以在JEE環境中使用AEM 6.5 Forms的最新軟體，Adobe建議在JEE上使用AEM 6.5.12.0 Forms的完整安裝程式，而非2019年4月08日發行的AEM 6.5 Forms安裝程式。 使用完整安裝程式後，安裝最新的Service Pack。

## 在JEE環境的AEM表單上下載和安裝Service Pack {#download-and-install-for-jee-service-pack}

![JEE安裝](/help/forms/using/assets/jeeinstallation.png)

+++1. 備份現有環境：

1. 備份 [CRX儲存庫、資料庫架構和GDS（全局文檔儲存）](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).
1. 備份&lt;*AEM_forms_root*>/部署資料夾。 如果您決定解除安裝Service Pack，則此為必要操作。

>[!NOTE]
>
> 在執行AEM Service Pack安裝程式之前，請確定您對AEM安裝目錄具有寫入存取權限。

+++

+++2.下載所需軟體：

* [AEM Forms on JEE 6.5.15.0 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/jee-patch-installer-65.html)
* [AEM 6.5.15.0 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fservicepack%2Faem-service-pkg-6.5.15.0.zip)
* [Forms 附加元件套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-forms-addon-2022.12.20.00-220900.zip)
* [片段Servlet](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

+++

+++3. 在JEE Service Pack上安裝AEM Forms :

1. 停止應用程式伺服器。
1. 擷取 **AEM Forms on JEE 6.5.15.0 Service Pack安裝程式封存** 到硬碟：

   * **Windows**
在複製安裝程式的硬碟上，導覽至安裝媒體或資料夾上的適當目錄，然後按兩下 
`aemforms65_cfp_install.exe` 檔案。

      * （Windows 32位元） `Windows\Disk1\InstData\VM`
      * （Windows 64位元） `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux®**
導航到相應的目錄，並從殼和類型導航 
`./aem65_cfp_install.bin`。

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   這會啟動安裝精靈，引導您完成安裝。

1. 在 Introduction 面板上，按一下 **[!UICONTROL Next]**。
1. 在 **選擇安裝資料夾** 螢幕上，驗證顯示的預設位置是否正確，或者按一下 **[!UICONTROL 瀏覽]** 要選擇安裝AEM表單的替代資料夾，請按一下 **[!UICONTROL 下一個]**.
1. 閱讀Service Pack摘要資訊，然後按一下 **[!UICONTROL 下一個]**.
1. 閱讀 Pre-Installation Summary 資訊，然後按一下 **[!UICONTROL Install]**。
1. 安裝後，按一下 **[!UICONTROL Next]**，將快速修正更新套用至已安裝的檔案。
1. **[僅適用於Windows]:** 執行下列步驟之一：

   * 取消選取 **啟動Configuration Manager** 選項 **[!UICONTROL 完成]**. 執行 **Configuration Manager** 使用 **ConfigurationManager.bat** 位於 `[aem-forms root]\configurationManager\bin`.

   * 或取消選取 **啟動Configuration Manager** 選項 **[!UICONTROL 完成]**. 執行前 **Configuration Manager** 使用 **ConfigurationManager.exe** 或 **ConfigurationManager_IPv6.exe**，導覽至 *`<AEMForms_Install_Dir>\configurationManager\bin`* 目錄和替換 [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) 和 [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) 檔案。

      >[!NOTE]
      >
      > 使用 **ConfigurationManager.bat** 檔案可幫助您避免手動更新.lax檔案的名稱。

1. **[僅基於Unix]:** 此 **啟動Configuration Manager** 複選框。 按一下 **[!UICONTROL 完成]** 以立即運行Configuration Manager或運行 **Configuration Manager** 稍後，取消選取 **啟動Configuration Manager** 選項 **[!UICONTROL 完成]**. 您可以開始 **Configuration Manager** 稍後在 `[AEM_forms_root]/configurationManager/bin` 目錄。

   執行 **Configuration Manager**:
   * 配置CRX
   * 部署Adobe Experience Manager Forms EAR
   * 初始化Adobe Experience Manager Forms資料庫
   * 部署Adobe Experience Manager Forms元件
   * 部署並驗證DSC jar。

1. 根據您的應用程式伺服器，選擇以下文檔之一，然後按照 *設定和部署AEM表單* 區段。

   * [安裝和部署適用於JBoss®的AEM表單](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [安裝和部署AEM forms for WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)
   * [安裝和部署AEM Forms for WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65)

>[!NOTE]
>
> 在JEE Service Pack上安裝AEM Forms後，您需要從 `crx-repository\install` 資料夾，再重新啟動appserver。 從下載最新的Forms附加元件套件 [Software Distribution入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

+++

+++4. 安裝Servlet片段

必須安裝 **servlet片段** 對於除運行在JBoss® EAP 7.4.0上的應用程式伺服器以外的所有應用程式伺服器。要下載和安裝servlet片段，請執行以下操作：

1. 如果您尚未下載片段，請從下載 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

1. 啟動應用程式伺服器，等待日誌穩定並檢查捆綁狀態。

1. 開啟Web控制台套件組合。 預設URL為 `http://[Server]:[Port]/system/console/bundles`.

1. 按一下「安裝/更新」。 選擇下載的片段， `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. 按一下 **安裝** 或 **更新**. 等待應用程式伺服器穩定

1. 停止應用程式伺服器。

+++

+++5. 安裝 AEM Service Pack

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請先重新啟動執行個體再進行安裝。 Adobe建議，如果執行個體的目前正常運行時間很長，則重新啟動。
1. 安裝之前，請拍攝快照或對 [!DNL Experience Manager] 例項。
1. 從下載Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->
1. 開啟「套件管理器」，然後選取 **[!UICONTROL 上傳套件]** 上傳套件。 要了解更多資訊，請參閱 [封裝管理員](/help/sites-administering/package-manager.md).
1. 選取套件，然後選取 **[!UICONTROL 安裝]**.
1. 若要更新S3連接器，請在安裝Service Pack後停止執行個體，以安裝資料夾中提供的新二進位檔案取代現有連接器，然後重新啟動執行個體。 請參閱 [Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

**自動安裝**

您可以使用兩種不同的方法來自動安裝 [!DNL ExperienceManager] 6.5.15.0。<!--       UPDATE FOR EACH NEW RELEASE -->

* 將包裝放入 `../crx-quickstart/install` 資料夾。
程式包會自動安裝。

* 使用 [來自套件管理器的HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html). 使用  `cmd=install&recursive=true` 以便安裝嵌套包。

   >[!NOTE]
   >
   >Experience Manager6.5.15.0不支援Bootstrap安裝。 <!-- UPDATE FOR EACHNEW RELEASE -->

**驗證安裝**

若要了解經認證可與此版本搭配使用的平台，請參閱 [技術要求](/help/sites-deploying/technical-requirements.md).

1. 產品資訊頁面(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience      Manager (6.5.15.0)` 在 [!UICONTROL 已安裝的產品].<!-- UPDATE FOR EACH NEW RELEASE -->
1. 所有OSGi套件組合 **[!UICONTROL 活動]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。
1. OSGi捆綁 `org.apache.jackrabbit.oak-core` 為1.22.13版或更新版本(使用WebConsole: `/system/console/     bundles`)。

+++

+++6. 安裝AEM Experience Manager Forms附加元件套件

1. 確認您已安裝 [!DNL Experience Manager] 服務包。
1. 下載適用於您作業系統的 [AEM Forms 發行版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#forms-updates)所列出的對應 Forms 附加套件。
1. 依照 [安裝AEM Forms附加元件套件](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi.html?lang=en#install-aem-forms-add-on-package).
1. 若您在Experience Manager6.5 Forms中使用信函，請安裝 [最新AEMFD相容性套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++


<!-- 1. (JBoss only) After installing the patch and configuring the server, delete  tmp  and work directories of JBoss application server.

>[!IMPORTANT]
>
>Before installing [AEM 6.5.15.0 service pack](#install-the-aem-service-pack-install-aem-service-pack), for all the AEM Forms on JEE environments using any application servers other than JBoss EAP 7.4.0: 
> * Install  the [org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) servlet fragment and wait for the application server to stabilize.
>* If you install the latest [AEM service pack (6.5.15.0)](#install-the-aem-service-pack-install-aem-service-pack), prior to the fragment servlet `org.apache.felix.http.servlet-api-1.2.0_fragment-full.jar` on JEE environment, the CRX/bundle and the start page show service unavailable errors, [click here](/help/forms/using/aem-service-pack-installation-solution.md) to know the troubleshooting steps. 

### !-->


## 在OSGi環境的AEM表單上下載和安裝Service Pack {#download-and-install-for-osgi-service-pack}

![OSGi安裝步驟](/help/forms/using/assets/osgiinstallation.png)


+++1. 備份現有環境：

1. 備份 [CRX儲存庫和資料庫架構](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).

>[!NOTE]
>
> 如果安裝關係資料庫的AEM Forms Service Pack，則必須備份DB_schema。

+++

+++2.下載所需軟體：

* [AEM 6.5.15.0 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fservicepack%2Faem-service-pkg-6.5.15.0.zip)
* [Forms 附加元件套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-forms-addon-2022.12.20.00-220900.zip)

+++

+++3. 安裝 AEM Service Pack

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請先重新啟動執行個體再進行安裝。 Adobe建議，如果執行個體的目前正常運行時間很長，則重新啟動。
1. 安裝之前，請拍攝快照或對 [!DNL Experience Manager] 例項。
1. 從下載Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->
1. 開啟「套件管理器」，然後選取 **[!UICONTROL 上傳套件]** 上傳套件。 要了解更多資訊，請參閱 [封裝管理員](/help/sites-administering/package-manager.md).
1. 選取套件，然後選取 **[!UICONTROL 安裝]**.
1. 若要更新S3連接器，請在安裝Service Pack後停止執行個體，以安裝資料夾中提供的新二進位檔案取代現有連接器，然後重新啟動執行個體。 請參閱 [Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

**自動安裝**

您可以使用兩種不同的方法來自動安裝 [!DNL Experience Manager] 6.5.15.0。<!--       UPDATE FOR EACH NEW RELEASE -->

* 將包裝放入 `../crx-quickstart/install` 資料夾。 程式包會自動安裝。
* 使用 [來自套件管理器的HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html). 使用 `cmd=install&recursive=true` 以便安裝嵌套包。

   >[!NOTE]
   >
   >Experience Manager6.5.15.0不支援Bootstrap安裝。 <!-- UPDATE FOR EACH NEW RELEASE -->

**驗證安裝**

若要了解經認證可與此版本搭配使用的平台，請參閱 [技術要求](/help/sites-deploying/technical-requirements.md).

1. 產品資訊頁面(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience      Manager (6.5.15.0)` 在 [!UICONTROL 已安裝的產品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi套件組合 **[!UICONTROL 活動]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

   1. OSGi捆綁 `org.apache.jackrabbit.oak-core` 為1.22.13版或更新版本(使用Web控制台： `/system/console/bundles`)。

+++

+++4. 安裝AEM Experience Manager Forms附加元件套件

1. 確認您已安裝 [!DNL Experience Manager] 服務包。
1. 下載適用於您作業系統的 [AEM Forms 發行版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#forms-updates)所列出的對應 Forms 附加套件。
1. 依照 [安裝AEM Forms附加元件套件](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi.html?lang=en#install-aem-forms-add-on-package).
1. 若您在Experience Manager6.5 Forms中使用信函，請安裝 [最新AEMFD相容性套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## 疑難排解

* 如果AEM Forms Service Pack安裝期間發生錯誤，請重新安裝。 如果問題仍然存在，請聯絡產品團隊。

* 若 **套件管理器UI上的對話方塊** 在安裝Service Pack期間退出，請等待錯誤記錄穩定，再存取部署。 請等待與卸載更新程式捆綁相關的特定日誌，然後確保安裝成功。 此問題通常會在Safari瀏覽器中發生，但可能在任何瀏覽器上間歇性發生。

* 安裝完成後，檢查監視器記錄(error.log)以查看任何活動。 等候幾分鐘，直到記錄中沒有任何活動。 重新啟動AEM執行個體。

* 萬一你 **服務不可用錯誤** 安裝最新的AEM Forms 6.5.15.0 service pack後， [安裝servlet片段和套件組合](/help/forms/using/aem-service-pack-installation-solution.md) 來修正錯誤。


