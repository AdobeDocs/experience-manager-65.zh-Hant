---
title: Adobe分類
seo-title: Adobe Classifications
description: 瞭解Adobe分類。
seo-description: Learn about Adobe Classifications.
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
exl-id: 0e675ce8-ba3b-481d-949e-0c85c97054d2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 5%

---

# Adobe分類{#adobe-classifications}

Adobe分類將分類資料導出到 [Adobe Analytics](/help/sites-administering/adobeanalytics.md) 按計畫進行。 出口商是 **com.adobe.cq.scheduled.exporter.Exporter**。

要配置此項，請執行以下操作：

1. 使用 **導航**&#x200B;選中 **工具**。 **Cloud Services**，則 **舊Cloud Services**。
1. 滾動到 **Adobe Analytics** 選擇 **顯示配置**。
1. 按一下 **[+]** 連結到您的Adobe Analytics配置。

1. 在 **建立框架** 對話框：

   * 指定 **標題**。
   * （可選）您可以指定 **名稱**，用於將框架詳細資訊儲存在儲存庫中的節點。
   * 選擇 **Adobe Analytics分類**

   然後按一下 **建立**。

   ![「建立框架」對話框](assets/aa-25.png)

1. 的 **分類設定** 對話框開啟以進行編輯。

   ![「分類設定」對話框](assets/aa-classifications-settings.png)

   屬性包括：

   | **欄位** | **說明** |
   |---|---|
   | 已啟用 | 選擇 **是** 啟用Adobe分類設定。 |
   | 發生衝突時覆寫 | 選擇 **是** 覆蓋任何資料衝突。 預設情況下，此值設定為 **否**。 |
   | 刪除已處理的項目 | 如果設定為 **是**，在導出處理的節點後刪除它們。 預設值為 **假**。 |
   | 匯出工作說明 | 輸入Adobe分類作業的說明。 |
   | 通知電子郵件 | 輸入Adobe分類通知的電子郵件地址。 |
   | 報表套裝 | 輸入要為其運行導入作業的報表套件。 |
   | 資料集 | 輸入要為其運行導入作業的資料集關係ID。 |
   | 轉換程式 | 從下拉菜單中，選擇變壓器實現。 |
   | 資料來源 | 導航到資料容器的路徑。 |
   | 匯出排程 | 選擇導出的計畫。 預設值是每30分鐘一次。 |

1. 按一下 **確定** 的子菜單。

## 修改頁面大小 {#modifying-page-size}

記錄在頁中處理。 預設情況下，Adobe分類會建立頁面大小為1000的頁面。

「Adobe分類」中的每個定義，頁面最大可以是25000頁，並可從Felix控制台修改。 在導出過程中，「Adobe分類」會鎖定源節點以防止併發修改。 導出後、出錯時或會話關閉時，節點將解鎖。

要更改頁面大小：

1. 導航至OSGI控制台，位於 **https://&lt;host>:&lt;port>/system/console/configMgr** 選擇 **AdobeAEM分類導出器**。

   ![aa-26](assets/aa-26.png)

1. 更新 **導出頁面大小** 根據需要，按一下 **保存**。

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Adobe分類以前稱為SAINT出口商。

導出器可以使用轉換器將導出資料轉換為特定格式。 對於Adobe分類，子介面 `SAINTTransformer<String[]>` 實現了變壓器介面。 此介面用於將資料類型限制為 `String[]` SAINTAPI使用的，並具有標籤器介面來查找此類服務以供選擇。

在預設實現SAINTDefaultTransformer中，導出器源的子資源被視為記錄，屬性名稱作為鍵，屬性值作為值。 的 **鍵** 列作為第一列自動添加 — 其值將是節點名稱。 命名空間屬性(包含 `:`)。

*節點結構：*

* ID分類 `nt:unstructured`

   * 1 `nt:unstructured`

      * 產品=我的產品名稱（字串）
      * 價格= 120.90（字串）
      * 大小= M（字串）
      * 顏色=黑色（字串）
      * 顏色^代碼= 101（字串）

**SAINT題頭和記錄：**

| **金鑰** | **產品** | **價格** | **大小** | **彩色** | **顏色^代碼** |
|---|---|---|---|---|---|
| 1 | 我的產品名稱 | 120.90 | M | black | 101 |

屬性包括：

<table>
 <tbody>
  <tr>
   <td><strong>屬性路徑</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>變壓器</td>
   <td>SAINTransferer實現的類名</td>
  </tr>
  <tr>
   <td>電子郵件</td>
   <td>通知電子郵件地址。</td>
  </tr>
  <tr>
   <td>報告套房</td>
   <td>要為其運行導入作業的報表套件ID。 </td>
  </tr>
  <tr>
   <td>資料集</td>
   <td>要為其運行導入作業的資料集關係ID。 </td>
  </tr>
  <tr>
   <td>說明</td>
   <td>作業描述。 <br /> </td>
  </tr>
  <tr>
   <td>覆寫</td>
   <td>覆蓋資料衝突的標誌。 預設值為 <strong>假</strong>。</td>
  </tr>
  <tr>
   <td>校驗分區</td>
   <td>用於檢查報告套件是否相容的標誌。 預設值為 <strong>真</strong>。</td>
  </tr>
  <tr>
   <td>刪除已處理</td>
   <td>標誌，用於在導出後刪除已處理的節點。 預設值為 <strong>假</strong>。</td>
  </tr>
 </tbody>
</table>

## 自動Adobe分類導出 {#automating-adobe-classifications-export}

您可以建立自己的工作流，以便任何新導入都啟動工作流以在中建立適當且結構正確的資料 **/var/export/** 以便將其導出到Adobe分類。
