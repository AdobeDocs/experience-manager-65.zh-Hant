---
title: 變更字元集
seo-title: 變更字元集
description: 您可以指定用於編碼輸出流的字元集。 瞭解如何變更字元集。
seo-description: 您可以指定用於編碼輸出流的字元集。 瞭解如何變更字元集。
uuid: ecb0c3ff-368c-4553-80e4-aa35fc15af62
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 811b31f8-5465-4fb2-b1f9-513936041771
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 變更字元集 {#change-the-character-set}

您可以指定用於編碼輸出流的字元集。

1. 在管理控制台中，按一下「 **[!UICONTROL 服務>輸出」]**。
1. 在「國際化」下的「字元集」清單中，選擇一個字元集。 此設定取決於透過API `TransformationFormat` 指 `PrintFormat` 定的和。 要指定列出的字元集以外的字元集，請選擇「自定義」並在顯示的框中指定編碼值。

   如果 `TransformationFormat` 是PDF和PDF/A或 `PrintFormat` 是PCL、PostScript、Zebra標籤、IPL、DPL、TPCL、GenericColorPCL或GenericPSLevel3，則只支援特定字元集。

   字元集必須是有效的標準名稱。 預設值為ISO-8859-1。

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

