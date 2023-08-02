---
title: 指定XCI組態選項
description: 瞭解如何指定XCI設定選項。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
source-git-commit: f0dd1ac3ab9c17a8b331f5048d84ec97dd23924f
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 1%

---

# 指定XCI組態選項 {#specifying-xci-configuration-options}

Forms可讓您指定其可用於轉譯的自訂XCI檔案。 (請參閱 [設定Forms的位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) 依預設，Forms會覆寫XCI檔案中指定的某些選項，包括下列專案：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以選取取消上述選項覆寫的選項，在此情況下，Forms會使用自訂XCI檔案中指定的值。

1. 在管理控制檯中，按一下 **服務** > **Forms**.
1. 選取或取消選取使用系統預設XCI選項核取方塊。 選取此選項時，Forms會使用封包、建立者、製作者和compressObjectStream設定的預設值。 取消選取此選項時，Forms會使用自訂XCI檔案中指定的值。
1. 按一下「**儲存**」。
