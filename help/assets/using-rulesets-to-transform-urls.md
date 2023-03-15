---
title: 使用規則集轉換 URL
description: 您可以在Dynamic Media中部署規則集以轉換URL。 規則集是以指令碼語言（如JavaScript）編寫的一組指令，這些指令可評估XML資料，並在資料滿足某些條件時採取某些操作。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin,Developer
exl-id: b0ac587b-8592-4d37-9ce0-98a0859c367f
feature: Configuration,Rulesets
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# 使用規則集來轉換URL {#using-rulesets-to-transform-urls}

您可以在Dynamic Media中部署規則集以轉換URL。 規則集是以指令碼語言（如JavaScript）編寫的一組指令，這些指令可評估XML資料，並在資料滿足某些條件時採取某些操作。 每個規則至少包含一個條件和至少一個動作。 規則會根據條件評估XML資料，如果符合條件，則會採取適當的動作。 規則集的範例包括：

* 添加MIME類型尾碼。 許多服務和網站都需要影像尾碼，例如新增 `.jpg` 至URL。
* 為SEO（搜尋引擎最佳化）目的建立URL的資料夾路徑。

   請參閱 [Adobe Dynamic Media Classic如何支援SEO](/help/assets/assets/s7_seo.pdf).

* 為SEO（搜尋引擎最佳化）目的，將中繼資料新增至URL。

   請參閱 [Adobe Dynamic Media Classic如何支援SEO](/help/assets/assets/s7_seo.pdf).

* 設定內容配置以觸發下載。
* 簡化影像提供範本URL以供個人化。 例如， `rgb{XX,YY,ZZ}` RTF就緒 `\redXX\greenYY\blueZZ`

* 請求要編碼的特定字元，例如 `$`, `{`，和 `}`，以及要解碼到ImageServer的某些字元。 例如，Facebook在包含特殊字元的URL上無法正常運作。

   請參閱 [從URL中移除特殊字元](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

在Dynamic Media中，使用XML型系統來管理資產資訊的網站可將XML檔案上傳至Dynamic Media。 您可以指定其中一個檔案作為為Dynamic Media資產提供服務的預先處理規則集檔案。 此檔案會重新建構標準URL通訊協定格式，以符合與Dynamic Media整合之系統的業務邏輯。 指定XML檔案作為規則集定義檔案路徑。

>[!CAUTION]
>
>使用規則集時請小心；它們可防止Dynamic Media內容顯示在您的網站上。

有可用的規則集範例可協助您建立自己的規則集。
請參閱 [規則集參考](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

與建立所有規則集時一樣，在使用XMLVALID等XML驗證程式來上載XML檔案之前，請確保XML檔案有效。
另請參閱 [疑難排解規則集](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

此外，請務必先在測試環境中測試規則集，以免影響您的即時生產環境。
生產環境和測試環境通常需要不同的登入。

請參閱 [Adobe Dynamic Media Classic案頭應用程式登入資訊](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!-- OBSOLETE INFORMATION * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

另請參閱 [在規則集中使用「asset」而非「is」影像](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

**要部署XML規則集，請執行以下操作：**

1. 登入 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

   配置時，Adobe提供了您的憑據和登錄詳細資訊。 如果您沒有此資訊，請聯絡Adobe客戶支援。

1. 執行下列動作，上傳規則集檔案：

   * 在全局導航欄上，選擇 **[!UICONTROL 上傳]**.
   * 在 **[!UICONTROL 上傳]** 頁面，在左上角附近，選取 **[!UICONTROL 瀏覽]**.
   * 在 **[!UICONTROL 開啟]** 對話框，瀏覽到規則集檔案(XML)。
   * 選取檔案，然後選取 **[!UICONTROL 開啟]**.
   * 在 **[!UICONTROL 上傳]** 頁，為規則集檔案選擇目標資料夾。
   * 在頁面底部附近，確定 **[!UICONTROL 上傳後發佈]** 已勾選。
   * 在頁面的右下角，選取 **[!UICONTROL 提交上傳]**.
   * 在全局導航欄上，選擇 **[!UICONTROL 工作]** 來檢查上傳作業的狀態。 當 **[!UICONTROL 狀態]** 欄 **[!UICONTROL 工作]** 頁面顯示「上傳完成」，請繼續下列步驟。

1. 在頁面頂端附近的導覽列上，選取 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 發佈設定]** > **[!UICONTROL 影像伺服器]**.
1. 在 **[!UICONTROL 影像伺服器發佈]** 頁面下方 **[!UICONTROL 目錄管理]** 群組，找出 **[!UICONTROL 規則集定義檔案路徑]**，然後選取 **[!UICONTROL 選擇]**.
1. 在 **[!UICONTROL 選擇規則集定義檔案(XML)]** 頁，瀏覽到規則集檔案，然後在頁的右下角，選擇 **[!UICONTROL 選擇]**.
1. 在「設定」頁面的右下角，選取 **[!UICONTROL 關閉]**.
1. 運行映像伺服器發佈作業。

   規則集條件會套用至即時Dynamic Media影像伺服器的要求。

   如果您變更規則集檔案，當您重新上傳和重新發佈更新的規則集檔案時，會立即套用變更。
