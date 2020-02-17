---
title: 支援IPTC中繼資料
description: 瞭解Adobe Experience Manager(AEM)Assets如何透過Adobe bridge和其他Creative Apps支援IPTC中繼資料、創意評分和新增至資產的關鍵字。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# 支援IPTC中繼資料 {#support-for-iptc-metadata}

瞭解Adobe Experience Manager(AEM)Assets如何透過Adobe bridge和其他Creative Apps支援IPTC中繼資料、創意評分和新增至資產的關鍵字。

Adobe Experience Manager(AEM)Assets支援IPTC中繼資料標準，此標準廣泛用於描述資產。 如此，AEM Assets就可增強各方對其影像的接受度，包括攝影師、創意廣告公司、圖書館、博物館等。

資產的預設中繼資料結構現在整合了IPTC核心和IPTC擴充功能中繼資料結構，以定義完整的中繼資料屬性，讓使用者新增有關影像中顯示之人物、位置和產品的精確可靠資料。 它也支援建立影像的日期、名稱和識別碼，並提供彈性的方式來表達權限資訊。

資產的「屬性」頁面現在包含個別的標籤，可在可編輯欄位中顯示「IPTC核心」和「IPTC擴充功能」中繼資料。

1. 從「資產」使用者介面中，選取影像。
1. 從工具 **[!UICONTROL 列點選]** 「屬性」。
1. 點選「 **[!UICONTROL IPTC]** 」標籤以檢視資產的IPTC中繼資料。
1. 視需要編輯IPTC中繼資料屬性。

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. 按一下／點選「 **[!UICONTROL IPTC擴充功能」標籤]** ，以檢視資產的IPTC擴充功能中繼資料。
1. 視需要編輯IPTC Extension中繼資料屬性。
1. 點選／按一 **[!UICONTROL 下「儲存並關閉]** 」以儲存變更。

## 創意評分支援 {#creative-rating-support}

除了顯示個別使用者分級和匯總分級外，「屬性」頁面現在還會顯示透過Adobe bridge和其他Creative Apps指派給資產的分級

這些評等可在「進階」標 **[!UICONTROL 簽的「創作評分]** 」區段 **[!UICONTROL 下取得]** 。

此分級是唯讀屬性，範圍介於1-5之間。 您可以從「搜尋面板」根據資產的「創意評分」來搜尋資產。

不過，此屬性目前未建立索引，以避免與使用者所做的自訂變更產生任何衝突。

## 關鍵字支援 {#keyword-support}

「屬 **[!UICONTROL 性」頁面的]** 「IPTC  」索引標籤也會顯示透過Adobe bridge和其他Adobe Creative cloud應用程式新增至資產的關鍵字。 您也可以編輯這些關鍵字，並從「 **[!UICONTROL IPTC」索引標籤新增更多關]** 鍵字。

![關鍵字](assets/keywords-in-iptc-tab.png)
