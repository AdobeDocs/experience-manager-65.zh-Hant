---
title: 在OSGi上升級至AEM 6.5 Forms
description: 您可以從AEM 6.1 Forms、AEM 6.2 Forms和LiveCycleES4 SP1直接升級至AEM 6.3 Forms。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin,User
exl-id: 1e39455e-f588-42a2-91f5-daefcfed82a0
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on OSGi, AEM Forms Upgrade
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 1%

---

# 在OSGi上升級至AEM 6.5 Forms {#upgrade-to-aem-forms-osgi}

您可以從AEM 6.3 Forms或AEM 6.4 Forms直接升級至AEM 6.5 Forms。

不提供從&#x200B;**AEM 6.0 Forms、AEM 6.1 Forms**&#x200B;和&#x200B;**AEM 6.2 Forms**&#x200B;到AEM 6.5 Forms的直接升級路徑。 執行中繼[升級至AEM 6.2 Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html)、[升級至AEM 6.3 Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html)，或[升級至AEM 6.4 Forms](/help/forms/using/upgrade.md)，然後從AEM 6.3 Forms或AEM 6.4 Forms升級至AEM 6.5 Forms。

若要從AEM 6.3 Forms或AEM 6.4 Forms升級至AEM 6.5 Forms，請執行下列動作：

1. 將現有AEM執行個體升級至AEM 6.5。步驟如下：

   1. 安裝AEM 6.3 Forms或AEM 6.4 Forms的最新Service Pack和修補程式。 如需詳細資訊，請參閱[AEM維護中心](https://helpx.adobe.com/tw/experience-manager/aem-releases-updates.html)。
   1. 準備來源執行個體以進行升級。 如需詳細步驟，請參閱[升級至AEM 6.5](/help/sites-deploying/upgrade.md)。
   1. 下載[AEM 6.5 QuickStart](/help/sites-deploying/deploy.md#getting%20the%20software)。
   1. **（僅限Unix/Linux安裝）**&#x200B;如果您使用UNIX或Linux做為基礎作業系統，請開啟終端機視窗，瀏覽至包含crx-quickstart的資料夾，然後執行下列命令：

      `chmod -R 755 ../crx-quickstart`

   1. 將您的AEM執行個體升級至AEM 6.3。如需逐步指示，請參閱[升級至AEM 6.5](/help/sites-deploying/upgrade.md)。

      繼續後續步驟之前，請等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在&lt;crx-repository>/error.log檔案中。

      >[!NOTE]
      >
      >伺服器啟動並執行後，一些AEM Forms套件組合會維持安裝狀態。 每個安裝的套件組合數量可能有所不同。 您可以安全地忽略這些套裝的狀態。 套件組合列於https://&#39;[伺服器]：[連線埠]&#39;/system/console/。

1. 安裝AEM Forms附加元件套件。 步驟如下：

   1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
   1. 選取標題功能表中可用的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
   1. 在&#x200B;**[!UICONTROL 篩選器]**&#x200B;區段中：
      1. 從&#x200B;**[!UICONTROL 解決方案]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms]**。
      1. 選取封裝的版本和型別。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
   1. 選取適用於您作業系統的封裝名稱，選取&#x200B;**[!UICONTROL 接受EULA條款]**，然後選取&#x200B;**[!UICONTROL 下載]**。
   1. 開啟[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。
   1. 選取封裝並按一下&#x200B;**[!UICONTROL 安裝]**。

      您也可以使用[AEM Forms發行版本](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)文章中所列的直接連結來下載套件。

      >[!NOTE]
      >
      >安裝套件後，系統會提示您重新啟動AEM執行個體。 **不要立即停止伺服器。**&#x200B;在停止AEM Forms伺服器之前，請等候直到ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在&lt;crx-repository>/error.log檔案中，而且記錄檔穩定。 另請注意，有些套件可能維持已安裝狀態。 您可以安全地忽略這些套裝程式的狀態。

1. 重新啟動AEM執行個體。

   >[!NOTE]
   >
   建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。

1. 執行安裝後活動。

   * **執行移轉公用程式**

     移轉公用程式可讓舊版的最適化表單和通訊管理資產相容於AEM 6.5表單。 您可以從AEM Software Distribution下載公用程式。 如需設定及使用移轉公用程式的逐步資訊，請參閱[移轉公用程式](../../forms/using/migration-utility.md)。

     如果您使用[範例將草稿與提交元件](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html)與資料庫整合，並從舊版升級，請在執行升級後執行下列SQL查詢：

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

   * **(若僅從AEM 6.2 Forms或舊版升級)重新設定Adobe Sign**

     如果您已在舊版Adobe Sign中設定AEM Forms，請從AEM雲端服務重新設定Adobe Sign 。 如需詳細資訊，請參閱[整合Adobe Sign與AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)。

   * **支援jQuery**

     在AEM 6.5 Forms中，jQuery版本更新至3.2.1，jQuery UI版本更新至1.12.1。AEM表單在&#x200B;**noConflict**&#x200B;模式下使用JQuery。 因此，如果您使用任何其他jQuery版本，則執行升級時不會顯示任何問題。 不過，當您升級至AEM 6.5 Forms時：

      * 確保您的自訂元件（如果有的話）與支援的jQuery版本相容。
      * 從自訂元件移除不支援的API。 如需已移除的API清單，請參閱[升級指南](https://jquery.com/upgrade-guide/3.0/)。 例如，會移除對load()、.unload()和.error() API的支援。 使用.on()方法取代上述的API。 例如，將$(&quot;img&quot;)。load(fn)變更為$(&quot;img&quot;)。on(&quot;load&quot;， fn)。

   * **(若僅從AEM 6.2 Forms或舊版升級)重新設定分析和報表**

     在AEM 6.4 Forms中，無法使用曝光的來源和成功事件流量變數。 因此，當您從AEM 6.2 Forms或舊版升級時，AEM Forms會停止傳送資料至Adobe Analytics伺服器，且無法使用最適化表單的Analytics報表。 此外，AEM 6.4 Forms為表單分析版本引入流量變數，並為在欄位上逗留的時間量引入成功事件。 因此，請為您的AEM Forms環境重新設定分析和報表。 如需詳細步驟，請參閱[設定分析和報表](../../forms/using/configure-analytics-forms-documents.md)。

1. 請確認伺服器已順利升級，所有資料也已成功移轉，而且伺服器可正常運作。

   * **驗證套裝的狀態：**&#x200B;請確定所有套裝都處於作用中狀態。
   * **驗證復寫與反向復寫：** Publish、填寫並提交一些已移轉的表單。 同時驗證提交的資料。
   * **驗證對管理員和開發人員使用者介面的存取權：**&#x200B;從管理員帳戶登入AEM執行個體，並確認您擁有下列URL的存取權：

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   在AEM 6.4 Forms中，crx-repository的結構已變更。 如果從6.3 Forms升級至AEM 6.5 Forms，請使用變更的路徑進行重新建立的自訂。 如需已變更路徑的完整清單，請參閱AEM](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)中的[Forms存放庫重組。
