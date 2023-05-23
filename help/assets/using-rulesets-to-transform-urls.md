---
title: 使用規則集轉換 URL
description: 可以在Dynamic Media部署規則集以轉換URL。 規則集是用指令碼語言（如JavaScript）編寫的一組指令，用於評估XML資料，並在資料滿足特定條件時採取特定操作。
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

# 使用規則集轉換URL {#using-rulesets-to-transform-urls}

可以在Dynamic Media部署規則集以轉換URL。 規則集是用指令碼語言（如JavaScript）編寫的一組指令，用於評估XML資料，並在資料滿足特定條件時採取特定操作。 每個規則包括至少一個條件和至少一個操作。 規則根據條件評估XML資料，如果滿足條件，則採取相應的操作。 規則集示例包括：

* 添加MIME類型尾碼。 許多服務和網站需要映像尾碼，如添加 `.jpg` 的子菜單。
* 為SEO（搜索引擎優化）目的建立指向URL的資料夾路徑。

   請參閱 [Adobe Dynamic Media Classic如何支援SEO](/help/assets/assets/s7_seo.pdf)。

* 將元資料添加到URL以用於SEO（搜索引擎優化）。

   請參閱 [Adobe Dynamic Media Classic如何支援SEO](/help/assets/assets/s7_seo.pdf)。

* 設定內容處置以觸發下載。
* 簡化影像服務模板URL以實現個性化。 例如， `rgb{XX,YY,ZZ}` RTF就緒 `\redXX\greenYY\blueZZ`

* 請求某些要編碼的字元，例如 `$`。 `{`, `}`，以及某些要向ImageServer解碼的字元。 例如，Facebook在包含特殊字元的URL上不能正常工作。

   請參閱 [從URL中刪除特殊字元](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html)。

在Dynamic Media的背景下，使用基於XML的系統管理資產資訊的網站可以將XML檔案上傳到Dynamic Media。 您可以將其中一個檔案指定為預處理規則集檔案，用於為Dynamic Media資產提供服務。 該檔案重構了標準URL協定格式，以滿足與Dynamic Media整合的系統的業務邏輯。 指定XML檔案作為規則集定義檔案路徑。

>[!CAUTION]
>
>使用規則集時要小心；它們可以阻止Dynamic Media內容在你的網站上顯示。

有示例規則集可幫助您建立自己的規則集。
請參閱 [規則集引用](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html)。

與建立所有規則集一樣，請確保XML檔案在使用XML驗證程式（如xmlvalid）上載它之前有效。
另請參閱 [排除規則集故障](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html)。

另外，請確保首先在不影響即時生產環境的轉移環境中test規則集。
生產環境和過渡環境通常需要不同的登錄名。

查看 [Adobe Dynamic Media Classic案頭應用程式，用於登錄資訊](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app)。

<!-- OBSOLETE INFORMATION * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

另請參閱 [在規則集中使用「asset」而不是「is」影像](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html)。

**要部署XML規則集：**

1. 登錄到 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app)。

   您的憑據和登錄詳細資訊是在設定時由Adobe提供的。 如果您沒有此資訊，請與Adobe客戶支援聯繫。

1. 通過執行以下操作上載規則集檔案：

   * 在全局導航欄上，選擇 **[!UICONTROL 上載]**。
   * 在 **[!UICONTROL 上載]** 頁，靠近左上角，選擇 **[!UICONTROL 瀏覽]**。
   * 在 **[!UICONTROL 開啟]** 對話框，瀏覽到規則集檔案(XML)。
   * 選擇檔案，然後選擇 **[!UICONTROL 開啟]**。
   * 在右側 **[!UICONTROL 上載]** 的子菜單。
   * 靠近頁面底部，確保 **[!UICONTROL 上載後發佈]** 的子菜單。
   * 在頁面的右下角，選擇 **[!UICONTROL 提交上載]**。
   * 在全局導航欄上，選擇 **[!UICONTROL 作業]** 以檢查上載作業的狀態。 當 **[!UICONTROL 狀態]** 列 **[!UICONTROL 作業]** 頁面顯示「Upload Done（上載完成）」 ，繼續執行後續步驟。

1. 在頁面頂部附近的導航欄上，選擇 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 發佈設定]** > **[!UICONTROL 映像伺服器]**。
1. 在 **[!UICONTROL 映像伺服器發佈]** 的子菜單。 **[!UICONTROL 目錄管理]** 組，查找 **[!UICONTROL 規則集定義檔案路徑]**，然後選擇 **[!UICONTROL 選擇]**。
1. 在 **[!UICONTROL 選擇規則集定義檔案(XML)]** 頁面，瀏覽到規則集檔案，然後在頁面的右下角選擇 **[!UICONTROL 選擇]**。
1. 在「設定」頁面的右下角，選擇 **[!UICONTROL 關閉]**。
1. 運行Image Server發佈作業。

   規則集條件應用於即時Dynamic Media映像伺服器的請求。

   如果更改了規則集檔案，則在重新上載和重新發佈更新的規則集檔案時，將立即應用更改。
