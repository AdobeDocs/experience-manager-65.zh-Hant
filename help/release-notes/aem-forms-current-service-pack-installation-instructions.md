---
title: 適用於AEM Forms的AEM Forms修補程式安裝指示
description: 適用於OSGi和JEE環境的AEM Forms Service Pack安裝指示
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: ffa882ed69098bcacb7df04fa0cff69df3a3097f
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 6%

---

# AEM 6.5 Forms Service Pack安裝指示 {#aem-form-patch-installation-instructions}

## 發行資訊

| 產品 | Adobe Experience Manager 6.5 Forms |
|---|---|
| 版本 | 6.5.22.0 |
| 類型 | Service Pack發行 |
| 日期 | 2024 年 11 月 29 日 |
| 下載 URL | [最新AEM Forms版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant) |

>[!NOTE]
>
>如需已修正問題的完整清單，請參閱最新[AEM Service Pack發行說明](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=zh-Hant)。

## Experience Manager Forms 6.5包含的內容

Adobe Experience Manager (AEM) Forms service pack包含新功能和升級功能，例如客戶要求的重要增強功能、效能、穩定性和安全性改善專案。 AEM Forms會定期發行Service Pack，提供最新功能和改進專案。 根據您的技術棧疊，選擇下列其中一個路徑，以下載並在您的環境中安裝Service Pack：

