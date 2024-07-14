---
title: 指定XCI設定選項
description: 瞭解如何指定XCI設定選項。 您可以為最適化表單指定自訂XCI檔案值，以便在表單轉譯時使用該值。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---

# 指定XCI設定選項 {#specify-xci-configuration-options}

輸出可讓您指定其用於呈現的自訂XCI檔案。 請參閱[指定輸出](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)的檔案位置。

依預設，「輸出」會覆寫XCI檔案中指定的某些選項，包括：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以選取取消上述選項覆寫的選項，在這種情況下「輸出」會使用自訂XCI檔案中指定的值。

1. 在管理主控台中，按一下&#x200B;**服務** >輸出。
1. 選取或取消選取使用系統預設XCI選項核取方塊。 選取此選項時，Output會使用封包、建立者、製作者和compressObjectStream設定的預設值。 取消選取此選項時，輸出使用自訂XCI檔案中指定的值。
1. 按一下「**儲存**」。
