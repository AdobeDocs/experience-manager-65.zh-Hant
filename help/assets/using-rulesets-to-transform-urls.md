---
title: 使用規則集轉換URL
description: 您可以在動態媒體中部署規則集以轉換URL。 規則集是以指令碼語言（例如JavaScript）編寫的指令集，可評估XML資料，並在資料符合特定條件時採取特定動作。
uuid: 9fed0c83-67b7-4483-a9b4-322e6a483449
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: abcff903-204b-4ab6-87d8-6f0ce63d7b41
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 使用規則集轉換URL {#using-rulesets-to-transform-urls}

您可以在動態媒體中部署規則集以轉換URL。 規則集是以指令碼語言（例如JavaScript）編寫的指令集，可評估XML資料，並在資料符合特定條件時採取特定動作。 每個規則都包含至少一個條件和至少一個動作。 規則會根據條件評估XML資料，如果符合條件，則會採取適當的動作。 規則集的範例包括：

* 添加MIME類型尾碼。 許多服務和網站都需要影像字尾，例如 `.jpg` 新增至URL。
* 建立URL的資料夾路徑，以利搜尋引擎最佳化(SEO)。

   了 [解Adobe Scene7 Publishing system如何支援搜尋引擎最佳化](/help/assets/assets/s7_seo.pdf)。

* 新增中繼資料至URL，以利搜尋引擎最佳化(Search Engine Optimization)。

   了 [解Adobe Scene7 Publishing system如何支援搜尋引擎最佳化](/help/assets/assets/s7_seo.pdf)。

* 設定內容配置以觸發下載。
* 簡化影像伺服範本URL以利個人化。 例如，將 `rgb{XX,YY,ZZ}` RTF轉換為 `\redXX\greenYY\blueZZ`

* 請求對某些字元進行編碼( `$`如、 `{`和 `}`)，並向ImageServer解碼某些字元。 例如，Facebook在包含特殊字元的URL上無法正常運作。

   請參 [閱從URL移除特殊字元](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html)。

在Dynamic media中，使用XML系統來管理資產資訊的網站可將XML檔案上傳至Dynamic Media。 您可以指定其中一個檔案為提供動態媒體資產的預處理規則集檔案。 此檔案會重新架構標準URL通訊協定格式，以符合與Dynamic media整合之系統的商業邏輯。 您可以指定XML檔案作為規則集定義檔案路徑。

>[!CAUTION]
>
>使用規則集時請謹慎；它們可防止動態媒體內容顯示在您的網站上。

有可用的範例規則集可協助您建立自己的規則集。
請參 [閱規則集參考](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/image_catalog/c_rule_set_reference.html)。

如同建立所有規則集一樣，請使用XMLVALID等XML驗證程式，在上傳XML檔案之前，先確定其有效性。
另請參閱 [疑難排解規則集](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html)。

此外，請務必先在測試環境中測試規則集，而不會影響您的即時生產環境。
生產環境和測試環境通常需要不同的登入。

* **NA測試環境** 登錄頁： [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA測試環境** 登錄頁： [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC測試環境** 登錄頁： [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/)

另請參 [閱在規則集中使用&#39;asset&#39;而非&#39;is&#39;影像](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html)。

**要部署XML規則集：**

1. 登入您的Dynamic Media Classic帳戶：

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   您的認證和登入是在布建時由Adobe提供。 如果您沒有此資訊，請聯絡技術支援。

1. 執行下列動作，上傳規則集檔案：

   * 在全域導覽列上，按一下「上 **[!UICONTROL 傳]**」。
   * 在「上 **[!UICONTROL 傳]** 」頁面的左上角附近，按一下「 **[!UICONTROL 瀏覽」]**。
   * 在「開 **[!UICONTROL 啟]** 」對話方塊中，瀏覽至您的規則集檔案(XML)。
   * 選取檔案，然後按一下「 **[!UICONTROL 開啟]**」。
   * 在「上傳」頁面的右 **[!UICONTROL 側]** ，為規則集檔案選擇一個目標資料夾。
   * 在頁面底部附近，請確定已勾選「 **[!UICONTROL 上傳後發佈]** 」。
   * 在頁面的右下角，按一下「送出上 **[!UICONTROL 傳」]**。
   * 在全域導覽列上，按一 **[!UICONTROL 下「工作]** 」以檢查上傳工作的狀態。 當「工 **[!UICONTROL 作]** 」頁面上的「狀態」欄顯示 **[!UICONTROL 「上傳完成]** 」時，請繼續下一步驟。

1. 在頁面頂端的導覽列上，按一下「設定>應 **[!UICONTROL 用程式設定>發佈設定>影像伺服器」]**。
1. 在「映 **[!UICONTROL 像伺服器發佈]** 」頁的「目錄管理」組下，找到「規則集定義檔案路徑」 **[!UICONTROL ，然後按一下]**********「選擇」。
1. 在「選 **[!UICONTROL 擇規則集定義檔案(XML)]** 」頁上，瀏覽到規則集檔案，然後在頁的右下角按一下「選 **[!UICONTROL 擇」]**。
1. 在「設定」頁面的右下角，按一下「關 **[!UICONTROL 閉」]**。
1. 執行影像伺服器發佈工作。

   規則集條件會套用至即時動態媒體影像伺服器的請求。

   如果您對規則集檔案進行變更，在您重新上傳並重新發佈更新的規則集檔案時，會立即套用變更。

