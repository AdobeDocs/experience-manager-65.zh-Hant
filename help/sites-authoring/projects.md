---
title: 專案
description: 專案可讓您將資源分組到一個實體中，其共用的共用環境可讓您輕鬆管理專案。
exl-id: 632c0608-2ab8-4a5b-8251-cd747535449b
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 27%

---


# 專案 {#projects}

專案可讓您將資源群組到一個實體中。共同的共用環境使您的專案容易管理。您可以與專案相關聯的資源類型在 AEM 中稱為圖磚。圖磚可能包括專案和團隊資訊、資產、工作流程和其他類型的資訊，如[專案圖磚](#project-tiles)中詳細所述。

身為使用者，您可以：

* 建立和刪除專案
* 將內容和資產資料夾與專案建立關聯
* 從專案中刪除內容連結

## 存取需求 {#access-requirements}

專案標準AEM功能，不需要任何其他設定。

不過，若使用者在專案中使用專案（如當建立專案、建立任務/工作流程或檢視和管理團隊時）時檢視其他使用者/群組，這些使用者需要擁有讀取許可權 `/home/users` 和 `/home/groups`.

最簡單的方法是提供 **projects-users** 群組讀取存取權至 `/home/users` 和 `/home/groups`.

## 專案主控台 {#projects-console}

專案主控台是您在 AEM 中存取和管理專案的地方。

![專案主控台](assets/screen-shot_2019-03-05at125110.png)

專案主控台類似於AEM中的其他主控台，可在個別專案上執行數個動作，並調整您的專案檢視。

### 切換您的模式 {#modes}

您可以使用邊欄選擇器，在主控台模式之間變更。

![邊欄選擇器](assets/projects-rail.png)

#### 僅限內容 {#content-only}

開啟主控台時，預設模式為僅內容。 它會顯示您的所有專案。

#### 時間軸 {#timeline}

時間表檢視可讓您選取個別專案並檢視其上的活動。 使用邊欄選擇器或快速鍵 `alt+1` 以變更此檢視。

![時間軸模式](assets/project-timeline.png)

### 切換檢視 {#views}

您可以使用檢視選擇器，在以大型圖磚檢視專案（預設）、以清單或行事曆檢視專案之間變更。

![檢視](assets/projects-views.png)

### 篩選您的檢視 {#filter}

您可以使用篩選器在所有專案與僅限作用中的專案之間切換。

![篩選](assets/projects-filter.png)

### 選取和檢視專案 {#selecting}

將滑鼠停留在專案拼貼上，然後按一下核取記號來選取專案。

按一下專案以檢視專案的詳細資訊，以深入瞭解專案的詳細資訊。

### 建立新專案 {#creating}

按一下 **建立** 以新增專案。

## 專案圖磚 {#project-tiles}

專案由您想要一起管理的不同資訊型別組成。 此資訊由不同的專案表示 **圖磚**.

您可以擁有下列與專案關聯的圖磚。

* [Assets](#assets)
* [資產集合](#asset-collections)
* [體驗](#experiences)
* [連結](#links)
* [專案資訊](#project-info)
* [團隊](#team)
* [登陸頁面](#landing-pages)
* [電子郵件](#emails)
* [工作流程](#workflows)
* [啟動](#launches)
* [任務](#tasks)

按一下任何圖磚右上角的下拉式功能表，即可新增更多資料至圖磚。

按一下任何圖磚右下方的省略符號按鈕，即可在圖磚的相關主控台中開啟圖磚資料。

### 資產 {#assets}

在&#x200B;**資產**&#x200B;圖磚中，您可以收集所有要用於特定專案的資產。

![資產圖磚](assets/project-tile-assets.png)

您直接在圖磚中上傳資產。

### 資產集合 {#asset-collections}

與資產類似，您可以將[資產集合](/help/assets/manage-collections.md)直接新增到您的專案中。您在 Assets 中定義集合。

![資產集合圖磚](assets/project-tile-asset-collection.png)

按一下&#x200B;**新增系列**，並從清單中選取適當的系列，即可新增系列。

### 體驗 {#experiences}

此 **體驗** 圖磚可讓您將行動應用程式、網站或出版物新增至專案。

![體驗圖磚](assets/project-tile-experiences.png)

這些圖示會指出所代表的體驗型別。

* 網站
* 行動應用程式

### 連結 {#links}

此 **連結** 圖磚可讓您將外部連結與專案建立關聯。

![連結圖磚](assets/project-tile-links.png)

您可以使用易於識別的名稱為連結命名，也可以變更縮圖。

### 專案資訊 {#project-info}

此 **專案資訊** 圖磚提供專案的一般資訊，包括說明、專案狀態（非作用中或作用中）、到期日和成員。 此外，您可以加入專案縮圖，它顯示在主要專案頁面上。

![專案資訊拼貼](assets/project-tile-info.png)

### 翻譯工作 {#translation-job}

此 **翻譯工作** 圖磚是您開始翻譯的位置，也是您檢視翻譯狀態的位置。

![翻譯工作拼貼](assets/project-tile-translation.png)

若要設定翻譯，請參閱檔案 [正在建立翻譯專案。](/help/assets/translation-projects.md)

### 團隊 {#team}

在此圖磚中，您可以指定專案團隊的成員。編輯時，您可以輸入團隊成員的姓名並指派使用者角色。

![團隊圖磚](assets/project-tile-team.png)

您可以在團隊中新增和刪除團隊成員。此外，您可以編輯指派給團隊成員的[使用者角色](#userroles)。

### 登陸頁面 {#landing-pages}

此 **登陸頁面** 圖磚可讓您請求新的登陸頁面。

![登陸頁面圖磚](assets/project-tile-landing.png)

本檔案將說明此工作流程[建立登入頁面工作流程。](/help/sites-authoring/projects-with-workflows.md#request-landing-page-workflow)

### 電子郵件 {#emails}

此 **電子郵件** 圖磚可協助您管理電子郵件請求。 它會開始 **要求電子郵件** 工作流程。

![電子郵件動態磚](assets/project-tile-email.png)

如需詳細資訊，請參閱 [請求電子郵件工作流程。](/help/sites-authoring/projects-with-workflows.md#request-email-workflow)

### 工作流程 {#workflows}

您可以開始專案的工作流程。 如果有任何工作流程在執行中，其狀態會顯示在 **工作流程** 圖磚。

![工作流程動態磚](assets/project-tile-workflows.png)

根據您建立的專案，有不同的工作流程可供使用。

相關說明請參閱[使用專案工作流程](/help/sites-authoring/projects-with-workflows.md)。

### Launch {#launches}

此 **啟動** 圖磚會顯示「 」要求的任何啟動， [請求啟動工作流程。](/help/sites-authoring/projects-with-workflows.md)

![「啟動」圖磚](assets/project-tile-launches.png)

### 任務 {#tasks}

任務可讓您監控任何專案相關任務的狀態，包括工作流程。如需任務的詳細資訊，請參閱[使用任務](/help/sites-authoring/task-content.md)。

![「任務」圖磚](assets/project-tile-tasks.png)

## 專案範本 {#project-templates}

範本是啟動專案的基礎。 AEM提供這些標準專案範本。

* **媒體專案**  — 此為媒體相關活動的參考範例專案。 其中包含數個與媒體相關的專案角色，也包括與媒體內容相關的工作流程。
* **[產品拍照專案](/help/sites-authoring/managing-product-information.md)**  — 此為管理電子商務相關產品攝影的參考範例。
* **[翻譯專案](/help/sites-administering/translation.md)**  — 此為管理翻譯相關活動的參考範例。 其中包含基本角色，並包含管理翻譯的工作流程。
* **簡單專案**  — 這是任何不符合其他類別的專案的參考範例。 其中包含三個基本角色和四個一般AEM工作流程。

根據您選取的範本，專案中提供了不同的可用選項，例如使用者角色和工作流程。

## 專案中的使用者角色 {#user-roles-in-a-project}

不同的使用者角色會在專案範本中定義，主要原因有二：

1. 許可權：使用者角色屬於列出的三個類別之一：觀察者、編輯者、擁有者。 例如，攝影師或撰稿人將擁有與編輯者相同的許可權。 權限決定使用者可對專案內容進行的操作。
1. 工作流程：工作流程會決定指派給專案中任務的使用者。 任務可以與專案角色相關聯。例如，可以將任務指派給攝影師，以便所有擁有攝影師角色的團隊成員都能取得任務。

所有專案都支援下列預設角色，可讓您管理安全性及控制許可權。

| 角色 | 說明 | 權限 | 群組會籍 |
|---|---|---|---|
| 觀察者 | 擁有此角色的使用者可以檢視專案詳細資料，包括專案狀態。 | 專案的唯讀權限 | `workflow-users` 群組 |
| 編輯者 | 擁有此角色的使用者可以上傳和編輯專案的內容。 | 對專案、關聯中繼資料和相關資產的讀寫存取權<br>上傳快照清單、拍照以及檢閱和核准資產的許可權<br>的寫入許可權 `/etc/commerce`<br>修改特定專案的許可權 | `workflow-users` 群組 |
| 所有者 | 具有此角色的使用者可以建立專案、在專案中起始工作，並將核准的資產移至生產資料夾。 擁有者也可以檢視及執行專案中的所有其他任務。 | `/etc/commerce` 的寫入權限 | `dam-users` 群組以建立專案<br>`projects-administrators` 群組，以便建立專案和移動資產 |

對於創意專案，也會提供其他角色，例如攝影師。 您可以使用這些角色來衍生特定專案的自訂角色。

### 自動群組建立 {#auto-group-creation}

當您建立專案並將使用者新增至各種角色時，系統會自動建立與專案關聯的群組以管理關聯的許可權。

例如，名為Myproject的專案將包含三個群組 **Myproject所有者**， **Myproject編輯器**， **Myproject觀察員**.

如果刪除專案，則只有在您選取適當的選項時，才會刪除這些群組 [刪除專案時。](/help/sites-authoring/touch-ui-managing-projects.md#deleting-a-project) 管理員也可以手動刪除中的群組 **工具** > **安全性** > **群組**.

## 其他資源 {#additional-resources}

如需有關使用專案的詳細資訊，請參閱下列附加檔案：

* [管理專案](/help/sites-authoring/touch-ui-managing-projects.md)
* [使用任務](/help/sites-authoring/task-content.md)
* [使用專案工作流程](/help/sites-authoring/projects-with-workflows.md)
* [Creative Project與PIM整合](/help/sites-authoring/managing-product-information.md)
