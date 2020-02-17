---
title: 指定XCI配置選項
seo-title: 指定XCI配置選項
description: 瞭解如何指定XCI配置選項。
seo-description: 瞭解如何指定XCI配置選項。
uuid: cf9e544d-63cd-4fad-8f89-bdb46eeef409
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f38ebd69-8d1c-49b6-824f-4bf0ec8a8953
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 指定XCI配置選項 {#specify-xci-configuration-options}

Output可讓您指定自訂XCI檔案，供其用於轉譯。 (請參 [閱指定輸出的檔案位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)。)依預設，「輸出」會覆寫XCI檔案中指定的部分選項，包括：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以選取取消上述選項覆寫的選項，此時「輸出」會使用自訂XCI檔案中指定的值。

1. 在管理控制台中，按一下「服務>輸出」。
1. 選中或取消選擇「使用系統預設XCI選項」複選框。 選取此選項時，「輸出」會針對封包、建立者、生產者和compressObjectStream設定使用其預設值。 取消選取此選項時，「輸出」會使用自訂XCI檔案中指定的值。
1. 按一下「儲存」。

