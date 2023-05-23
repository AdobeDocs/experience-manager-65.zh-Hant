---
title: 指定XCI配置選項
seo-title: Specify XCI configuration options
description: 瞭解如何指定XCI配置選項。
seo-description: Learn how to specify XCI configuration options.
uuid: cf9e544d-63cd-4fad-8f89-bdb46eeef409
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f38ebd69-8d1c-49b6-824f-4bf0ec8a8953
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 1%

---

# 指定XCI配置選項 {#specify-xci-configuration-options}

通過輸出，可以指定用於呈現的自定義XCI檔案。 (請參閱 [為輸出指定檔案位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)。) 預設情況下，「輸出」會覆蓋XCI檔案中指定的一些選項，包括：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以為上面列出的選項選擇取消覆蓋的選項，在這種情況下，「輸出」使用在自定義XCI檔案中指定的值。

1. 在管理控制台中，按一下「服務」>「輸出」。
1. 選中或取消選擇「使用系統預設XCI選項」複選框。 選中此選項後，Output將其預設值用於資料包、建立者、生產者和compressObjectStream設定。 取消選中此選項後，「輸出」將使用自定義XCI檔案中指定的值。
1. 按一下「儲存」。
