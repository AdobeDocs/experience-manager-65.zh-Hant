---
title: 已知問題
description: Adobe Experience Manager 6.5已知問題的發行說明
translation-type: tm+mt
source-git-commit: f72101dadaa8d5d12f2f9a636548b18386b79b0a
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 3%

---


# 已知問題 {#known-issues}

本頁保留2019年4月發行的Adobe Experience Manager 6.5已知問題清單。

[如果](https://helpx.adobe.com/tw/support/experience-manager.html) 您需要有關已知問題的詳細資訊，請聯絡支援。

## 平台 {#platform}

* 會報告刪除CRX-Quickstart及其內容的問題。

   在這些動作中，請確定屬性`htmllibmanager.fileSystemOutputCacheLocation`不是空字串：

   1. 呼叫`/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`。
   2. 升級至AEM 6.5。
   3. 在AEM 6.5上執行「延遲內容移轉」。

   有[知識庫](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html)文章提供進一步的詳細資訊，以及此問題的解決方法。

* 如果您正在搭配AEM 6.5執行個體使用JDK 11，部分頁面在部署某些封裝後可能會顯示為空白。 日誌檔案中顯示以下錯誤消息：

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

要解決此錯誤：

1. 停止AEM例項。 前往`<aem_server_path_on_server>crx-quickstart\conf`並開啟`sling.properties`檔案。 Adobe建議備份此檔案。

1. 搜尋 `org.osgi.framework.bootdelegation=`. 添加`jdk.internal.reflect,jdk.internal.reflect.*`屬性以將結果顯示為。

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. 儲存檔案並重新啟動AEM例項。

## 資產 {#assets}

* **搜尋：** 如果搜尋字串包含前導空格，搜尋不會產生任何傳回([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **資料夾中繼資料結構**:新增選擇按鈕後，ID和值欄位不會如預期呈現，刪除功能也無法運作。(CQ-4261144)
* 在重新命名資產時，無法在資產名稱中使用空白字元。 (CQ-4266403)

## 表單 {#forms}

* 當AEM Forms安裝在Linux作業系統上時，Digital Signature with Hardware Security Module無法運作。 (CQ-4266721)
* （僅限WebSphere上的AEM Forms）如果您以&#x200B;**使用者名稱**&#x200B;搜尋標準搜尋&#x200B;**管理員**，則&#x200B;**表單工作流程** > **任務搜尋**&#x200B;選項不會傳回任何結果。 (CQ-4266457)

* AEM Forms無法將TIF和TIFF檔案與JPEG壓縮轉換為PDF檔案。 (CQ-4265972)
* **AEM Forms Assets Scanner**&#x200B;和&#x200B;**Letter to Interactive Communication Migration**&#x200B;選項在&#x200B;**AEM Forms Migration**&#x200B;頁面上無法運作。 (CQ-4266572)

* （僅限JBoss 7）從舊版升級至AEM 6.5 Forms，而舊版有建立並使用預設提交或預設演算程式副本的程式(.lca)時，使用此類程式(.lca)的HTML5 Forms無法執行必要動作。 (CQ-4243928)
* 在自適應中，當從規則編輯器調用表單資料模型服務以動態更新影像選擇元件的值時，不更新影像選擇元件的值。 (CQ-4254754)
* AEM Forms Designer安裝程式需要32位元版本的[Visual C++可重新散發的執行階段套件2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads)和[Visual C++可重新散發的執行階段套件2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package)。 在開始安裝之前，請確定已安裝前述的可重新分發的執行階段套件。 (CQ-4265668)

* PDF產生器不支援智慧卡驗證。  當管理員在Windows伺服器上啟用「群組原則`Interactive Logon: Require Smart card`」時，所有現有的PDF產生器使用者都會失效。

* 當將自適應表單配置為動態更新元件的值並且托管表單的發佈實例通過調度器訪問時，動態更新欄位值的功能將停止工作。 若要解決問題，請在發佈例項上開啟CRXDE，導覽至`/libs/fd/af/runtime/clientlibs/guideChartReducer`，並建立下列的屬性。

   * 名稱：allowProxy
   * 類型：布林值
   * 值：true
   * 受保護：False
   * 強制：False
   * 多重：False
   * 自動建立：False

   此屬性可讓執行時期資料夾下的用戶端程式庫存取Proxy。 (CQ-4268679)

* 當AEM Forms啟動時，會出現`SAX Security Manager could not be setup`警告。
* 當您在執行Adobe Acrobat Reader 20.10.00版的Apple iOS或iPadOS上開啟受AEM Forms Document Security保護的PDF時。
