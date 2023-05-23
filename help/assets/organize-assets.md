---
title: 組織您的數位資產
description: 使用Experience Manager組織您的數字資產、影像、檔案、資料夾等。
contentOwner: AG
role: User
feature: Asset Management,Search
exl-id: d6f815b5-e4fc-4f8c-a6c1-9e50035ab9f2
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 2%

---

# 組織您的數位資產 {#organize-digital-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/organize-assets.html?lang=en) |
| AEM 6.5 | 本文 |

Microsoft辦事處和PDF檔案的所有數字資產、元資料和內容都被提取並可供搜索。 搜索允許對資產進行複雜的過濾，並完全尊重適當的權限。 元資料在數字資產管理的元資料中作了詳細介紹。

[!DNL Experience Manager Assets] 支援多種組織內容的方法。 可以使用資料夾以分層方式組織它們，或者可以使用例如標籤以無序即席方式組織它們。 用戶可以在DAM資產編輯器中編輯標籤，其中顯示子資產、格式副本和元資料。

## 在資料夾中組織資產 {#organize-using-folders}

組織資產的最基本方法是將這些資產保存在資料夾中。 它類似於在本地檔案系統中的資料夾中組織檔案。 有關如何建立和管理資料夾的詳細資訊，請參見 [管理資產](manage-assets.md)。 如何命名檔案和資料夾、如何排列子資料夾以及如何處理這些資料夾中的檔案都會對處理這些資產的方式產生重大影響。 通過使用一致且適當的檔案和資料夾命名策略以及良好的元資料做法，您可以充分利用數字資產儲存庫。

* 在大多數情況下，您的數字資產儲存庫始終在增長。 因此，在內容建立週期的早期就對元資料的使用、資料夾結構和檔案命名進行規範非常重要。
* 僅使用資料夾為您的數字資產強加一致的儲存結構。 此一致性有助於您的流程和更好地管理資產。 例如，放置在以下類型的資料夾中的資產可以幫助您使用適當的 [配置檔案用於資產處理](processing-profiles.md):

   * **開發資料夾**:包含您當前正在處理的數字資產。
   * **客戶端資料夾**:包含基於客戶端或項目名稱的數字資產。
   * **主資料夾**:包含原始的源數字資產。
   * **格式副本資料夾**:包含原始源數字資產的格式副本和副本。
   * **檔案大小資料夾**:包含基於小、中或大檔案大小的數字資產。
   * **暫存資料夾**:包含已準備好在您的網站上即時發佈的數字資產。
   * **MIME類型資料夾**:包含特定於MIME類型的數字資產，如影像、文檔和多媒體。
   * **存檔資料夾**:包含已停用的數字資產。
   * **基於日期的資料夾**:包含基於建立日期或上次修改日期的數字資產。

* 建立不太可能更改的資料夾目錄，以便任何自定義或自動化都繼續工作。 例如，已分配的處理配置檔案繼續工作。
* 如果已發佈資產，則使用 [!DNL Experience Manager] 要將資產移動到另一個資料夾並從其新位置重新發佈，原始發佈的資產位置以及新重新發佈的資產仍然可用。 但是，原始發佈的資產是 *失* 至 [!DNL Experience Manager] 不能不發表。 因此，作為最佳做法，首先取消發佈資產，然後將其移動到其他資料夾。

## 使用標籤組織資產 {#use-tags-to-organize-assets}

使用標籤作為元資料，您可以輕鬆搜索資產、使用搜索結果建立集合、提高某些資產的搜索排名，並利用Adobe Sensei的AI算法進行資產發現。

[!DNL Adobe Experience Manager Assets] 使用自學習算法建立高度描述性的標籤，使您只需按一下幾下即可找到合適的資產。 智慧標籤使用Adobe Sensei，我們的人工智慧和機器學習框架，可以訓練它識別和應用標準標籤和特定於業務的標籤到影像。 智慧標籤還可以識別內容、單個詞或短語，並自動將描述性標籤應用於資產

有關詳細資訊，請參閱以下文章：

* [關於Experience Manager中的標籤](/help/sites-authoring/tags.md)
* [編輯資產元資料](metadata.md)
* [增強的資產智慧標籤](enhanced-smart-tags.md)

## 組織為集合 {#organize-as-collections}

將資產收集 [!DNL Experience Manager Assets]，您可以簡化用戶之間建立、編輯和共用資產的功能。 根據使用方式建立多種類型的集合，包括包含資產、資料夾和集合的靜態引用清單的集合，以及根據搜索標準納入資產的集合。  您還可以使用不同位置的資產建立集合，並與具有不同訪問、查看和編輯權限級別的多個用戶共用這些集合。

有關詳細資訊，請參見 [管理集合](manage-collections.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## 組織資產以使用配置檔案 {#organize-to-use-profiles}

處理配置檔案包含 [!DNL Assets] 正在處理適用於上載到預定義資料夾的資產的命令。 配置檔案用於自動處理資料夾或新上載的資產的內容。 您可以利用配置檔案來更好地組織資產。

標準化元資料使用、檔案命名和資料夾結構可確保隨著數字資產池的增長，您可以以更高的精確度和一致性將處理配置檔案應用於資料夾。

>[!MORELIKETHIS]
>
>* [處理元資料、影像和視頻的配置檔案](processing-profiles.md)。
>* [中繼資料設定檔](/help/assets/metadata-config.md#metadata-profiles).
>* [視頻配置檔案](video-profiles.md)。
>* [Dynamic Media影像配置檔案](image-profiles.md)。