* [在JEE環境的AEM表單上下載並安裝Service Pack](#download-and-install-for-jee-service-pack)
* [在OSGi環境上的AEM表單上下載並安裝Service Pack](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> * Adobe會每六個Service Pack發行完整安裝程式。 AEM 6.5 Forms Service Pack 18 (6.5.18.0)是最新的JEE完整安裝程式。 完整版安裝程式支援新平台，而一般Service Pack安裝程式則包含新功能、錯誤修正和一般改善。 如果您在JEE環境中執行全新安裝或計畫使用適用於您的AEM 6.5 Forms的最新軟體，Adobe建議使用2023年8月31日發行的AEM 6.5.18.0 Forms on JEE完整安裝程式，而非2019年4月8日發行的AEM 6.5 Forms安裝程式或2022年3月3日發行的AEM 6.5.12.0 Forms安裝程式。 使用完整安裝程式後，請安裝最新的Service Pack。
> * [AEM 6.5 QuickStart](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=zh-Hant)中提供的AEM Forms功能(例如最適化Forms)僅供探索和評估之用。 若要用於生產，必須獲得 AEM Forms 有效授權。

<!--

## Prerequisites {#prerequisites}

From AEM Service Pack 6.5.19.0 and onwards, XMLFM (XML output) will be available in 64-bit only, therefore you require the latest [Microsoft Visual C++ Redistributable (2015-2022) 64-bit](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) to be installed on Windows Server prior to JEE or OSGi installation.

>[!NOTE]
> This prerequisite is required in addition to the already existing Microsoft Visual C++ Redistributable 32-bit.

-->

## 在JEE環境的AEM表單上下載並安裝Service Pack {#download-and-install-for-jee-service-pack}

<!--
![JEE Installation](/help/forms/using/assets/jeeinstallation.png) -->

+++1. 備份您的現有環境

1. 備份您的[CRX存放庫、資料庫結構描述和GDS （全域檔案儲存）](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html?lang=zh-Hant)。
1. 備份&lt;*AEM_forms_root*>/deploy資料夾。

>[!NOTE]
>
> 在執行AEM Service Pack安裝程式之前，請確定您擁有AEM安裝目錄的寫入許可權。

+++

+++2. 下載必要的軟體

* JEE Service Pack上的[AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)

* [片段Servlet](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=zh-Hant)
* [Forms附加元件套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)


+++

+++3. 安裝Microsoft Visual C++可轉散發套件

* 在安裝Microsoft 6.5 Forms的電腦上，下載並安裝適用於Visual Studio 2015、2017、2019和2022[&#128279;](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022)的64位元版AEM Visual C++可轉散發套件。

>[!NOTE]
>
> 請確定您安裝了可轉散發套件（即使已安裝舊版），以確保最新版本的可用性。

+++

+++4. 在JEE Service Pack上安裝AEM Forms：

1. 停止應用程式伺服器。
1. 將JEE Service Pack安裝程式封存&#x200B;**上的** AEM Forms解壓縮至硬碟：

   * **Windows**
導覽至安裝媒體上的適當目錄，或您硬碟上您所複製的資料夾     安裝程式，然後按兩下`aemforms65_cfp_install.exe`檔案。

      * （Windows 32位元） `Windows\Disk1\InstData\VM`
      * （Windows 64位元） `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
導覽至適當的目錄，並從Shell和型別`./aem65_cfp_install.bin`。

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   這會啟動安裝精靈，引導您完成安裝。

1. 在 Introduction 面板上，按一下 **[!UICONTROL Next]**。
1. 在「**選擇安裝資料夾**」畫面上，確認顯示的預設位置對您現有的安裝而言是正確的，或按一下「**[!UICONTROL 瀏覽]**」以選取安裝AEM表單的替代資料夾，然後按一下「**[!UICONTROL 下一步]**」。
1. 閱讀Service Pack摘要資訊，然後按一下&#x200B;**[!UICONTROL 下一步]**。
1. 閱讀 Pre-Installation Summary 資訊，然後按一下 **[!UICONTROL Install]**。
1. 安裝後，按一下 **[!UICONTROL Next]**，將快速修正更新套用至已安裝的檔案。
1. **[僅適用於Windows]：**&#x200B;執行下列其中一個步驟：

   * 取消選取&#x200B;**Start Configuration Manager**&#x200B;選項，再按一下&#x200B;**[!UICONTROL 完成]**。 使用`[aem-forms root]\configurationManager\bin`中的&#x200B;**ConfigurationManager.bat**&#x200B;檔案執行&#x200B;**Configuration Manager**。

   * 或取消選取&#x200B;**Start Configuration Manager**&#x200B;選項，再按一下&#x200B;**[!UICONTROL 完成]**。 在使用&#x200B;**ConfigurationManager.exe**&#x200B;或&#x200B;**ConfigurationManager_IPv6.exe**&#x200B;執行&#x200B;**Configuration Manager**&#x200B;之前，請瀏覽至&#x200B;*`<AEMForms_Install_Dir>\configurationManager\bin`*&#x200B;目錄，並以最新的[ConfigurationManager.lax](/help/assets/ConfigurationManager.lax)和[ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax)檔案取代&#x200B;**ConfigurationManager.lax**&#x200B;和&#x200B;**ConfigurationManager_IPV6.lax**，搜尋並取代在這兩個檔案中具有&#x200B;**軸 — 1.4.1.2.jar**&#x200B;的&#x200B;**軸 — 1.4.1.1.jar**。

     >[!NOTE]
     >
     >* 更新或取代&#x200B;**ConfigurationManager.bat**&#x200B;檔案可協助您避免手動更新.lax檔案。

1. **[僅適用於Unix]：**&#x200B;預設會選取&#x200B;**啟動組態管理員**&#x200B;核取方塊。 按一下&#x200B;**[!UICONTROL 完成]**&#x200B;立即執行Configuration Manager，或稍後執行&#x200B;**組態管理員**，取消選取&#x200B;**啟動組態管理員**&#x200B;選項，然後再按一下&#x200B;**[!UICONTROL 完成]**。 您可以使用`[AEM_forms_root]/configurationManager/bin`目錄中的適當指令碼，稍後再啟動&#x200B;**組態管理員**。

1. 視您的應用程式伺服器而定，選擇下列其中一份檔案，然後依照&#x200B;*設定和部署AEM表單*&#x200B;區段中的指示操作。

   * [安裝和部署JBoss適用的AEM表單®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_tw)
   * [安裝和部署AEM Forms for WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_tw)
   * [安裝和部署AEM Forms for WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65_tw)
   * [安裝和部署JBoss®叢集適用的AEM表單](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [安裝和部署AEM Forms for WebSphere®叢集](https://helpx.adobe.com/tw/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [安裝和部署WebLogic叢集的AEM Forms](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
>* 在JEE Service Pack上安裝AEM Forms後，您必須先從`crx-repository\install`資料夾中移除Forms附加元件套件，才能重新啟動Appserver。 從[軟體發佈入口網站](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)下載最新的Forms附加元件套件。
>* 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式），可能會導致AEM開發環境不一致。
>* 針對[用於緩解JEE](/help/release-notes/aem-forms-hotfix.md)上AEM Forms之Spring Framework弱點的Hotfix。在叢集環境中部署時，必須確保定位器是使用JDK 17開始的。

+++

+++5. 如果未安裝，請安裝servlet片段（**必要步驟**）

<!-- >[!NOTE] > > * If you are upgrading from **AEM Service Pack 6.5.15.0**, the installation of the **servlet fragment** is not required. For versions **AEM Service Pack 6.5.14.0** or earlier, it is **mandatory to install** the servlet fragment. -->

若要下載並安裝servlet片段：

1. 如果您尚未下載片段，請從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)下載。

2. 啟動應用程式伺服器，等待記錄檔穩定並檢查套件組合狀態。

3. 開啟Web控制檯套件組合。 預設URL為`http://[Server]:[Port]/system/console/bundles`。

4. 按一下「安裝/更新」。 選擇下載的片段`org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`。 按一下&#x200B;**安裝**&#x200B;或&#x200B;**更新**。 等待應用程式伺服器穩定下來

5. 停止應用程式伺服器。

+++

+++6. 安裝AEM Service Pack

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請在安裝前重新啟動執行個體。 如果執行個體的目前運作時間很高，Adobe建議重新啟動。
1. 安裝之前，請為您的[!DNL Experience Manager]執行個體建立快照或全新備份。
1. 從[軟體發佈](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)下載Service Pack。<!-- UPDATE FOR EACH NEW RELEASE -->
1. 開啟封裝管理員，然後選取&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。 如需詳細資訊，請參閱[封裝管理員](/help/sites-administering/package-manager.md)。
1. 選取封裝，然後選取&#x200B;**[!UICONTROL 安裝]**。

**自動安裝**

您可以使用兩種不同的方法來自動安裝[!DNL ExperienceManager] Service Pack。<!--       UPDATE FOR EACH NEW RELEASE -->

* 伺服器上線時，請將封裝放入`../crx-quickstart/install`資料夾。
此封裝為      已自動安裝。

* 使用封裝管理員[&#128279;](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant)的HTTP API。 使用`cmd=install&recursive=true`安裝巢狀套件。

  >[!NOTE]
  >
  >Experience Manager service pack不支援Bootstrap安裝。<!-- UPDATE FOR EACH NEW RELEASE -->

  **驗證安裝**

  若要瞭解經過認證可搭配此版本使用的平台，請參閱[技術需求](/help/sites-deploying/technical-requirements.md)。

   1. 產品資訊頁(`/system/console/productinfo`)會在[!UICONTROL 已安裝產品].<!-- UPDATE FOR EACH NEW RELEASE -->下顯示更新的版本字串`Adobe Experience Manager (spversion)`
   1. 在OSGi主控台（使用網頁）中，所有OSGi套件組合均為&#x200B;**[!UICONTROL ACTIVE]**&#x200B;或&#x200B;**[!UICONTROL FRAGMENT]**     主控台： `/system/console/bundles`)。
   1. OSGi套件`org.apache.jackrabbit.oak-core`的版本為1.22.14或更新版本（使用WebConsole： `/system/console/bundles`）。

+++

+++7. 安裝AEM Experience Manager Forms附加元件套件

1. 確定您已安裝[!DNL Experience Manager] Service Pack。
1. 下載適用於您作業系統的 [AEM Forms 發行版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)所列出的對應 Forms 附加元件套件。
1. 依照[安裝Forms附加元件套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)中的說明安裝AEM Forms附加元件套件。
1. 如果您在Experience Manager 6.5 Forms中使用字母，請安裝[最新的AEMFD相容性套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)。

+++

## 在OSGi環境的AEM表單上下載並安裝Service Pack {#download-and-install-for-osgi-service-pack}


<!-- ![OSGi Installation Steps](/help/forms/using/assets/osgiinstallation.png)
-->

+++1. 備份您的現有環境

1. 備份[CRX儲存庫和資料庫結構描述](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html?lang=zh-Hant)。

>[!NOTE]
>
> 如果您安裝關聯式資料庫的AEM Forms Service Pack，則必須備份DB_schema。

+++

+++2. 下載必要的軟體

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=zh-Hant)
* [Forms附加元件套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)

+++

+++ 3.安裝Microsoft Visual C++可轉散發套件

* 在安裝Microsoft 6.5 Forms的電腦上，下載並安裝適用於Visual Studio 2015、2017、2019和2022[&#128279;](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022)的64位元版AEM Visual C++可轉散發套件。

>[!NOTE]
>
>
> 請確定您安裝了可轉散發套件（即使已安裝舊版），以確保最新版本的可用性。

+++

+++4. 安裝AEM Service Pack

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請在安裝前重新啟動執行個體。 如果執行個體的目前運作時間很高，Adobe建議重新啟動。
1. 安裝之前，請為您的[!DNL Experience Manager]執行個體建立快照或全新備份。
1. 從[軟體發佈](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)下載Service Pack。<!-- UPDATE FOR EACH NEW RELEASE -->
1. 開啟封裝管理員，然後選取&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。 如需詳細資訊，請參閱[封裝管理員](/help/sites-administering/package-manager.md)。
1. 選取封裝，然後選取&#x200B;**[!UICONTROL 安裝]**。

**自動安裝**

您可以使用兩種不同的方法來自動安裝[!DNL Experience Manager] Service Pack。<!--  UPDATE FOR EACH NEW RELEASE -->

* 伺服器上線時，請將封裝放入`../crx-quickstart/install`資料夾。 此封裝為      已自動安裝。
* 使用封裝管理員[&#128279;](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant)的HTTP API。 使用`cmd=install&recursive=true`安裝巢狀套件。

  >[!NOTE]
  >
  >Experience Manager service pack不支援Bootstrap安裝。<!-- UPDATE FOR EACH NEW RELEASE -->

  **驗證安裝**

  若要瞭解經過認證可搭配此版本使用的平台，請參閱[技術需求](/help/sites-deploying/technical-requirements.md)。

   1. 產品資訊頁(`/system/console/productinfo`)會在[!UICONTROL 已安裝產品]下顯示更新的版本字串`Adobe Experience Manager (spversion)`。<!-- UPDATE FOR EACH NEW RELEASE -->

   1. 在OSGi主控台中，所有OSGi套件組合均為&#x200B;**[!UICONTROL 作用中]**&#x200B;或&#x200B;**[!UICONTROL 片段]** （使用Web主控台： `/system/console/bundles`）。

      1. OSGi套件`org.apache.jackrabbit.oak-core`的版本為1.22.14或更新版本（使用Web主控台： `/system/console/bundles`）。

+++

+++5. 安裝Adobe Experience Manager Forms (AEM)附加元件套件

1. 確定您已安裝[!DNL Experience Manager] Service Pack。
1. 下載適用於您作業系統的 [AEM Forms 發行版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)所列出的對應 Forms 附加元件套件。
1. 依照[安裝Forms附加元件套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)中的說明安裝AEM Forms附加元件套件。
1. 如果您在Experience Manager 6.5 Forms中使用字母，請安裝[最新的AEMFD相容性套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)。

+++

## 疑難排解

* 如果封裝管理員UI **上的**&#x200B;對話方塊在安裝Service Pack期間結束，請等候錯誤記錄穩定後再存取部署。 等待與更新程式套件組合解除安裝相關的特定記錄，再確認安裝成功。 此問題通常會發生在Safari瀏覽器中，但也可能間歇性地發生在任何瀏覽器上。

* 安裝完成後，請檢查監視器記錄(error.log)是否有任何活動。 等候幾分鐘，直到記錄中沒有活動。 重新啟動AEM執行個體。

* 安裝AEM Forms 6.5.15.0或更新版本的Service Pack之後，如果您收到&#x200B;**服務無法使用錯誤**，[請安裝servlet片段和套件](/help/forms/using/aem-service-pack-installation-solution.md)以修正錯誤。
