---
title: 指定XCI配置選項
seo-title: Specifying XCI configuration options
description: 瞭解如何指定XCI配置選項。
seo-description: Learn how to specify XCI configuration options.
uuid: 5d3c10c1-4a93-4336-b311-20faaf835b9f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 162c9fda-f4d4-4ad5-a9ab-7554828e821c
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 1%

---

# 指定XCI配置選項 {#specifying-xci-configuration-options}

Forms允許您指定用於呈現的自定義XCI檔案。 (請參閱 [配置Forms的位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)。) 預設情況下，Forms會覆蓋XCI檔案中指定的一些選項，包括：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以為上面列出的選項選擇取消覆蓋的選項，在這種情況下，Forms將使用自定義XCI檔案中指定的值。

1. 在管理控制台中，按一下「服務」>「Forms」。
1. 選中或取消選擇「使用系統預設XCI選項」複選框。 選擇此選項後，Forms將其預設值用於資料包、建立者、生產者和compressObjectStream設定。 取消選擇此選項後，Forms將使用自定義XCI檔案中指定的值。
1. 按一下「儲存」。
