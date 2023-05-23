---
title: 資產轉換的最佳做法
description: 高效管理資產的最佳做法，以同步各種翻譯版本和簡化翻譯工作流。
contentOwner: AG
role: Admin
feature: Asset Management
exl-id: e632dcdb-b2b9-45bc-89e7-337b44b6fc61
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# 資產轉換的最佳做法 {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] 支援多語言工作流，將二進位檔案、元資料和數字資產標籤轉換為多個語言環境，並管理已轉換的資產。 有關詳細資訊，請參閱 [多語言資產](multilingual-assets.md)。

為了高效地管理資產以確保不同翻譯版本保持同步，請建立 [語言副本](preparing-assets-for-translation.md) 在運行翻譯工作流之前。

資產或資產組的語言副本是具有相似內容層次結構的語言同級（或以同一語言表示的資產版本）。

每種語言副本都是獨立的資產。 因此，將資產轉換為多個區域設定可以顯著增加CRX儲存庫的大小。 例如，將總大小為10 GB的資產翻譯成兩種語言可將儲存庫大小增加大約20 GB（每種語言為10 GB）。

資產二進位檔案佔用的儲存空間比元資料和標籤大得多。 因此，如果轉換元資料和標籤僅符合您的目的，請省略以轉換二進位檔案。 您可以保留儲存庫中二進位檔案的原始副本，以便與轉換到不同語言環境的元資料和標籤關聯。 維護二進位檔案的單個副本，而不是多個已轉換的版本，可最大限度地減少對儲存庫大小的影響。

檔案資料儲存和AmazonS3資料儲存提供了最適合這些情形的儲存基礎架構。 這些儲存儲存庫儲存資產二進位檔案（包括格式副本）的單個副本，這些二進位檔案可以在多個語言環境中由元資料和標籤共用。 因此，建立資產語言副本以及轉換元資料和標籤不會影響儲存庫大小。

您還可以對兩個工作流和翻譯整合框架進行一些配置更改，以進一步簡化流程。

1. 執行下列任一項作業：

   * [設定檔案資料儲存](/help/sites-deploying/data-store-config.md)
   * [設定AmazonS3資料儲存](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. 啟用 [!UICONTROL 設定上次修改日期] 工作流。

   的 [!UICONTROL DAM元資料寫回] 工作流配置資產的上次修改日期。 因為您在步驟2中禁用了此工作流， [!DNL Assets] 不再能夠使資產的上次修改日期保持最新。 因此，啟用 *設定上次修改日期* 工作流，確保資產的上次修改日期是最新的。 具有過期的上次修改日期的資產可能會導致錯誤。

1. [配置翻譯整合框架](/help/sites-administering/tc-tic.md) 停止轉換資產二進位檔案。 取消選擇 **[!UICONTROL 轉換資產]** 選項 [!UICONTROL 資產] 頁籤，以停止Asset二進位檔案的翻譯。
1. 轉換資產元資料/標籤 [多語言資產工作流](multilingual-assets.md)。
