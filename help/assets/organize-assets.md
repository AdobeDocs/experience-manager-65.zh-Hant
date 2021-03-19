---
title: 組織您的數位資產
description: 使用Experience Manager組織您的數位資產、影像、檔案、檔案夾等。
contentOwner: AG
role: 業務從業人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---


# 組織您的數位資產 {#organize-digital-assets}

Microsoft Office和PDF檔案的所有數位資產、中繼資料和內容都會加以擷取並設為可搜尋。 搜尋功能可讓您對資產進行精密的篩選，並完全尊重適當的權限。 在數位資產管理中，中繼資料會在中繼資料中詳細說明。

[!DNL Experience Manager Assets] 支援多種組織內容的方式。您可以使用資料夾以階層式方式來組織資料夾，或使用例如標籤，以無序、臨機方式來組織資料夾。 使用者可在DAM資產編輯器中編輯標籤，子資產、轉譯和中繼資料會顯示在此處。

## 組織資料夾{#organize-using-folders}中的資產

組織資產的最基本方式是將資產儲存在檔案夾中。 它類似於在本地檔案系統中組織資料夾中的檔案。 如需如何建立和管理資料夾的詳細資訊，請參閱[管理資產](manage-assets.md)。 如何命名檔案和檔案夾、如何排列子檔案夾，以及如何處理這些檔案夾中的檔案，都會對這些資產的處理方式產生重大影響。 透過使用一致且適當的檔案和資料夾命名策略，以及良好的中繼資料實務，您可以充份運用您的數位資產儲存庫。

* 在大多數情況下，您的數位資產存放庫會一直在成長。 因此，在內容建立週期的初期，必須正式化中繼資料的使用、檔案夾結構和檔案命名。
* 僅使用資料夾，為您的數位資產建立一致的儲存結構。 此一致性有助於您的流程，並更好地管理資產。 例如，放置在下列類型資料夾中的資產可協助您使用適當的[描述檔，以用於資產處理](processing-profiles.md):

   * **開發資料夾**:包含您目前正在處理的數位資產。
   * **客戶端資料夾**:包含根據客戶或專案名稱的數位資產。
   * **主資料夾**:包含原始的來源數位資產。
   * **轉譯資料夾**:包含原始來源數位資產的轉譯和復本。
   * **檔案大小資料夾**:包含以小型、中型或大型檔案大小為基礎的數位資產。
   * **轉移資料夾**:包含可立即發佈至網站的數位資產。
   * **MIME類型資料夾**:包含特定於MIME類型（例如影像、檔案和多媒體）的數位資產。
   * **封存資料夾**:包含淘汰的數位資產。
   * **日期型資料夾**:包含根據建立日期或上次修改日期的數位資產。

* 建立不可能變更的資料夾目錄，讓任何自訂或自動功能都能繼續運作。 例如，指派的處理設定檔仍可繼續運作。
* 如果資產已發佈，則您會使用[!DNL Experience Manager]將資產移至另一個檔案夾，並從其新位置重新發佈，則原始已發佈的資產位置以及新重新發佈的資產仍然可用。 但是，原始發佈的資產是&#x200B;*lost*&#x200B;至[!DNL Experience Manager]，無法解除發佈。 因此，最佳實務是，先解除發佈資產，然後將其移至其他資料夾。

## 使用標籤{#use-tags-to-organize-assets}組織資產

使用標籤作為中繼資料，您可以輕鬆搜尋資產、使用搜尋結果建立系列、大幅提升某些資產的搜尋排名，並運用Adobe Sensei的AI演算法進行資產搜尋。

[!DNL Adobe Experience Manager Assets] 使用自學習演算法建立高度描述性的標籤，只要按幾下滑鼠，就能找到正確的資產。智慧標籤使用Adobe Sensei，這是我們的人工智慧和機器學習框架，可經過訓練，以識別並套用標準和業務特定標籤至影像。 智慧型標籤也可識別內容、個別字詞或片語，並自動將描述性標籤套用至資產

如需詳細資訊，請參閱下列文章：

* [關於Experience Manager中的標籤](/help/sites-authoring/tags.md)
* [編輯資產中繼資料](metadata.md)
* [資產中的增強智慧標籤](enhanced-smart-tags.md)

## 組織為系列{#organize-as-collections}

透過[!DNL Experience Manager Assets]中的資產收集，您可以簡化在使用者之間建立、編輯和共用資產的功能。 根據您的使用方式建立數種系列，包括包含資產、檔案夾和系列之靜態參考清單的系列，以及根據搜尋准則提取資產的系列。  您也可以使用不同位置的資產建立系列，並與具有不同存取、檢視和編輯權限等級的多名使用者共用。

如需詳細資訊，請參閱[管理系列](manage-collections.md)

<!-- TBD items: add screenshots where applicable
Any hints/recommendations of when to use what method of organizing? Some examples of how organizing helps towards a better taxonomy and improved content velocity.
Add back links to blog posts by marketing?
-->

## 組織您的資產以使用設定檔{#organize-to-use-profiles}

處理設定檔包含[!DNL Assets]處理指令，這些指令會套用至上傳至預先定義的資料夾的資產。 描述檔可用來自動處理資料夾或新上傳資產的內容。 您可以運用個人檔案，更好地組織資產。

標準化中繼資料的使用、檔案命名和資料夾結構，可確保隨著數位資產的儲存量增加，您可以更精確、更一致地將處理設定檔套用至資料夾。

>[!MORELIKETHIS]
>
>* [處理中繼資料、影像和視訊的設定檔](processing-profiles.md)。
>* [中繼資料設定檔](/help/assets/metadata-config.md#metadata-profiles).
>* [視訊設定檔](video-profiles.md)。
>* [Dynamic Media影像描述檔](image-profiles.md)。

