---
title: 翻譯資產的最佳實務
description: 有效管理資產的最佳實務，以同步各種翻譯版本並簡化翻譯工作流程。
contentOwner: AG
role: Admin
feature: Asset Management
exl-id: e632dcdb-b2b9-45bc-89e7-337b44b6fc61
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# 翻譯資產的最佳實務 {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets]支援多語言工作流程，以將數位資產的二進位檔、中繼資料和標籤翻譯成多個地區設定，以及管理翻譯的資產。 如需詳細資訊，請參閱[多語言Assets](multilingual-assets.md)。

為了有效管理資產，以確保不同的翻譯版本保持同步，在執行翻譯工作流程之前，請先建立資產的[語言副本](preparing-assets-for-translation.md)。

資產或資產群組的語言副本是具有類似內容階層的語言同層級（或相同語言的資產版本）。

每個語言副本都是獨立的資產。 因此，將資產轉譯為多個地區設定會大幅增加CRX存放庫的大小。 例如，將大小總和為10 GB的資產翻譯成兩種語言，可讓存放庫大小增加約20 GB （每種語言增加10 GB）。

和中繼資料和標籤相比，資產二進位檔所佔用的儲存空間要大得多。 因此，如果轉譯中繼資料和標籤只符合您的用途，請省略轉譯二進位檔案。 您可以保留儲存庫中二進位檔的原始復本，以便與翻譯成不同地區設定的中繼資料和標籤產生關聯。 維護二進位檔的單一副本（而不是多個翻譯版本），可將對存放庫大小的影響降至最低。

檔案資料存放區和Amazon S3資料存放區提供最適合這些情況的儲存基礎架構。 這些存放庫會儲存單一的資產二進位檔復本（包括轉譯），可供多個區域設定中的中繼資料和標籤共用。 因此，建立資產語言副本並翻譯中繼資料和標籤不會影響存放庫大小。

您也可以對幾個工作流程和翻譯整合框架進行一些設定變更，以進一步簡化程式。

1. 執行下列任一項作業：

   * [設定檔案資料存放區](/help/sites-deploying/data-store-config.md)
   * [設定Amazon S3資料存放區](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. 啟用[!UICONTROL 設定上次修改日期]工作流程。

   [!UICONTROL DAM MetaData回寫]工作流程會設定資產的最後修改日期。 由於您在步驟2中停用此工作流程，[!DNL Assets]無法再將資產的上次修改日期維持在最新狀態。 因此，請啟用&#x200B;*設定上次修改日期*&#x200B;工作流程，以確保資產的上次修改日期是最新的。 Assets如果包含過時的上次修改日期，可能會導致錯誤。

1. [設定轉譯整合架構](/help/sites-administering/tc-tic.md)以停止轉譯資產二進位檔。 取消選取[!UICONTROL Assets]標籤下的&#x200B;**[!UICONTROL 翻譯Assets]**&#x200B;選項，以停止翻譯資產二進位檔案。
1. 使用[多語言資產工作流程](multilingual-assets.md)翻譯資產中繼資料/標籤。
