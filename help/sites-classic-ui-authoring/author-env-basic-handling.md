---
title: 基本處理
description: 使用Adobe Experience Manager作者環境時的基本處理概觀。 它使用Sites主控台作為基礎。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 2981dc20-b2ba-4ea2-a53b-8b5fe526aa9c
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 3%

---

# 基本處理{#basic-handling}

>[!NOTE]
>
>* 此頁面旨在概略說明使用Adobe Experience Manager (AEM)製作環境時的基本處理方式。 它會使用 **網站** 以主控台為基礎。
>
>* 部分功能並非在所有主控台中提供，而其他功能則在某些主控台中提供。 有關個別主控台及其相關功能的特定資訊，請參閱其他頁面上的詳細說明。
>* 在整個AEM環境中都可以使用鍵盤快速鍵。 尤其是當 [使用主控台](/help/sites-classic-ui-authoring/author-env-keyboard-shortcuts.md) 和 [編輯頁面](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md).
>

## 歡迎畫面 {#the-welcome-screen}

傳統UI提供一系列主控台，這些主控台使用眾所周知的機制來導覽和起始動作，包括按一下、連按兩下和 [內容功能表](#context-menus).

登入後，歡迎畫面會隨即顯示。 它提供控制檯與服務的連結清單：

![screen_shot_2012-01-30at61745pm](assets/screen_shot_2012-01-30at61745pm.png)

## 主控台 {#consoles}

主要主控台包括：

<table>
 <tbody>
  <tr>
   <td><strong>主控台</strong></td>
   <td><strong>用途</strong></td>
  </tr>
  <tr>
   <td><strong>歡迎</strong></td>
   <td>提供概述和（透過連結）直接存取AEM主要功能。</td>
  </tr>
  <tr>
   <td><strong>數位資產</strong><br /> </td>
   <td>這些主控台可讓您匯入和 <a href="/help/sites-classic-ui-authoring/classicui-assets.md">管理數位資產</a> 例如影像、影片、檔案和音訊檔案。 這些資產隨後便可由同一AEM例項上執行的任何網站使用。 </td>
  </tr>
  <tr>
   <td><strong>啟動</strong></td>
   <td>這有助於您管理您的 <a href="/help/sites-classic-ui-authoring/classic-launches.md">啟動</a>；這些功能可讓您為未來發行的一或多個已啟動網頁開發內容。<br /> <i>注意：在觸控式UI中，Sites主控台與「參考」邊欄提供許多相同的功能。</i> <i>如有必要，可以從「工具」主控台使用此主控台；請選取作業，然後選取啟動。</i></td>
  </tr>
  <tr>
   <td><strong>收件匣 </strong></td>
   <td>通常，工作流程的子任務會涉及不同的人，每個人必須先完成自己的步驟，才能將工作移交給下一個人。 「收件匣」可讓您檢視與這類工作相關的通知。 另請參閱 <a href="/help/sites-administering/workflows.md">使用工作流程</a>. <br /> </td>
  </tr>
  <tr>
   <td><strong>標記</strong></td>
   <td>「標籤」主控台可讓您管理標籤。 標籤是簡短名稱或片語，可用來分類和註釋內容片段，以便更容易找到並組織。 如需詳細資訊，請參閱 <a href="/help/sites-classic-ui-authoring/classic-feature-tags.md">使用和管理標籤</a>.</td>
  </tr>
  <tr>
   <td><strong>工具</strong></td>
   <td>此 <a href="/help/sites-administering/tools-consoles.md">工具主控台</a> 可讓您存取協助您管理網站、數位資產和內容存放庫其他方面的數種專用工具和主控台。</td>
  </tr>
  <tr>
   <td><strong>使用者</strong></td>
   <td>這些主控台可讓您管理使用者和群組的存取許可權。 如需完整詳細資訊，請參閱 <a href="/help/sites-administering/security.md">使用者管理與安全性</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>網站</strong></td>
   <td>「網站/網站」主控台可讓您 <a href="/help/sites-classic-ui-authoring/classic-page-author.md">建立、檢視及管理網站</a> 在您的AEM執行個體上執行。 透過這些主控台，您可以建立、複製、移動和刪除網站頁面、啟動工作流程，以及啟用（發佈）頁面。 您也可以開啟頁面進行編輯。<br /> </td>
  </tr>
  <tr>
   <td><strong>工作流程</strong></td>
   <td>工作流程是一系列已定義的步驟，用於說明完成某些任務的流程。 通常會有幾個人參與工作，且每個人都必須先完成自己的步驟，才能將工作移交給下一位人員。 「工作流程」主控台可讓您建立工作流程模型，並管理執行中的工作流程例項。 另請參閱 <a href="/help/sites-administering/workflows.md">使用工作流程</a>.<br /> </td>
  </tr>
 </tbody>
</table>

此 **網站** 控制檯提供兩個窗格，供您導覽及管理頁面：

* 左窗格

  這會顯示您網站的樹狀結構以及這些網站內的頁面。

  它也會顯示其他方面或AEM的相關資訊，包括專案、藍圖和資產。

* 右窗格

  這會顯示頁面（在左窗格中選取的位置），並可用來採取動作。

從這裡，您可以 [管理您的頁面](/help/sites-authoring/managing-pages.md) 使用工具列、快顯功能表或透過開啟頁面進行進一步動作。

>[!NOTE]
>
>所有主控台的基本處理方式都相同。 本節將重點放在 **網站** 主控台，因為它是編寫時使用的主要主控台。

![chlimage_1-9](assets/chlimage_1-9a.png)

## 存取說明 {#accessing-help}

在各種主控台（例如網站）上， **說明** 按鈕可供使用。 按一下 **說明** 開啟「封裝共用」或檔案網站。

![chlimage_1-10](assets/chlimage_1-10a.png)

編輯頁面時， [sidekick也有存取說明的按鈕](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#accessing-help).

## 使用網站主控台導覽 {#navigating-with-the-websites-console}

此 **網站** 主控台會以樹狀結構列出您的內容頁面（左側窗格）。 為方便瀏覽，可視需要展開樹狀結構的區段(+)或收合區段(-)：

* 按一下左窗格中的頁面名稱會執行下列動作：

   * 列出右側窗格中的子頁面
   * 展開左側窗格中的結構。

     基於效能考量，此動作會視子節點的數目而定。 在標準安裝中，此擴充方法適用於 `30` 或更少的子節點。

* 連按兩下頁面名稱（左窗格）會展開樹狀結構，不過同時開啟頁面時，這種效果並不明顯。

>[!NOTE]
>
>此預設值( `30`)可以在您的siteadmin widget應用程式特定設定中，依主控台進行變更：
>
>在網站管理員節點上：
>
>設定屬性的值：
>`treeAutoExpandMax`
>於：
>`/apps/wcm/core/content/siteadmin`
>
>或是全域佈景主題：
>設定下列專案的值：
>`TREE_AUTOEXPAND_MAX`
>在：
>`/apps/cq/ui/widgets/themes/default/widgets/wcm/SiteAdmin.js`
>
>另請參閱 [CQ Widget API中的網站管理員](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.SiteAdmin) 以取得更多詳細資料。

## 網站主控台上的頁面資訊 {#page-information-on-the-websites-console}

的右窗格 **網站** console提供包含頁面相關資訊的清單檢視：

![page-info](assets/page-info.png)

以下是可供使用的欄位；這些欄位的子集會顯示為預設值：

<table>
 <tbody>
  <tr>
   <td><strong>欄</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>縮圖</td>
   <td>顯示頁面的縮圖。</td>
  </tr>
  <tr>
   <td>標題</td>
   <td>顯示在頁面上的標題</td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>AEM參考頁面的名稱</td>
  </tr>
  <tr>
   <td>已發佈</td>
   <td>指出頁面是否已發佈，並提供發佈日期和時間。</td>
  </tr>
  <tr>
   <td>已修改</td>
   <td>指出頁面是否已修改，並提供修改日期和時間。 若要儲存任何修改，您必須啟動頁面。</td>
  </tr>
  <tr>
   <td>Scene7發佈</td>
   <td>指出頁面是否已發佈至Scene7。<br /> </td>
  </tr>
  <tr>
   <td>狀態</td>
   <td>指出頁面的狀態，例如頁面是否為工作流程或即時副本的一部分，或頁面是否已鎖定。</td>
  </tr>
  <tr>
   <td>印象</td>
   <td>以點選數顯示頁面上的活動。</td>
  </tr>
  <tr>
   <td>範本</td>
   <td>指出頁面所依據的範本。</td>
  </tr>
  <tr>
   <td>在工作流程中</td>
   <td>表示頁面在工作流程中。</td>
  </tr>
  <tr>
   <td>鎖定者: </td>
   <td>顯示頁面何時已鎖定，以及已鎖定頁面的使用者帳戶。</td>
  </tr>
  <tr>
   <td>Live Copy</td>
   <td>指示頁面何時為即時副本的一部分。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>若要選取可見欄，請將滑鼠停留在欄標題上。 隨即顯示下拉式功能表，您可在其中使用 **欄** 選項。

中頁面旁的顏色 **已發佈** 和 **已修改** 欄指示發佈狀態：

| **欄** | **顏色** | **說明** |
|---|---|---|
| 已發佈 | 綠色 | 發佈成功。 內容已發佈。 |
| 已發佈 | 黃色 | 正在等候發佈。 系統尚未收到發佈的確認。 |
| 已發佈 | 紅色 | 發佈失敗。 未與發佈執行個體建立連線。 這也表示內容已停用。 |
| 已發佈 | *空白* | 此頁面未曾發佈。 |
| 已修改 | 藍色 | 自上次發佈後，頁面已修改。 |
| 已修改 | *空白* | 此頁面從未修改過，或自上次發佈後從未修改過。 |

## 內容功能表 {#context-menus}

Classic UI使用眾所周知的機制來導覽和起始動作，包括按一下和連按兩下。 根據目前的情況，也可以使用一系列前後關聯選單（以滑鼠右鍵開啟）：

![chlimage_1-11](assets/chlimage_1-11a.png)
