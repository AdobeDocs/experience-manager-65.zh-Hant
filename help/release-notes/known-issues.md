---
title: 已知問題
description: Adobe Experience Manager 6.3已知問題的發行說明
uuid: 8fbdb167-833a-4179-aad1-0a26a4e5b3a7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: d11fc727-f23a-4cde-9fa6-97e2c81b4ad0
docset: aem65
translation-type: tm+mt
source-git-commit: 0ae42d9f81df89a7e1c08fac5cce5240f14e8c60

---


# 已知問題 {#known-issues}

本頁保留2019年4月發行的Adobe Experience Manager 6.5已知問題清單。

[如果您需要](https://helpx.adobe.com/support/experience-manager.html) 有關已知問題的詳細資訊，請連絡支援。

## 平台 {#platform}

會報告刪除CRX-Quickstart及其內容的問題。

在每個動作上，請確定「*htmllibmanager.fileSystemOutputCacheLocation*」屬性從來不是空字串：

1. 呼叫&quot;*/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true*&quot;。
2. 升級至AEM 6.5。
3. 在AEM 6.5上執行「延遲內容移轉」。

有 [知識庫文章](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html) ，其中提供進一步的詳細資訊以及此問題的解決方法。

## 資產 {#assets}

* **搜尋：** 如果搜尋字串包含前導空格，則搜尋不會產生任何傳回([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))
* **資料夾中繼資料結構**:新增選擇按鈕後，ID和值欄位不會如預期呈現，刪除功能也無法運作。 (CQ-4261144)
* 在重新命名資產時，無法在資產名稱中使用空白字元。 (CQ-4266403)

## 表單 {#forms}

* 當AEM Forms安裝在Linux作業系統上時，Digital Signature with Hardware Security Module（含硬體安全性模組的數位簽章）將無法運作。 (CQ-4266721)
* （僅限WebSphere上的AEM Forms）如果您搜尋以使用者名稱為搜尋准則的管理員( **Administrator** ),**Forms Workflow **> **Task Search****** （任務搜尋）選項不會傳回任何結果。 (CQ-4266457)

* AEM Forms無法將具有JPEG壓縮的。tif和。tiff檔案轉換為PDF檔案。 (CQ-4265972)
* 「 **AEM Forms Assets掃描器** 」和「Letter to Interactive Communication Migration **」（互動式通訊移轉信號）選項無法在「** AEM Forms移轉 **** 」頁面上運作。 (CQ-4266572)

* （僅限JBoss 7）從舊版升級至AEM 6.5 Forms，而舊版有建立並使用預設提交或預設演算程式副本的程式(.lca)時，使用此類程式(.lca)的HTML5 Forms無法執行必要動作。 (CQ-4243928)
* 在自適應中，當從規則編輯器調用表單資料模型服務以動態更新影像選擇元件的值時，不更新影像選擇元件的值。 (CQ-4254754)
* AEM Forms Designer安裝程式需要32位元版本的 [Visual C++可重新分發的執行階段套件2012](https://support.microsoft.com/en-in/help/2977003/the-latest-supported-visual-c-downloads) , [Visual C++可重新分發的執行階段套件2013](https://support.microsoft.com/en-in/help/3179560/update-for-visual-c-2013-and-visual-c-redistributable-package)。 在開始安裝之前，請確定已安裝前述的可重新分發的執行階段套件。 (CQ-4265668)

* 當將自適應表單配置為動態更新元件的值並且托管表單的發佈實例通過調度器訪問時，動態更新欄位值的功能將停止工作。 若要解決此問題，請在發佈例項上開啟CRXDE，導覽至/libs/fd/af/runtime/clientlibs/guideChartReducer，並建立下列屬性。

   * 名稱：allowProxy
   * 類型：布林值
   * 值：true
   * 受保護：False
   * 強制：False
   * 多重：False
   * 自動建立：弗拉塞

此屬性可讓執行時期資料夾下的用戶端程式庫存取Proxy。 (CQ-4268679)

