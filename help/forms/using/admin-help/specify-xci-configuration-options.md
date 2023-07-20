---
title: 指定XCI設定選項
description: 瞭解如何指定XCI設定選項。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 1%

---

# 指定XCI設定選項 {#specify-xci-configuration-options}

輸出可讓您指定用於呈現的自訂XCI檔案。 另請參閱 [指定輸出的檔案位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

依預設，「輸出」會覆寫XCI檔案中指定的某些選項，包括：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以選取取消上述選項覆寫的選項，在這種情況下「輸出」會使用自訂XCI檔案中指定的值。

1. 在管理控制檯中，按一下 **服務** >輸出。
1. 選取或取消選取「使用系統預設XCI選項」核取方塊。 選取此選項時，Output會使用封包、建立者、製作者和compressObjectStream設定的預設值。 取消選取此選項時，輸出會使用自訂XCI檔案中指定的值。
1. 按一下「**儲存**」。
