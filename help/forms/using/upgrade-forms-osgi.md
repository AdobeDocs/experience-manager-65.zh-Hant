---
title: 升級至AEMOSGi上的6.5Forms
description: 您可以執行從AEM6.1Forms、AEM6.2Forms和LiveCycleES4 SP1到AEM6.3Forms的直接升級。
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 1e39455e-f588-42a2-91f5-daefcfed82a0
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 4%

---

# 升級至AEMOSGi上的6.5Forms {#upgrade-to-aem-forms-osgi}

您可以執行從AEM6.3Forms或AEM6.4Forms到6.AEM5Forms的直接升級。

直接升級路徑 **AEM6.0FormsAEM6.1Forms**, **AEM 6.2Forms** 至AEM6.5Forms 執行中間 [升級至AEM6.2Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html)。 [升級至AEM6.3Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html)或 [升級至AEM6.4Forms](/help/forms/using/upgrade.md) 然後從AEMForms6.3，或AEMForms6.4升AEM級為Forms6.5

執行以下操作將AEM從6.3Forms或AEM6.4Forms升級到AEM6.5Forms:

1. 將現有實AEM例升級AEM到6.5。下面列出了這些步驟：

   1. 安裝最新的Service Pack和AEM6.3Forms或AEM6.4Forms的修補程式。 有關詳細資訊，請參閱 [維AEM護中心](https://helpx.adobe.com/tw/experience-manager/aem-releases-updates.html)。
   1. 準備源實例以進行升級。 有關詳細步驟，請參見 [升級AEM到6.5](/help/sites-deploying/upgrade.md)。
   1. 下載 [AEM6.5快速啟動](/help/sites-deploying/deploy.md#getting%20the%20software)。
   1. **（僅基於Unix/Linux的安裝）** 如果使用UNIX或Linux作為底層作業系統，請開啟終端窗口，導航到包含crx-quickstart的資料夾，然後運行以下命令：

      `chmod -R 755 ../crx-quickstart`

   1. 將實AEM例升級AEM到6.3。有關逐步說明，請參見 [升級AEM到6.5](/help/sites-deploying/upgrade.md)。

      在繼續後續步驟之前，請等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止出現在 &lt;crx-repository>/error.log檔案。

      >[!NOTE]
      >
      >伺服器啟動並運行後，幾個AEM Forms捆綁包仍處於安裝狀態。 每個安裝的捆綁包數量可能不同。 您可以安全地忽略這些束的狀態。 這些捆綁包列於https://&#39;[伺服器]:[埠]「/system/console/。

1. 安裝AEM Forms載入項包。 下面列出了這些步驟：

   1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
   1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
   1. 在 **[!UICONTROL 篩選器]** 部分：
      1. 選擇 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 的子菜單。
      1. 選擇包的版本和類型。 您還可以使用 **[!UICONTROL 搜索下載]** 選項。
   1. 點擊適用於您的作業系統的包名稱，選擇 **[!UICONTROL 接受EULA條款]**，然後點擊 **[!UICONTROL 下載]**。
   1. 開啟[套件管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
   1. 選擇包並按一下 **[!UICONTROL 安裝]**。

      您還可以使用中列出的直接連結下載軟體包 [AEM Forms釋放](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 文章。

      >[!NOTE]
      >
      >安裝軟體包後，系統會提示您重新啟動實AEM例。 **不要立即停止伺服器。** 停止AEM Forms伺服器之前，請等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止出現在 &lt;crx-repository>/error.log檔案，日誌穩定。 另請注意，一些軟體包可以保持已安裝狀態。 您可以安全地忽略這些包的狀態。

1. 重新啟動AEM實例。

1. 執行安裝後活動。

   * **運行遷移實用程式**

      遷移實用程式使早期版本的自適應表單和通信管理資產與AEM6.5表單相容。 可以從軟體分發下載AEM該實用程式。 有關配置和使用遷移實用程式的逐步資訊，請參見 [遷移實用程式](../../forms/using/migration-utility.md)。

      如果您使用 [整合草稿和提交元件的示例](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) 使用資料庫並從早期版本升級，然後在執行升級後運行以下SQL查詢：

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

   * **(如果僅從AEM6.2Forms或早期版本升級)重新配置Adobe Sign**

      如果您在以前版本的AEM Forms中配置了Adobe Sign，則從AEM雲服務中重新配置Adobe Sign。 有關詳細資訊，請參閱 [整合Adobe Sign與AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)。

   * **支援jQuery**

      在AEMForms6.5中， jQuery的版本更新為3.2.1, jQuery UI版本更新為1.12.1。AEM窗體在 **無衝突** 的子菜單。 因此，如果您使用的是任何其他jQuery版本，則在執行升級時不會顯示任何問題。 但是，升級到AEM6.5Forms時：

      * 確保自定義元件（如果有）與支援的jQuery版本相容。
      * 從自定義元件中刪除不支援的API。 請參閱 [升級指南](https://jquery.com/upgrade-guide/3.0/) 的API清單。 例如，將刪除對load()、.unload()和.error()API的支援。 使用.on()方法代替上述API。 例如，將$(&quot;img&quot;)。load(fn)更改為$(&quot;img&quot;)。on(&quot;load&quot;, fn)。
   * **(如果僅從AEM6.2Forms或早期版本升級)重新配置分析和報告**

      在AEMForms6.4中，沒有源流量變數和印象成功事件。 因此，當您從AEM6.2Forms或早期版本升級時，AEM Forms將停止向Adobe Analytics伺服器發送資料，並且自適應表單的分析報告不可用。 此外，AEM6.4Forms為表格分析版本引入了流量變數，並為欄位花費的時間引入了成功事件。 因此，請重新配置您的AEM Forms環境的分析和報告。 有關詳細步驟，請參見 [配置分析和報告](../../forms/using/configure-analytics-forms-documents.md)。


1. 驗證伺服器是否已成功升級，所有資料是否也已成功遷移，並且它可以正常運行。

   * **驗證捆綁包的狀態：** 確保所有捆綁包都處於活動狀態。
   * **驗證複製和反向複製：** 發佈、填寫和提交幾個遷移的表單。 同時驗證提交的資料。
   * **驗證對管理員和開發人員用戶介面的訪問權限：** 從管理AEM員帳戶登錄到實例，並驗證您是否有權訪問以下URL:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   在AEMForms6.4中，crx-repository的結構已更改。 如果從6.3Forms升級到AEM6.5Forms，請使用更改的路徑重新建立自定義。 有關已更改路徑的完整清單，請參見 [Forms資源庫重AEM組](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)。
