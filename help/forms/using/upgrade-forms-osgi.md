---
title: 升級至AEM 6.5 Forms
seo-title: 升級至AEM 6.5 Forms
description: 您可以從AEM 6.1 Forms、AEM 6.2 Forms和LiveCycle ES4 SP1直接升級至AEM 6.3 Forms。
seo-description: 您可以從AEM 6.1 Forms、AEM 6.2 Forms和LiveCycle ES4 SP1直接升級至AEM 6.3 Forms。
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---


# 升級至OSGi {#upgrade-to-aem-forms-osgi}上的AEM 6.5 Forms

您可以直接從AEM 6.3 Forms或AEM 6.4 Forms升級至AEM 6.5 Forms。

無法提供從&#x200B;**AEM 6.0 Forms、AEM 6.1 Forms**&#x200B;和&#x200B;**AEM 6.2 Forms**&#x200B;直接升級至AEM 6.5 Forms的路徑。 執行升級至AEM 6.2 Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html)、[的中級[升級至AEM 6.3 Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html)或[升級至AEM 6.4 Forms](/help/forms/using/upgrade.md)，然後從AEM 6.3 Forms或AEM 6.4 Forms升級至AEM 6.5表格。

請執行下列動作，以從AEM 6.3 Forms或AEM 6.4 Forms升級至AEM 6.5 Forms:

1. 將現有的AEM例項升級至AEM 6.5。步驟如下：

   1. 安裝AEM 6.3 Forms或AEM 6.4 Forms的最新Service Pack和修補程式。 如需詳細資訊，請參閱[AEM維護中樞](https://helpx.adobe.com/experience-manager/aem-releases-updates.html)。
   1. 準備升級的源實例。 如需詳細步驟，請參閱[升級至AEM 6.5](/help/sites-deploying/upgrade.md)。
   1. 下載[AEM 6.5 QuickStart](/help/sites-deploying/deploy.md#getting%20the%20software)。
   1. **（僅限基於Unix/Linux的安裝）** 如果您使用UNIX或Linux作為底層作業系統，請開啟終端窗口，導航到包含crx-quickstart的資料夾，然後運行以下命令：

      `chmod -R 755 ../crx-quickstart`

   1. 將您的AEM實例升級至AEM 6.3。如需逐步指示，請參閱「升級至AEM 6.5[」。](/help/sites-deploying/upgrade.md)

      在繼續後續步驟之前，請等待&lt;crx-repository>/error.log檔案中停止顯示ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息。

      >[!NOTE]
      >
      >伺服器啟動並執行後，一些AEM Forms組合會維持在安裝狀態。 每個安裝的捆綁包數量可能不同。 您可以安全地忽略這些束的狀態。 這些捆綁列在https://&#39;[server]:[port]&#39;/system/console/中。

1. 安裝AEM Forms附加元件套件。 步驟如下：

   1. 開啟[軟體分發](https://experience.adobe.com/downloads)。 您必須有Adobe ID才能登入「軟體散發」。
   1. 點選頁首功能表中的「Adobe Experience Manager **[!UICONTROL 」。]**
   1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;區段中：
      1. 從&#x200B;**[!UICONTROL Solution]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL Forms]**。
      1. 選擇包的版本和類型。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
   1. 點選適用於您作業系統的套件名稱，選取「**[!UICONTROL 接受EULA條款]**」，然後點選「**[!UICONTROL 下載]**」。
   1. 開啟[包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) ，然後按一下&#x200B;**[!UICONTROL 上載包]**&#x200B;來上載包。
   1. 選擇軟體包並按一下&#x200B;**[!UICONTROL Install]**。

      您也可以使用[AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)文章中所列的直接連結下載套件。

      >[!NOTE]
      >
      >安裝套件後，系統會提示您重新啟動AEM例項。 **不要立即停止伺服器。** 在停止AEM Forms伺服器之前，請等到ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在 &lt;crx-repository>/error.log檔案中，且記錄檔是穩定的。另請注意，一些軟體包可以保持安裝狀態。 您可以安全地忽略這些包的狀態。

1. 重新啟動AEM例項。

1. 執行安裝後活動。

   * **運行遷移實用程式**

      移轉公用程式可讓舊版的最適化表單和通訊管理資產與AEM 6.5表單相容。 您可從「AEM Software Distribution」（AEM軟體散發）下載公用程式。 有關配置和使用遷移實用程式的逐步資訊，請參見[遷移實用程式](../../forms/using/migration-utility.md)。

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

   * **（如果僅從AEM 6.2 Forms或舊版升級）重新設定Adobe Sign**

      如果您在舊版AEM Forms中設定了Adobe Sign，請從AEM Cloud服務重新設定Adobe Sign。 如需詳細資訊，請參閱[將Adobe Sign與AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)整合。

   * **支援jQuery**

      在AEM 6.5 Forms中，jQuery版本已更新為3.2.1，而jQuery UI版本已更新為1.12.1。AEM Form在&#x200B;**noConflict**&#x200B;模式中使用JQuery。 因此，如果您使用任何其他jQuery版本，則在執行升級時不會顯示任何問題。 不過，當您升級至AEM 6.5 Forms時：

      * 請確定您的自訂元件（如果有）與支援的jQuery版本相容。
      * 從自訂元件移除不支援的API。 如需已移除API的清單，請參閱[升級指南](https://jquery.com/upgrade-guide/3.0/)。 例如，會移除對load()、.unload()和。error()API的支援。 使用。on()方法取代前述的API。 例如，將$(&quot;img&quot;)。load(fn)變更為$(&quot;img&quot;)。on(&quot;load&quot;, fn)。
   * **（如果僅從AEM 6.2 Forms或舊版升級）重新設定分析和報表**

      在AEM 6.4 Forms中，沒有來源的流量變數和曝光的成功事件。 因此，當您從AEM 6.2 Forms或舊版升級時，AEM Forms會停止傳送資料至Adobe Analytics伺服器，而且不提供最適化表單的分析報表。 此外，AEM 6.4 Forms針對表單分析和成功事件的版本，針對欄位逗留時間引入流量變數。 因此，請重新設定AEM Forms環境的分析和報表。 如需詳細步驟，請參閱[設定分析和報表](../../forms/using/configure-analytics-forms-documents.md)。


1. 驗證伺服器是否升級成功，所有資料也成功遷移，並且可以正常運行。

   * **驗證綁定的狀態：確** 保所有綁定都處於活動狀態。
   * **驗證複製和反向複製：** 發佈、填寫和提交一些遷移的表單。也驗證已提交的資料。
   * **驗證管理員和開發人員使用者介面的存** 取權：從管理員帳戶登入AEM例項，並驗證您有下列URL的存取權：

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   在AEM 6.4 Forms中，crx-repository的結構已變更。 如果從6.3 Forms升級至AEM 6.5 Forms，請使用您重新建立的變更路徑進行自訂。 如需變更路徑的完整清單，請參閱「AEM](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)中的[ Forms Repository Restructing」。

