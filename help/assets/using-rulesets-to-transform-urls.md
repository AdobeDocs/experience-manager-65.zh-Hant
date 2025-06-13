---
title: 使用規則集轉換 URL
description: 您可以在Dynamic Media中部署規則集以轉換URL。 規則集是以指令碼語言(例如JavaScript)撰寫的指令集，可評估XML資料並在該資料符合特定條件時採取特定動作。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin,Developer
exl-id: b0ac587b-8592-4d37-9ce0-98a0859c367f
feature: Configuration,Rulesets
solution: Experience Manager, Experience Manager Assets
source-git-commit: 0b90fdd13efc5408ef94ee1966f04a80810b515e
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# 使用規則集轉換URL {#using-rulesets-to-transform-urls}

您可以在Dynamic Media中部署規則集以轉換URL。 規則集是以指令碼語言(例如JavaScript)撰寫的指令集，可評估XML資料並在該資料符合特定條件時採取特定動作。 每個規則至少包含一個條件和至少一個動作。 規則會根據條件評估XML資料，如果符合條件，則會採取適當的動作。 規則集的範例包括：

* 新增MIME型別字尾。 許多服務和網站都需要影像尾碼，例如將`.jpg`新增至URL。
* 針對SEO （搜尋引擎最佳化）目的建立URL的資料夾路徑。

  請參閱[Adobe Dynamic Media Classic如何支援SEO](/help/assets/assets/s7_seo.pdf)。

* 將中繼資料新增至URL以用於SEO （搜尋引擎最佳化）用途。

  請參閱[Adobe Dynamic Media Classic如何支援SEO](/help/assets/assets/s7_seo.pdf)。

* 設定內容處置以觸發下載。
* 簡化影像伺服範本URL以進行個人化。 例如，將`rgb{XX,YY,ZZ}`轉換為RTF就緒的`\redXX\greenYY\blueZZ`

* 要求將某些字元（例如`$`、`{`和`}`）編碼，並將某些字元解碼為ImageServer。 例如，Facebook無法順利處理包含特殊字元的URL。

在Dynamic Media中，使用XML系統管理資產資訊的網站可將XML檔案上傳至Dynamic Media。 您可以將其中一個檔案指定為預先處理規則集檔案，以提供Dynamic Media資產。 此檔案會重新建構標準URL通訊協定格式，以符合與Dynamic Media整合之系統的商業邏輯。 您可以指定XML檔案做為規則集定義檔案路徑。

>[!CAUTION]
>
>使用規則集時請務必小心，因為規則集可能會導致Dynamic Media內容無法在您的網站上顯示。

有些範例規則集可幫助您建立自己的規則集。
請參閱[規則集參考](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference)。

與建立所有規則集時一樣，使用XML驗證器程式（例如xmlvalid）來上傳XML檔案之前，請確定該檔案有效。

此外，請務必先在中繼環境中測試規則集，以免影響您的即時生產環境。
生產環境和測試環境通常需要不同的登入。

如需登入資訊，請參閱[Adobe Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/getting-started/signing-out#sign-in-dmc-app)。

<!-- OBSOLETE INFORMATION * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

**若要部署XML規則集：**

1. 登入您的[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/getting-started/signing-out#sign-in-dmc-app)。

   布建時Adobe已提供您的憑證和登入詳細資訊。 如果您沒有這項資訊，請聯絡Adobe客戶支援。

1. 執行下列操作上傳規則集檔案：

   * 在全域導覽列上，選取&#x200B;**[!UICONTROL 上傳]**。
   * 在&#x200B;**[!UICONTROL 上傳]**&#x200B;頁面的左上角附近，選取&#x200B;**[!UICONTROL 瀏覽]**。
   * 在&#x200B;**[!UICONTROL 開啟]**&#x200B;對話方塊中，瀏覽至您的規則集檔案(XML)。
   * 選取檔案，然後選取&#x200B;**[!UICONTROL 開啟]**。
   * 在&#x200B;**[!UICONTROL 上傳]**&#x200B;頁面的右側，選取規則集檔案的目標資料夾。
   * 在接近頁面底部時，請確定已核取&#x200B;**[!UICONTROL 上傳後發佈]**。
   * 在頁面的右下角，選取&#x200B;**[!UICONTROL 送出上傳]**。
   * 在全域導覽列上，選取&#x200B;**[!UICONTROL 工作]**&#x200B;以檢查上載工作的狀態。 當&#x200B;**[!UICONTROL 工作]**&#x200B;頁面上的&#x200B;**[!UICONTROL 狀態]**&#x200B;資料行顯示「上載完成」時，請繼續後續步驟。

1. 在靠近頁面頂端的導覽列上，選取&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 發佈設定]** > **[!UICONTROL 影像伺服器]**。
1. 在&#x200B;**[!UICONTROL 影像伺服器發佈]**&#x200B;頁面的&#x200B;**[!UICONTROL 目錄管理]**&#x200B;群組下，找到&#x200B;**[!UICONTROL 規則集定義檔案路徑]**，然後選取&#x200B;**[!UICONTROL 選取]**。
1. 在&#x200B;**[!UICONTROL 選取規則集定義檔案(XML)]**&#x200B;頁面上，瀏覽至您的規則集檔案，然後在頁面的右下角選取&#x200B;**[!UICONTROL 選取]**。
1. 在[設定]頁面的右下角，選取&#x200B;**[!UICONTROL 關閉]**。
1. 執行影像伺服器發佈工作。

   規則集條件會套用到即時Dynamic Media影像伺服器的要求。

   如果您變更規則集檔案，當您重新上傳並重新發佈更新的規則集檔案時，變更會立即套用。
