---
title: 指定XCI組態選項
description: 瞭解如何指定XCI設定選項。 您可以為最適化表單指定自訂XCI檔案值，以便在表單轉譯時使用該值。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 1%
---
# 指定XCI組態選項 {#specifying-xci-configuration-options}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

Forms可讓您指定其可用於轉譯的自訂XCI檔案。 （請參閱[設定Forms的位置](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)。） 依預設，Forms會覆寫XCI檔案中指定的某些選項，包括下列專案：

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

您可以選取取消上述選項覆寫的選項，在此情況下，Forms會使用自訂XCI檔案中指定的值。

1. 在管理控制檯中，按一下&#x200B;**服務** > **Forms**。
1. 選取或取消選取使用系統預設XCI選項核取方塊。 選取此選項時，Forms會使用封包、建立者、製作者和compressObjectStream設定的預設值。 取消選取此選項時，Forms會使用自訂XCI檔案中指定的值。
1. 按一下&#x200B;**儲存**。
