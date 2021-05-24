---
title: 專案
seo-title: 專案
description: 專案可讓您將資源分組為一個實體，其共同的共用環境可讓您輕鬆管理專案
seo-description: 專案可讓您將資源分組為一個實體，其共同的共用環境可讓您輕鬆管理專案
uuid: 4b5b9d78-d515-46af-abe2-882da0a1c8ae
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: dee7ac7c-ca86-48e9-8d95-7826fa926c68
docset: aem65
exl-id: 632c0608-2ab8-4a5b-8251-cd747535449b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1399'
ht-degree: 10%

---

# 專案{#projects}

專案可讓您將資源分組為一個實體。 共用的共用環境讓您輕鬆管理專案。 您可與專案關聯的資源類型在AEM中以圖磚形式參照。 圖磚可以包括項目和團隊資訊、資產、工作流和其他類型的資訊，如[項目圖磚中詳細描述。](#project-tiles)

>[!CAUTION]
>
>若要讓專案中的使用者在使用專案功能（例如建立專案、建立工作/工作流程、查看及管理團隊）時查看其他使用者/群組，這些使用者必須擁有&#x200B;**/home/users**&#x200B;和&#x200B;**/home/groups**&#x200B;的讀取存取權。 實作此項目最簡單的方式是，為&#x200B;**projects-users**&#x200B;群組提供&#x200B;**/home/users**&#x200B;和**/home/groups**的讀取存取權。

身為使用者，您可以執行下列動作：

* 建立專案
* 將內容和資產資料夾關聯至專案
* 刪除專案
* 從專案移除內容連結

請參閱下列其他主題：

* [管理專案](/help/sites-authoring/touch-ui-managing-projects.md)
* [使用任務](/help/sites-authoring/task-content.md)
* [使用專案工作流程](/help/sites-authoring/projects-with-workflows.md)
* [創意專案與PIM整合](/help/sites-authoring/managing-product-information.md)

## 項目控制台{#projects-console}

專案主控台是您在AEM中存取及管理專案的位置。

![screen-shot_2019-03-05at125110](assets/screen-shot_2019-03-05at125110.png)

* 選擇&#x200B;**時間軸** ，然後選擇項目以查看其時間軸。
* 按一下/點選&#x200B;**選取**&#x200B;以進入選取模式。
* 按一下&#x200B;**建立**&#x200B;以新增專案。
* **切換「作** 用中專案」 ，即可在所有專案之間切換，而只切換作用中的專案。
* **顯示統** 計資訊查看有關任務完成的項目統計資訊。

## 專案圖磚{#project-tiles}

使用「專案」，可將不同類型的資訊與專案建立關聯。 這些名稱為&#x200B;**圖磚**。 本節將說明每個圖磚及其包含的資訊類型。

您可以有下列圖磚與您的專案相關聯。 以下各節將分別說明各項：

* 資產和資產集合
* 體驗
* 連結
* 專案資訊
* 團隊
* 著陸頁面
* 電子郵件
* 工作流程
* 啟動
* 任務

### 資產 {#assets}

在&#x200B;**Assets**&#x200B;方塊中，您可以收集您用於特定專案的所有資產。

![chlimage_1-70](assets/chlimage_1-70.png)

您直接在圖磚中上傳資產。 此外，如果您有Dynamic Media附加元件，也可以建立影像集、回轉集或混合媒體集。

![chlimage_1-71](assets/chlimage_1-71.png)

### 資產集合{#asset-collections}

與資產類似，您可以直接將[資產集合](/help/assets/manage-collections.md)新增至專案。 您可以在資產中定義集合。

![chlimage_1-72](assets/chlimage_1-72.png)

按一下「新增系列」 **並從清單中選取適當的系列** ，即可新增系列。

### 體驗 {#experiences}

「**體驗**」方塊可讓您新增行動應用程式、網站或發佈至專案。

![chlimage_1-73](assets/chlimage_1-73.png)

這些圖示會指出所呈現的體驗類型：網站、行動應用程式或出版物。按一下+號或按一下「新增體驗」 **並選取體驗類型** ，以新增體驗。

![chlimage_1-74](assets/chlimage_1-74.png)

選取縮圖的路徑，並變更體驗的縮圖（若適用）。 體驗會在&#x200B;**體驗**&#x200B;方塊中分組。

### 連結 {#links}

「連結」方塊可讓您將外部連結與專案建立關聯。

![chlimage_1-75](assets/chlimage_1-75.png)

您可以使用易於識別的名稱來命名連結，並變更縮圖。

![chlimage_1-76](assets/chlimage_1-76.png)

### 專案資訊 {#project-info}

「項目資訊」(Project Information)表徵圖提供有關項目的一般資訊，包括說明、項目狀態（非活動或活動）、到期日和成員。 此外，您可以新增專案縮圖，該縮圖會顯示在主「專案」頁面上。

![chlimage_1-77](assets/chlimage_1-77.png)

可以從此表徵圖（或更改其角色）和「團隊」表徵圖中分配和刪除團隊成員。

![chlimage_1-78](assets/chlimage_1-78.png)

### 翻譯工作 {#translation-job}

「翻譯工作」方塊是您開始翻譯的位置，也是您查看翻譯狀態的位置。 若要設定翻譯，請參閱[建立翻譯專案](/help/assets/translation-projects.md)。

![chlimage_1-79](assets/chlimage_1-79.png)

按一下&#x200B;**翻譯工作**&#x200B;卡片底部的刪節號，查看翻譯工作流程中的資產。 翻譯工作清單也會顯示資產中繼資料和標籤的項目。 這些項目表示資產的中繼資料和標籤也會翻譯。

![chlimage_1-80](assets/chlimage_1-80.png)

### 團隊 {#team}

在此圖磚中，您可以指定專案團隊的成員。 編輯時，您可以輸入團隊成員的名稱並分配用戶角色。

![chlimage_1-81](assets/chlimage_1-81.png)

您可以從團隊中添加和刪除團隊成員。 此外，還可以編輯分配給團隊成員的[用戶角色](#userroles)。

![chlimage_1-82](assets/chlimage_1-82.png)

### 著陸頁面 {#landing-pages}

「**著陸**&#x200B;頁面」方塊可讓您要求新的登陸頁面。

![chlimage_1-83](assets/chlimage_1-83.png)

[建立登錄頁面工作流程](/help/sites-authoring/projects-with-workflows.md#request-landing-page-workflow)中會說明此工作流程。

### 電子郵件 {#emails}

**電子郵件**&#x200B;方塊可協助您管理電子郵件請求。 它會啟動「請求電子郵件」工作流程。

![chlimage_1-84](assets/chlimage_1-84.png)

[請求電子郵件工作流程中會說明更多資訊。](/help/sites-authoring/projects-with-workflows.md#request-email-workflow)

### 工作流程 {#workflows}

您可以指派專案以遵循特定工作流程。 如果有任何工作流程在執行中，其狀態會顯示在「專案」的&#x200B;**Workflows**&#x200B;方塊中。

![chlimage_1-85](assets/chlimage_1-85.png)

您可以指派專案以遵循特定工作流程。 視您選擇的專案而定，您有不同的可用工作流程。

在[使用專案工作流程中對這些內容進行了說明。](/help/sites-authoring/projects-with-workflows.md)

### 啟動 {#launches}

「啟動」方塊會顯示已透過[「請求啟動」工作流程請求的任何啟動。](/help/sites-authoring/projects-with-workflows.md)

![chlimage_1-86](assets/chlimage_1-86.png)

### 任務 {#tasks}

任務可讓您監視任何專案相關任務的狀態，包括工作流程。 [使用任務](/help/sites-authoring/task-content.md)中將詳細介紹任務。

![chlimage_1-87](assets/chlimage_1-87.png)

## 項目模板{#project-templates}

AEM隨附三個不同的範本：

* 簡單專案 — 任何不符合其他類別（包羅永珍）的專案的參考範例。 它包含三個基本角色（擁有者、編輯者和觀察者）和四個工作流程（專案核准、請求啟動、請求登錄頁面和請求電子郵件）。
* 媒體專案 — 媒體相關活動的參考範例專案。 它包含數個與媒體相關的專案角色（攝影師、編輯、文案撰寫者、設計師、擁有者和觀察者）。 此外，還包含與媒體內容相關的兩個工作流程： 「要求復本」（用於要求和檢閱文字）和「產品像片拍攝」（用於管理與產品相關的像片）
* [產品像片拍攝專案](/help/sites-authoring/managing-product-information.md)  — 管理電子商務相關產品攝影的參考範例。它包括攝影師、編輯、像片閱讀者、擁有者、創意總監、社交媒體行銷人員、行銷經理、審核者和觀察者的角色。
* [翻譯專案](/help/sites-administering/translation.md)  — 管理翻譯相關活動的參考範例。它包含三個基本角色（擁有者、編輯和觀察者）。 它包含可在工作流程使用者介面中存取的兩個工作流程。

根據您選取的範本，您有不同的選項可供使用，尤其是使用者角色和工作流程。

## 項目{#user-roles-in-a-project}中的用戶角色

不同的使用者角色會在專案範本中設定，其使用原因有二：

1. 權限. 使用者角色分為下列三個類別之一：觀察者、編輯者、擁有者。 例如，攝影師或文案撰寫者具有與編輯者相同的權限。 權限會決定使用者可以對專案中的內容執行什麼動作。
1. 工作流程. 工作流程會決定專案中指派工作的人員。 這些任務可以與項目角色相關聯。 例如，任務可以分配給Photogrepers，因此具有Photogrepher角色的所有團隊成員都將獲得該任務。

所有專案都支援下列預設角色，可讓您管理安全性和控制權限：

<table>
 <tbody>
  <tr>
   <td><p><strong>角色</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
   <td><p><strong>權限</strong></p> </td>
   <td><p><strong>群組成員資格</strong></p> </td>
  </tr>
  <tr>
   <td><p>觀察者</p> </td>
   <td><p>此角色的使用者可以檢視專案詳細資訊，包括專案狀態。</p> </td>
   <td><p>專案的唯讀權限</p> </td>
   <td><p>工作流程使用者群組</p> </td>
  </tr>
  <tr>
   <td><p>編輯者</p> </td>
   <td><p>此角色的使用者可以上傳和編輯專案的內容。</p> <p> </p> </td>
   <td>
    <ul>
     <li>對專案、相關中繼資料和相關資產的讀取和寫入存取權。</li>
     <li>上傳照片清單、像片拍攝，以及檢閱和核准資產的權限</li>
     <li>/etc/commerce的寫入權限</li>
     <li>具有特定專案的修改權限</li>
    </ul> </td>
   <td><p>工作流程使用者群組</p> </td>
  </tr>
  <tr>
   <td><p>所有者</p> </td>
   <td><p>此角色的使用者可以起始專案。 擁有者可以建立專案、啟動專案中的工作，以及將已核准的資產移至生產資料夾。 雖然項目中的所有其他任務也可以由所有者查看和執行。</p> </td>
   <td>
    <ul>
     <li>/etc/commerce的寫入權限</li>
    </ul> </td>
   <td>
    <ul>
     <li>DAM使用者群組（以便建立專案）</li>
     <li>專案管理員群組（以建立專案和移動資產）</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

對於創意專案，也提供其他角色 — 例如攝影師 — 。 您可以使用這些角色來衍生特定專案的自訂角色。

>[!NOTE]
>
>當您建立專案並將使用者新增至各種角色時，系統會自動建立與專案相關的群組，以管理相關的權限。例如，名為Myproject的專案會有三個群組 **Myproject Owners**、 **Myproject Editors**、 **Myproject Obsertors**。不過，如果刪除專案，這些群組不會自動刪除。管理員需要手動刪除「工具 **>安全** 性 **>** 群組 ****」。
