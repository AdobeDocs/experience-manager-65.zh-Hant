---
title: 指定XCI配置選項
seo-title: 指定XCI配置選項
description: 瞭解如何指定XCI配置選項。
seo-description: 瞭解如何指定XCI配置選項。
uuid: 5d3c10c1-4a93-4336-b311-20faaf835b9f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 162c9fda-f4d4-4ad5-a9ab-7554828e821c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 指定XCI配置選項 {#specifying-xci-configuration-options}

Forms可讓您指定自訂XCI檔案，以用於演算。 (請參 [閱設定表單位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)。)依預設，Forms會覆寫XCI檔案中指定的部分選項，包括：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以選取取消上述選項覆寫的選項，此時Forms會使用自訂XCI檔案中指定的值。

1. 在管理控制台中，按一下「服務>表單」。
1. 選中或取消選擇「使用系統預設XCI選項」複選框。 選取此選項時，Forms會針對封包、建立者、producer和compressObjectStream設定使用其預設值。 取消選取此選項時，表單會使用自訂XCI檔案中指定的值。
1. 按一下「儲存」。

