---
title: 新增Search&Promote功能至您的頁面
seo-title: 新增Search&Promote功能至您的頁面
description: 將Search&Promote功能整合在您的網站中，您可以使用Search&Promote元件來新增功能至您的頁面，例如關鍵字搜尋、搜尋結果頁面搜尋調整和橫幅。
seo-description: 將Search&Promote功能整合在您的網站中，您可以使用Search&Promote元件來新增功能至您的頁面，例如關鍵字搜尋、搜尋結果頁面搜尋調整和橫幅。
uuid: 8cd3c143-cb0b-4eb0-931d-9d447ea3c950
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 968b9131-ccdf-4856-b504-bc1a44974980
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50

---


# 新增Search&amp;Promote功能至您的頁面{#adding-search-promote-features-to-your-page}

若要將Search&amp;Promote功能整合在您的網站中，請使用Search&amp;Promote元件將下列功能新增至您的頁面：

* 關鍵字搜尋
* 搜尋結果頁面
* 搜尋調整
* 橫幅

請注意，您只有在AEM管理員已啟用Search&amp;Promote功能時，才能使用這些功能。 請參 [閱「與Adobe Search&amp;Promote整合」](/help/sites-administering/search-and-promote.md)。

Facet是在Search&amp;Promote伺服器上設定，每個元件提供的資訊也是一樣。 下表提供每個元件的簡短說明。 後續章節提供其使用的詳細資訊。

<table>
 <tbody>
  <tr>
   <th>Search&amp;Promote元件</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>橫幅</td>
   <td>顯示橫幅廣告。 橫幅會根據透過Search&amp;Promote收集的資料來選取。<br /> </td>
  </tr>
  <tr>
   <td>階層連結</td>
   <td>顯示搜尋關鍵字以及使用者已套用至搜尋結果的篩選順序。</td>
  </tr>
  <tr>
   <td>核取方塊清單-Facet</td>
   <td>選取Facet以篩選搜尋結果的核取方塊清單。</td>
  </tr>
  <tr>
   <td>下拉式清單 Facet</td>
   <td>篩選搜尋結果的Facet下拉式清單。</td>
  </tr>
  <tr>
   <td>連結清單 Facet</td>
   <td>篩選搜尋結果的Facet連結清單。</td>
  </tr>
  <tr>
   <td>分頁</td>
   <td>控制在搜尋結果頁面中導覽。</td>
  </tr>
  <tr>
   <td>結果</td>
   <td>顯示關鍵字搜尋的結果。</td>
  </tr>
  <tr>
   <td>搜尋</td>
   <td>新增搜尋欄位至頁面。</td>
  </tr>
 </tbody>
</table>

## 建立搜索結果頁 {#creating-the-search-results-page}

使用WCM網站主控台建立顯示搜尋結果的頁面。 如果搜尋元件使用相同的Search&amp;Promote服務，其搜尋結果會顯示在此頁面上。

可讓使用者檢閱搜尋結果的元件包括「結果」和「分頁」。 在「編 **輯** 」或「設計」模式中，「結果」元件沒有可配置屬性。 「結果」元件只會列出搜尋結果，其中提供其他頁面的連結，並顯示搜尋關鍵字的結果數。

![srresultscomp](assets/srchresultscomp.png)

Pagination **元件** ，可讓使用者導覽多頁搜尋結果。 使用者可以查看頁數、移至下一頁或上一頁、選擇要開啟的頁面，或將所有結果合併至一頁。

![srchpagenation](assets/srchpagination.png)

您可以在「編輯」模式中設定下列元件屬性，以控制執行時期行為：

* 隱藏單一結果頁面：選取此選項，可在搜尋傳回單一結果頁面時隱藏頁面導覽控制項。
* Hide First/Last:選取此選項可防止使用者跳至結果的第一頁或最後一頁。
* 隱藏上一頁／下一頁：決定使用者是否可以相對於目前頁面導覽結果頁面。
* 全部隱藏檢視：判斷使用者是否可以合併單一頁面上的所有搜尋結果。 通常，提供分頁資料可以更有效地使用伺服器資源。 選擇此選項可防止在一條響應消息中傳輸大型資料集。

### 啟用依Facet篩選結果 {#enabling-the-filtering-of-results-by-facets}

您可讓使用者依刻面篩選搜尋結果。 「核 **取方塊清單Facet**」、「下拉式Facet **」和「連結清單Facet****** 」元件可讓使用者選取一或多個Facet進行篩選。 使用這些元件時，您也應包含 **Breadcrumbs元件** 。 階層連結會指出目前使用的篩選條件。

