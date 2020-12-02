---
title: Adobe分類
seo-title: Adobe分類
description: 瞭解Adobe分類。
seo-description: 瞭解Adobe分類。
uuid: 57fb59f4-da90-4fe7-a5b1-c3bd51159a16
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6787511a-2ce0-421a-bcfb-90d5f32ad35e
translation-type: tm+mt
source-git-commit: 4456b5366387c27810c407d6ac9e6c17fc290269
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 5%

---


# Adobe分類{#adobe-classifications}

Adobe分類會以排程方式將分類資料匯出至[Adobe Analytics](/help/sites-administering/adobeanalytics.md)。 導出器是&#x200B;**com.adobe.cq.scheduled.exporter.Exporter**&#x200B;的實現。

若要設定此值：

1. 使用&#x200B;**Navigation**，選擇&#x200B;**Tools**、**Cloud Services**，然後選擇&#x200B;**Legacy Cloud Services**。
1. 捲動至&#x200B;**Adobe Analytics**，然後選取&#x200B;**顯示設定**。
1. 按一下Adobe Analytics設定旁的&#x200B;**[+]**&#x200B;連結。

1. 在&#x200B;**建立框架**&#x200B;對話框中：

   * 指定&#x200B;**Title**。
   * 或者，您可以為儲存庫中儲存框架詳細資訊的節點指定&#x200B;**名稱**。
   * 選擇&#x200B;**Adobe Analytics分類**

   然後按一下&#x200B;**建立**。

   ![「建立框架」對話框](assets/aa-25.png)

1. **分類設定**&#x200B;對話方塊隨即開啟以供編輯。

   ![「分類設定」對話方塊](assets/aa-classifications-settings.png)

   屬性包括：

   | **欄位** | **說明** |
   |---|---|
   | 已啟用 | 選擇&#x200B;**是**&#x200B;以啟用Adobe分類設定。 |
   | 發生衝突時覆寫 | 選擇&#x200B;**是**&#x200B;覆寫任何資料衝突。 預設情況下，此值設定為&#x200B;**No**。 |
   | 刪除已處理的項目 | 如果設定為&#x200B;**Yes**，則在導出處理的節點後將其刪除。 預設值為&#x200B;**False**。 |
   | 匯出工作說明 | 輸入Adobe分類工作的說明。 |
   | 通知電子郵件 | 輸入Adobe分類通知的電子郵件地址。 |
   | 報表套裝 | 輸入報表套裝以執行其匯入工作。 |
   | 資料集 | 輸入要為其運行導入作業的資料集關係ID。 |
   | 轉換程式 | 從下拉式選單中，選取變壓器實作。 |
   | 資料來源 | 導覽至資料容器的路徑。 |
   | 匯出排程 | 選擇導出的計畫。 預設值是每30分鐘一次。 |

1. 按一下&#x200B;**確定**&#x200B;保存設定。

## 修改頁面大小{#modifying-page-size}

記錄會在頁面中處理。 依預設，Adobe分類會建立頁面大小為1000的頁面。

Adobe分類中的每個定義的頁面大小上限為25000，而且可從Felix主控台修改。 在匯出期間，Adobe分類會鎖定來源節點，以防止並行修改。 導出後、出錯時或會話關閉時，節點將被解鎖。

若要變更頁面大小：

1. 導覽至位於&#x200B;**https://&lt;host>:&lt;port>/system/console/configMgr**&#x200B;的OSGI主控台，然後選取&#x200B;**Adobe AEM Classifications Exporter**。

   ![aa-26](assets/aa-26.png)

1. 視需要更新&#x200B;**匯出頁面大小**，然後按一下「儲存&#x200B;**」。**

## SAINTDefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Adobe分類先前稱為SAINT匯出器。

導出器可以使用變壓器將導出資料轉換為特定格式。 對於Adobe分類，已提供實作變形器介面的子介面`SAINTTransformer<String[]>`。 此介面可用來將資料類型限制為`String[]`,SAINT API會使用此類資料類型，並具有標籤介面來尋找此類服務以供選擇。

在預設實施SAINTDefaultTransformer中，導出器源的子資源被視為具有屬性名稱作為密鑰的記錄，而屬性值作為值。 **Key**&#x200B;欄會自動新增為第一欄——其值將是節點名稱。 不考慮名稱空間屬性（包含`:`）。

*節點結構：*

* id-classification `nt:unstructured`

   * 1 `nt:unstructured`

      * 產品=我的產品名稱（字串）
      * 價格= 120.90（字串）
      * 大小= M（字串）
      * 顏色=黑色（字串）
      * Color^Code = 101（字串）

**SAINT標題與記錄：**

| **關鍵** | **產品** | **價格** | **大小** | **彩色** | **Color^Code** |
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
   <td>SAINTransfer實施的類名</td>
  </tr>
  <tr>
   <td>電子郵件</td>
   <td>通知電子郵件地址。</td>
  </tr>
  <tr>
   <td>reportsuites</td>
   <td>報表套裝ID，以執行其匯入工作。 </td>
  </tr>
  <tr>
   <td>資料集</td>
   <td>資料集關聯ID，以執行的匯入工作。 </td>
  </tr>
  <tr>
   <td>說明</td>
   <td>工作說明。<br /> </td>
  </tr>
  <tr>
   <td>覆寫</td>
   <td>覆寫資料衝突的旗標。 預設值為<strong>false</strong>。</td>
  </tr>
  <tr>
   <td>checkdipsions</td>
   <td>標幟以檢查報表套裝的相容性。 預設值為<strong>true</strong>。</td>
  </tr>
  <tr>
   <td>deleteprocessed</td>
   <td>標幟可在匯出後刪除已處理的節點。 預設值為<strong>false</strong>。</td>
  </tr>
 </tbody>
</table>

## 自動化Adobe分類匯出{#automating-adobe-classifications-export}

您可以建立自己的工作流程，讓任何新匯入都啟動工作流程，以建立&#x200B;**/var/export/**&#x200B;中適當且結構正確的資料，以便匯出至Adobe分類。
