---
title: 在[!DNL Adobe Experience Manager Assets]中使用IPTC中繼資料。
description: 瞭解[!DNL Adobe Experience Manager Assets]如何支援透過Adobe Bridge和其他Creative Apps新增至資產的IPTC中繼資料、創意評分和關鍵字。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 使用IPTC中繼資料 {#support-for-iptc-metadata}

瞭解如何 [!DNL Adobe Experience Manager Assets] 支援透過和其他應用程式新增至資產的IPTC中繼資料、創意評 [!DNL Adobe Bridge] 分和關 [!DNL Adobe Creative Cloud] 鍵字。

[!DNL Adobe Experience Manager Assets] 支援廣泛用於描述資產的IPTC中繼資料標準。 如此， [!DNL Assets] 就可提高攝影師、創意廣告公司、圖書館、博物館等各方對影像的接受度。

資產的預設中繼資料結構現在整合了IPTC核心和IPTC擴充功能中繼資料結構，以定義完整的中繼資料屬性，讓使用者新增有關影像中顯示之人物、位置和產品的精確可靠資料。 它也支援建立影像的日期、名稱和識別碼，並提供彈性的方式來表達權限資訊。

資產的「屬性」頁面現在包含個別的標籤，可在可編輯欄位中顯示「IPTC核心」和「IPTC擴充功能」中繼資料。

1. 從使用者 [!DNL Assets] 介面中，選取影像。
1. 從工具 **[!UICONTROL 列按一下]** 「屬性」。
1. 按一下 **[!UICONTROL IPTC]** 標籤，以檢視資產的IPTC中繼資料。
1. 視需要編輯IPTC中繼資料屬性。

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. Click the **[!UICONTROL IPTC Extension]** tab to view IPTC Extension metadata for the asset.
1. 視需要編輯IPTC Extension中繼資料屬性。
1. Click **[!UICONTROL Save &amp; Close]** to save the changes.

## 創意評分支援 {#creative-rating-support}

除了顯示個別使用者分級和匯總分級外，「屬性」頁面現在還會顯示透過Adobe Bridge和其他Creative Apps指派給資產的分級

這些評等可在「進階」標 **[!UICONTROL 簽的「創作評分]** 」區段 **[!UICONTROL 下取得]** 。

此分級是唯讀屬性，範圍介於1-5之間。 您可以從「搜尋面板」根據資產的「創意評分」來搜尋資產。

不過，此屬性目前未建立索引，以避免與使用者所做的自訂變更產生任何衝突。

## 關鍵字支援 {#keyword-support}

「屬 **[!UICONTROL 性」頁面的]** 「IPTC  」索引標籤也會顯示透過Adobe Bridge和其他Adobe Creative Cloud應用程式新增至資產的關鍵字。 您也可以編輯這些關鍵字，並從「 **[!UICONTROL IPTC」索引標籤新增更多關]** 鍵字。

![關鍵字](assets/keywords-in-iptc-tab.png)
