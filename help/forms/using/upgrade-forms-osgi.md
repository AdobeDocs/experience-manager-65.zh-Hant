---
title: 升級至 AEM 6.5 Forms
seo-title: 升級至 AEM 6.5 Forms
description: 您可以執行從6.1 AEMForms、AEM 6.2Forms和LiveCycleES4 SP1到AEM6.3Forms的直接升級。
seo-description: 您可以執行從6.1 AEMForms、AEM 6.2Forms和LiveCycleES4 SP1到AEM6.3Forms的直接升級。
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 6%

---


# 升級至AEMOSGi {#upgrade-to-aem-forms-osgi}上的Forms6.5版

您可以執行從6.3Forms或6.4AEMForms直AEM接升級到AEM6.5Forms。

沒有從&#x200B;**AEM6.0Forms、AEM 6.1Forms**&#x200B;和&#x200B;**AEM 6.2Forms**&#x200B;到AEM6.5Forms的直接升級路徑。 執行升級至AEM6.2Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html)、[升級至AEM6.3Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html)或[升級至AEM6.4FormsAEM&lt;a5/AEM>，然後從6.3Forms、6.4Forms或AEM6.4升級至6.5。[](/help/forms/using/upgrade.md)

請執行下列動作，將AEMForms6.3或AEMForms6.4升級AEM至Forms6.5:

1. 將現有AEM實例升AEM級至6.5。步驟如下：

   1. 安裝適用於6.3Forms或AEM6.4Forms的最AEM新Service Pack和修補程式。 有關詳細資訊，請參見[AEM維護集線器](https://helpx.adobe.com/experience-manager/aem-releases-updates.html)。
   1. 準備升級的源實例。 如需詳細步驟，請參閱[升級至AEM6.5](/help/sites-deploying/upgrade.md)。
   1. 下載[AEM 6.5 QuickStart](/help/sites-deploying/deploy.md#getting%20the%20software)。
   1. **（僅限基於Unix/Linux的安裝）** 如果您使用UNIX或Linux作為底層作業系統，請開啟終端窗口，導航到包含crx-quickstart的資料夾，然後運行以下命令：

      `chmod -R 755 ../crx-quickstart`

   1. 將您的AEM實例升AEM級至6.3。如需逐步指示，請參閱[升級至AEM6.5](/help/sites-deploying/upgrade.md)。

      在繼續後續步驟之前，請等待&lt;crx-repository>/error.log檔案中停止顯示ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息。

      >[!NOTE]
      >
      >伺服器啟動並運行後，一些AEM Forms捆綁包仍處於安裝狀態。 每個安裝的捆綁包數量可能不同。 您可以安全地忽略這些束的狀態。 這些捆綁列在https://&#39;[server]:[port]&#39;/system/console/中。

1. 安裝AEM Forms附加套件。 步驟如下：

   1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
   1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
   1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;區段中：
      1. 從&#x200B;**[!UICONTROL Solution]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL Forms]**。
      1. 選擇包的版本和類型。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
   1. 點選適用於您作業系統的套件名稱，選取「**[!UICONTROL 接受EULA條款]**」，然後點選「**[!UICONTROL 下載]**」。
   1. 開啟[套件管理器](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
   1. 選擇軟體包並按一下&#x200B;**[!UICONTROL Install]**。

      您也可以使用[AEM Forms版本](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)文章中所列的直接連結下載套件。

      >[!NOTE]
      >
      >安裝軟體包後，系統會提示您重新啟動AEM實例。 **不要立即停止伺服器。** 在停止AEM Forms伺服器之前，請等到ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止顯示在 &lt;crx-repository>/error.log檔案中，並且日誌是穩定的。另請注意，一些軟體包可以保持安裝狀態。 您可以安全地忽略這些包的狀態。

1. 重新啟動AEM實例。

1. 執行安裝後活動。

   * **運行遷移實用程式**

      遷移實用程式使舊版的自適應表單和通信管理資產與AEM6.5表單相容。 您可以從「軟體散發」下載AEM此公用程式。 有關配置和使用遷移實用程式的逐步資訊，請參見[遷移實用程式](../../forms/using/migration-utility.md)。

      如果您使用[Sample將草稿和提交元件](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html)與資料庫整合併從舊版升級，則在執行升級後運行以下SQL查詢：

      ```sql
      UPDATE metadata m, additionalmetadatatable am
      SET m.dataType = am.value
      WHERE m.id = am.id
      AND am.key = 'dataType'
      ```

      ```sql
      DELETE from additionalmetadatatable
      WHERE `key` = 'dataType'
      ```

   * **(如果僅從AEM6.2Forms或舊版升級)重新配置Adobe Sign**

      如果您在舊版AEM Forms中設定了Adobe Sign，請從AEM Cloud服務重新設定Adobe Sign。 如需詳細資訊，請參閱[將Adobe Sign與AEM Forms整合。](../../forms/using/adobe-sign-integration-adaptive-forms.md)

   * **支援jQuery**

      在AEMForms6.5中，jQuery版本更新為3.2.1，而jQuery UI版本更新為1.12.1。表AEM單在&#x200B;**noConflict**&#x200B;模式下使用JQuery。 因此，如果您使用任何其他jQuery版本，則在執行升級時不會顯示任何問題。 但是，當您升級至AEM6.5Forms:

      * 請確定您的自訂元件（如果有）與支援的jQuery版本相容。
      * 從自訂元件移除不支援的API。 如需已移除API的清單，請參閱[升級指南](https://jquery.com/upgrade-guide/3.0/)。 例如，會移除對load()、.unload()和。error()API的支援。 使用。on()方法取代前述的API。 例如，將$(&quot;img&quot;)。load(fn)變更為$(&quot;img&quot;)。on(&quot;load&quot;, fn)。
   * **(如果僅從AEM6.2Forms或舊版升級)重新設定分析和報表**

      在AEMForms6.4中，不提供來源的流量變數和曝光的成功事件。 因此，從6.2Forms或舊AEM版升級時，AEM Forms停止傳送資料至Adobe Analytics伺服器，因此無法使用最適化表單的分析報表。 此外，AEM6.4Forms推出表單分析和成功事件版本的流量變數，用於欄位逗留時間。 因此，請為您的AEM Forms環境重新配置分析和報告。 如需詳細步驟，請參閱[設定分析和報表](../../forms/using/configure-analytics-forms-documents.md)。


1. 驗證伺服器是否升級成功，所有資料也成功遷移，並且可以正常運行。

   * **驗證綁定的狀態：確** 保所有綁定都處於活動狀態。
   * **驗證複製和反向複製：** 發佈、填寫和提交一些遷移的表單。也驗證已提交的資料。
   * **驗證管理員和開發人員使用者介** 面的存取權：從AEM管理員帳戶登入例項，並確認您擁有下列URL的存取權：

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   在AEMForms6.4中，crx-repository的結構已經更改。 如果從6.3Forms升級至AEM6.5Forms，請使用您重新建立的自訂路徑變更。 有關已更改路徑的完整清單，請參見](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)中的[Forms儲存AEM庫重構。

