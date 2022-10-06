---
title: 轉譯資產的最佳實務
description: 高效管理資產的最佳做法，以同步各種翻譯版本並簡化翻譯工作流程。
contentOwner: AG
role: Admin
feature: Asset Management
exl-id: e632dcdb-b2b9-45bc-89e7-337b44b6fc61
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# 轉譯資產的最佳實務 {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] 支援多語言工作流程，將數位資產的二進位檔、中繼資料和標籤轉譯為多個地區設定，以及管理翻譯的資產。 如需詳細資訊，請參閱 [多語言資產](multilingual-assets.md).

為有效管理資產以確保不同翻譯版本保持同步，請建立 [語言副本](preparing-assets-for-translation.md) 執行翻譯工作流程之前取得Assets的說明。

資產或一組資產的語言副本是具有類似內容階層的語言同層級項目（或相同語言中的資產版本）。

每個語言副本都是獨立的資產。 因此，將資產轉譯為多個地區設定可大幅增加CRX存放庫的大小。 例如，將總大小為10 GB的資產轉換為兩種語言，可將存放庫大小增加約20 GB（每種語言10 GB）。

與中繼資料和標籤相比，資產二進位檔佔用的儲存空間要大得多。 因此，如果轉譯中繼資料和標籤只符合您的目的，請忽略轉譯二進位檔。 您可以保留存放庫中二進位檔的原始副本，以便與轉譯為不同地區設定的中繼資料和標籤產生關聯。 維護單一二進位檔副本（而非多個轉譯版本），可將對存放庫大小的影響降至最低。

檔案資料儲存和Amazon S3資料儲存提供了最適合這些情況的儲存基礎結構。 這些儲存存放庫會儲存資產二進位檔的單一副本（包括轉譯），這些二進位檔可由多個地區設定中的中繼資料和標籤共用。 因此，建立資產語言復本以及轉譯中繼資料和標籤不會影響存放庫大小。

您也可以對一些工作流程和翻譯整合框架進行一些配置更改，以進一步簡化流程。

1. 執行下列任一項作業：

   * [設定檔案資料儲存](/help/sites-deploying/data-store-config.md)
   * [設定Amazon S3資料存放區](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. 啟用 [!UICONTROL 設定上次修改日期] 工作流程。

   此 [!UICONTROL DAM中繼資料回寫] 工作流程會設定資產的上次修改日期。 因為您在步驟2中停用此工作流程， [!DNL Assets] 無法再將資產的最後修改日期保持為最新。 因此，請啟用 *設定上次修改日期* 工作流程，確保資產的上次修改日期為最新。 具有過時的上次修改日期的資產可能會導致錯誤。

1. [配置翻譯整合框架](/help/sites-administering/tc-tic.md) 停止轉譯資產二進位檔。 取消選取 **[!UICONTROL 轉換資產]** 選項 [!UICONTROL 資產] 標籤，停止轉譯資產二進位檔。
1. 使用 [多語言資產工作流程](multilingual-assets.md).