List Facet ****、Dropdown Facet **、** Link List Facet **Components每個都具有以下屬性，您可在「編輯模式」中****** 配置：

* **Facet名稱**:用於篩選器的Facet名稱。

「核 **取方塊清單Facet** 」元件會顯示Facet清單及隨附的核取方塊。 使用核取 **方塊清單Facet** ，讓使用者可以檢視包含多個Facet項目之結果的子集。 例如，品牌 **面** (Brand Facet)是適當的，因為數個品牌提供相同的產品類型。

每個與搜尋結果相關聯的Facet會出現核取方塊。 當使用者選取核取方塊時，頁面會重新載入更新的結果集。 所有核取方塊都會保留在頁面上，讓客戶可以隨時將Facet新增或移除至篩選器：

![sandpcheckboxcomp](assets/sandpcheckboxcomp.png)

「下 **拉式Facet** 」元件可讓客戶從下拉式清單中選取Facet項目。 當您希望客戶一次將注意力集中在單一Facet項目時，此元件很實用。 例如，「部門」面適合讓客戶依性別縮小產品搜尋範圍。 John先搜 *尋牛仔褲* ，然後在男裝部找濾鏡。

下拉式清單中會填入與所有搜尋結果相關聯的刻面。 在下拉式清單中選取項目時，頁面會重新載入更新的結果集。 下拉式清單中的項目不會變更，因此客戶可以隨時從Facet切換至Facet。

![sanddropdowndepartment](assets/sandpdropdowndepartment.png)

「連 **結清單Facet** 」元件可讓客戶逐步縮小對多個Facet成員或Facet下分類項目的關注。

Facet成員會以連結清單的形式顯示。 每個連結的文字是與目前搜尋結果相關聯之Facet成員的名稱。 當客戶按一下Facet連結時，頁面會重新載入，並顯示搜尋結果的子集。 相應地更新鏈路清單，使得聚焦更窄。

![sandplinklistcomp](assets/sandplinklistcomp.png)

當從不同類型的Search&amp;Promote元件套用篩選時，清單中的連結也會變更。 使用多種類型的篩選元件可提供有效的篩選組合。

Breadcrumbs **元件** ，可讓客戶依套用順序，查看目前套用至搜尋結果的篩選器。 客戶可以按一下階層連結中的項目，以回復至該篩選組合。

![sandbreadcrumbcomp](assets/sandpbreadcrumbcomp.png)

您可以在「編輯」模式中為Breadcrumbs設定下列屬性，以自訂元件的外觀：

* 分隔字元：定義字元或字元字串，作為每個階層連結之間的分隔字元。 分隔字元欄位可接受任何字元字串作為輸入。 預設設定為：&quot;>&quot;（不含引號）
* 尾隨分隔字元：定義要顯示在階層連結結尾的字元或字元字串。 「追蹤分隔字元」欄位接受任何字元字串作為輸入。 此預設設定為*blank*（亦即，階層連結行的尾端不會顯示任何內容）

### 新增搜尋方塊 {#adding-search-boxes}

搜尋元件可讓客戶執行關鍵字搜尋。 將「搜尋」元件新增至您要提供搜尋存取權的每個頁面。

在「編輯」模式中設定下列屬性，以控制執行時期行為：

* 結果頁面路徑：顯示搜尋結果之頁面的路徑。
* 啟用自動完成：選取此選項，可在客戶開始在搜尋方塊中輸入時顯示建議的搜尋關鍵字。

![sandsearchcomp](assets/sandpsearchcomp.png)

### 新增橫幅 {#adding-banners}

橫幅元件會根據客戶的Search&amp;Promote搜尋顯示橫幅廣告。 Search&amp;Replace伺服器上的邏輯會決定要顯示哪個橫幅。 例如，在牛仔褲上搜尋可能會導致出現與時尚相關的橫幅。 在男子部門過濾可以進一步細化橫幅的選擇。

Banners元件提供一個名為Banner area的可配置屬性。 在「編輯」模式中，選擇一個屬性值以指定橫幅的顯示方式。 Search&amp;Promote服務會決定您可從中選取的值清單。

### Search&amp;Promote搜尋頁面範例 {#example-search-promote-search-page}

此圖表顯示新增至頁面以建立功能完整的Search&amp;Promote結果頁面的元件。

![1328213789109](assets/1328213789109.png) ![sandppageexample](assets/sandppageexample.png)
