---
title: 組織您的數位資產
description: 使用Experience Manager組織您的數位資產、影像、檔案、資料夾等。
contentOwner: AG
role: User
feature: Asset Management,Search
exl-id: d6f815b5-e4fc-4f8c-a6c1-9e50035ab9f2
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 2%

---

# 組織您的數位資產 {#organize-digital-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/organize-assets.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/organize-assets.html?lang=en) |

擷取Microsoft Office和PDF檔案的所有數位資產、中繼資料和內容，並供搜尋。 搜尋可針對資產進行精密的篩選，並完全尊重適當的權限。 數位資產管理的中繼資料將詳細說明中繼資料。

[!DNL Experience Manager Assets] 支援多種組織內容的方式。 您可以使用資料夾以階層方式組織資料夾，或使用標籤等方式，以無序、隨選的方式組織資料夾。 使用者可以在DAM Asset Editor中編輯標籤，以顯示子資產、轉譯和中繼資料。

## 在資料夾中組織資產 {#organize-using-folders}

組織資產的最基本方式是將這些資產儲存在資料夾中。 它類似於在本地檔案系統中組織資料夾中的檔案。 有關如何建立和管理資料夾的詳細資訊，請參見 [管理資產](manage-assets.md). 如何命名檔案和資料夾、如何排列子資料夾，以及如何處理這些資料夾內的檔案，都會對處理這些資產的方式產生重大影響。 透過使用一致且適當的檔案和資料夾命名策略，以及良好的中繼資料實務，您可以充份運用數位資產存放庫。

* 在大多數情況下，您的數位資產存放庫會持續成長。 因此，在內容建立週期的早期將元資料的使用、資料夾結構和檔案命名正規化非常重要。
* 僅使用資料夾來為數位資產強加一致的儲存結構。 此一致性可協助您更妥善地處理及管理資產。 例如，放置在下列類型資料夾中的資產可協助您使用適當的 [用於資產處理的設定檔](processing-profiles.md):

   * **開發資料夾**:包含您目前使用的數位資產。
   * **用戶端資料夾**:包含根據用戶端或專案名稱的數位資產。
   * **主資料夾**:包含原始數位資產。
   * **轉譯資料夾**:包含原始數位資產的轉譯和復本。
   * **檔案大小資料夾**:包含以小型、中型或大型檔案大小為基礎的數位資產。
   * **中繼資料夾**:包含已準備好在您網站上上線發佈的數位資產。
   * **MIME類型資料夾**:包含MIME類型（如影像、檔案和多媒體）專屬的數位資產。
   * **封存資料夾**:包含已淘汰的數位資產。
   * **日期資料夾**:包含以建立日期或上次修改日期為基礎的數位資產。

* 建立不可能變更的資料夾目錄，以便任何自訂或自動化都能繼續運作。 例如，指派的處理設定檔可繼續運作。
* 如果資產已發佈，則您使用 [!DNL Experience Manager] 若要將資產移至另一個資料夾，並從新位置重新發佈，仍可使用原始發佈的資產位置，以及新重新發佈的資產。 然而，原始發佈的資產是 *遺失* to [!DNL Experience Manager] 無法取消發佈。 因此，最佳作法是先取消發佈資產，然後將其移至其他資料夾。

## 使用標籤組織資產 {#use-tags-to-organize-assets}

使用標籤做為中繼資料，您可以輕鬆搜尋資產、使用搜尋結果建立集合、提升某些資產的搜尋排名，以及運用Adobe Sensei的AI演算法來探索資產。

[!DNL Adobe Experience Manager Assets] 使用自學算法來建立描述性很強的標籤，只需按幾下即可找到正確的資產。 智慧標籤使用Adobe Sensei（我們的人工智慧和機器學習框架），可通過培訓識別標準標籤和特定於業務的標籤並應用於影像。 智慧標籤也可以識別內容、個別字詞或片語，並自動將描述性標籤套用至資產

如需詳細資訊，請參閱下列文章：

* [關於Experience Manager中的標籤](/help/sites-authoring/tags.md)
* [編輯資產中繼資料](metadata.md)
* [增強資產中的智慧標籤](enhanced-smart-tags.md)

## 組織為集合 {#organize-as-collections}

將資產集合放在 [!DNL Experience Manager Assets]，您可以簡化使用者間建立、編輯和共用資產的能力。 根據您使用方式建立數種集合類型，包括包含資產、資料夾和集合靜態參考清單的集合，以及根據搜尋准則提取資產的集合。  您也可以使用不同位置的資產建立集合，並與具有不同存取、檢視和編輯權限層級的多個使用者共用集合。

如需詳細資訊，請參閱 [管理集合](manage-collections.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## 組織您的資產以使用設定檔 {#organize-to-use-profiles}

處理設定檔包含 [!DNL Assets] 處理命令，此命令會套用至上傳至預先定義之資料夾的資產。 設定檔可用來自動處理資料夾或新上傳資產的內容。 您可以運用設定檔來更妥善地組織資產。

標準化中繼資料的使用、檔案命名和資料夾結構，可確保隨著數位資產池的成長，您可以更精確且一致地將處理設定檔套用至資料夾。

>[!MORELIKETHIS]
>
>* [處理中繼資料、影像和視訊的設定檔](processing-profiles.md).
>* [中繼資料設定檔](/help/assets/metadata-config.md#metadata-profiles).
>* [視訊設定檔](video-profiles.md).
>* [Dynamic Media影像設定檔](image-profiles.md).

