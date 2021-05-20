---
title: 已知問題
description: Adobe Experience Manager 6.5已知問題的發行說明
exl-id: 736037cf-af8c-4ce2-969e-c100a939a038
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 3%

---

# 已知問題 {#known-issues}

本頁保留2019年4月發行之Adobe Experience Manager 6.5的已知問題清單。

[如果](https://helpx.adobe.com/tw/support/experience-manager.html) 您需要已知問題的詳細資訊，請聯絡支援。

## 平台 {#platform}

* 系統回報CRX快速入門及其內容遭刪除的問題。

   在每個動作上，確定屬性`htmllibmanager.fileSystemOutputCacheLocation`不是空字串：

   1. 正在調用`/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`。
   2. 升級至AEM 6.5。
   3. 在AEM 6.5上執行「延遲內容移轉」。

   [知識庫](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html)文章提供了詳細資訊和解決此問題的方法。

* 如果您使用AEM 6.5執行個體的JDK 11，部署某些套件後，某些頁面可能會顯示為空白。 記錄檔中會顯示下列錯誤訊息：

   ```java
   *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
   java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
   ```

若要解決此錯誤：

1. 停止AEM例項。 前往`<aem_server_path_on_server>crx-quickstart\conf`並開啟`sling.properties`檔案。 Adobe建議備份此檔案。

1. 搜尋 `org.osgi.framework.bootdelegation=`. 新增`jdk.internal.reflect,jdk.internal.reflect.*`屬性，將結果顯示為。

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. 儲存檔案並重新啟動AEM執行個體。

## 資產 {#assets}

* **搜尋：** 如果搜尋字串包含前導空格，則搜尋不會產生任何傳回([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **資料夾中繼資料結構**:新增選擇按鈕後，ID和值欄位無法如預期呈現，且刪除功能無法運作。(CQ-4261144)
* 重新命名資產時，無法在資產名稱中使用空白字元。 (CQ-4266403)

## 表單 {#forms}

* 當AEM Forms安裝在Linux作業系統上時，具有硬體安全模組的數位簽名無法運作。 (CQ-4266721)
* (僅限WebSphere上的AEM Forms)如果您以&#x200B;**使用者名稱**&#x200B;作為搜尋准則搜尋&#x200B;**管理員**,**Forms Workflow** > **任務搜尋**&#x200B;選項不會傳回任何結果。 (CQ-4266457)

* AEM Forms無法將具有JPEG壓縮的TIF和TIFF檔案轉換為PDF檔案。 (CQ-4265972)
* **AEM Forms Assets Scanner**&#x200B;和&#x200B;**Letter to Interactive Communication Migration**&#x200B;選項在&#x200B;**AEM Forms Migration**&#x200B;頁面上無法運作。 (CQ-4266572)

* （僅限JBoss 7）從舊版升級至AEM 6.5 Forms，且舊版有已建立並使用預設提交或預設呈現程式副本的程式(.lca)時，使用此類程式(.lca)的HTML5 Forms無法執行所需動作。 (CQ-4243928)
* 在自適應自中，當從規則編輯器調用表單資料模型服務以動態更新影像選擇元件的值時，不更新影像選擇元件的值。 (CQ-4254754)
* AEM Forms Designer安裝程式需要32位版本的[Visual C++可再發行運行時包2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads)和[Visual C++可再發行運行時包2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package)。 在開始安裝之前，請確保已安裝上述可重新分發的運行時包。 (CQ-4265668)

* PDF產生器不支援智慧卡驗證。  當管理員在Windows伺服器上啟用組策略`Interactive Logon: Require Smart card`時，所有現有PDF生成器用戶都將失效。

* 將適用性表單設定為動態更新元件的值，並透過Dispatcher存取托管表單的發佈例項時，動態更新欄位值的功能將停止運作。 若要解決此問題，請在發佈執行個體上開啟CRXDE，導覽至`/libs/fd/af/runtime/clientlibs/guideChartReducer`，並建立下方所列的屬性。

   * 名稱：allowProxy
   * 類型：布林值
   * 值：true
   * 受保護：False
   * 強制：False
   * 多個：False
   * 自動建立：False

   此屬性可讓執行階段資料夾下的用戶端程式庫存取Proxy。 (CQ-4268679)

* AEM Forms啟動時，會顯示`SAX Security Manager could not be setup`警告。
* 在執行AEM FormsReader20.10.00版的Apple iOS或iPadOS上開啟受Adobe Acrobat檔案安全性保護的PDF時。
