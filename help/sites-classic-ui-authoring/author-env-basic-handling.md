---
title: 基本處理
description: 使用作者環境時基本處理AEM的概述。 它以站點控制台為基礎。
uuid: ab488d7c-7b7f-4a23-a80c-99d37ac84246
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 9737ead9-e324-43c9-9780-7abd292f4e5b
exl-id: 2981dc20-b2ba-4ea2-a53b-8b5fe526aa9c
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 4%

---

# 基本處理{#basic-handling}

>[!NOTE]
>
>* 此頁面旨在概述使用作者環境時的基AEM本處理。 它使用 **站點** 控制台。
>
>* 某些功能並非在所有控制台中都可用，而/或某些控制台中有其他功能。 有關各個控制台及其相關功能的具體資訊將在其他頁面中詳細介紹。
>* 鍵盤快捷鍵在整個區域都AEM可用。 特別是 [使用控制台](/help/sites-classic-ui-authoring/author-env-keyboard-shortcuts.md) 和 [編輯頁](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)。
>


## 歡迎螢幕 {#the-welcome-screen}

經典UI提供了一系列控制台，使用眾所周知的導航和啟動操作機制，包括按一下、按兩下和 [上下文菜單](#context-menus)。

登錄後，將顯示「歡迎」螢幕，其中提供了指向控制台和服務的連結清單：

![screen_shot_2012-01-30at61745pm](assets/screen_shot_2012-01-30at61745pm.png)

## 控制台 {#consoles}

主控制台包括：

<table>
 <tbody>
  <tr>
   <td><strong>主控台</strong></td>
   <td><strong>用途</strong></td>
  </tr>
  <tr>
   <td><strong>歡迎</strong></td>
   <td>提供對的主要功能的概述和直接訪問（通過連結）AEM。</td>
  </tr>
  <tr>
   <td><strong>數位資產</strong><br /> </td>
   <td>這些控制台允許您導入和 <a href="/help/sites-classic-ui-authoring/classicui-assets.md">管理數字資產</a> 如影像、視頻、文檔和音頻檔案。 然後，在同一實例上運行的任何網站都可以使用這些AEM資產。 </td>
  </tr>
  <tr>
   <td><strong>Launch</strong></td>
   <td>這有助於您管理 <a href="/help/sites-classic-ui-authoring/classic-launches.md">啟動</a>;這些功能使您能夠為將來發佈的一個或多個激活網頁開發內容。<br /> <i>注：在啟用觸摸功能的UI中，「站點」控制台和「參考」欄中提供了大部分相同的功能。</i> <i>如果需要，此控制台可從工具控制台獲得；依次選擇操作和啟動。</i></td>
  </tr>
  <tr>
   <td><strong>收件匣 </strong></td>
   <td>在很多情況下，工作流的子任務中涉及許多人，每個人必須先完成其步驟，然後才能將工作交給下一個人。 「收件箱」允許您查看與此類任務相關的通知。 請參閱 <a href="/help/sites-administering/workflows.md">使用工作流</a>。 <br /> </td>
  </tr>
  <tr>
   <td><strong>標記</strong></td>
   <td>通過「標籤」控制台，您可以管理標籤。 標籤是短名稱或短語，您可以使用這些短名稱或短語來對內容分類和注釋，使查找和組織內容更加容易。 有關詳細資訊，請參閱 <a href="/help/sites-classic-ui-authoring/classic-feature-tags.md">使用和管理標籤</a>。</td>
  </tr>
  <tr>
   <td><strong>工具</strong></td>
   <td>的 <a href="/help/sites-administering/tools-consoles.md">工具控制台</a> 提供對多種專用工具和控制台的訪問，這些工具和控制台可幫助您管理網站、數字資產和內容儲存庫的其他方面。</td>
  </tr>
  <tr>
   <td><strong>使用者</strong></td>
   <td>這些控制台允許您管理用戶和組的訪問權限。 有關完整詳細資訊，請參閱 <a href="/help/sites-administering/security.md">用戶管理和安全</a>。<br /> </td>
  </tr>
  <tr>
   <td><strong>網站</strong></td>
   <td>站點/網站控制台允許您 <a href="/help/sites-classic-ui-authoring/classic-page-author.md">建立、查看和管理網站</a> 運行AEM。 通過這些控制台，您可以建立、複製、移動和刪除網站頁面、啟動工作流以及激活（發佈）頁面。 也可以開啟頁面進行編輯。<br /> </td>
  </tr>
  <tr>
   <td><strong>工作流程</strong></td>
   <td>工作流是定義的一系列步驟，描述了完成某些任務的過程。 在很多情況下，有許多人參與一項任務，每個人必須先完成自己的步驟，然後才能將工作交給下一個人。 使用「工作流」控制台可以生成工作流模型並管理正在運行的工作流實例。 請參閱 <a href="/help/sites-administering/workflows.md">使用工作流</a>。<br /> </td>
  </tr>
 </tbody>
</table>

的 **網站** console提供了兩個窗格，供您瀏覽和管理頁面：

* 左窗格

   這顯示了網站的樹結構和這些網站中的頁面。

   它還顯示了其他方面或AEM包括項目、藍圖和資產的資訊。

* 右窗格

   這顯示頁面（位於左窗格中選定的位置），可用於執行操作。

從這裡你可以 [管理頁面](/help/sites-authoring/managing-pages.md) 使用工具欄、上下文菜單或開啟頁面以執行進一步操作。

>[!NOTE]
>
>所有控制台的基本處理都相同。 本節集中介紹 **網站** 控制台，因為它是創作時使用的主控制台。

![chlimage_1-9](assets/chlimage_1-9a.png)

## 訪問幫助 {#accessing-help}

在各種控制台（如網站）上， **幫助** 按鈕可用，這將開啟包共用或文檔站點。

![chlimage_1-10](assets/chlimage_1-10a.png)

編輯頁面時 [sidekick還具有訪問幫助的按鈕](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#accessing-help)。

## 使用網站控制台導航 {#navigating-with-the-websites-console}

的 **網站** 控制台以樹形結構（左窗格）列出內容頁面。 為便於導航，可根據需要展開(+)或折疊(-)樹結構的部分：

* 按一下頁面名稱（在左窗格中）將：

   * 在右窗格中列出子頁
   * 同時展開左窗格中的結構。

      出於效能原因，此操作取決於子節點數。 在標準安裝下，此擴展方法在有 `30` 或更少子節點。

* 按兩下頁面名稱（左窗格）也會展開樹，儘管在開啟頁面的同時，效果並不明顯。

>[!NOTE]
>
>此預設值( `30`)可以按控制台更改站點管理小部件的應用程式特定配置：
>
>在siteadmin節點上：
>
>設定屬性的值：
>`treeAutoExpandMax`
>於:
>`/apps/wcm/core/content/siteadmin`
>
>或者全球主題：
>設定值：
>`TREE_AUTOEXPAND_MAX`
>中的:
>`/apps/cq/ui/widgets/themes/default/widgets/wcm/SiteAdmin.js`
>
>請參閱 [CQ小部件API中的SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin) 的子菜單。

## 網站控制台上的頁面資訊 {#page-information-on-the-websites-console}

右窗格 **網站** console提供清單視圖，其中包含有關頁面的資訊：

![頁面資訊](assets/page-info.png)

以下內容可供使用：這些欄位的子集顯示為預設值：

<table>
 <tbody>
  <tr>
   <td><strong>欄</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>縮圖</td>
   <td>顯示頁面的縮略圖。</td>
  </tr>
  <tr>
   <td>標題</td>
   <td>頁面上顯示的標題</td>
  </tr>
  <tr>
   <td>名稱</td>
   <td>該名AEM稱指頁面</td>
  </tr>
  <tr>
   <td>已發佈</td>
   <td>指示是否已發佈該頁並提供發佈日期和時間。</td>
  </tr>
  <tr>
   <td>修改時間</td>
   <td>指示是否已修改頁面並提供修改日期和時間。 要保存任何修改，必須激活頁面。</td>
  </tr>
  <tr>
   <td>Scene7出版</td>
   <td>指示該頁是否已發佈到Scene7。<br /> </td>
  </tr>
  <tr>
   <td>狀態</td>
   <td>指示頁面的當前狀態，如頁面是工作流還是livecopy的一部分，或當前是否鎖定頁面。</td>
  </tr>
  <tr>
   <td>印象</td>
   <td>以點擊次數顯示頁面上的活動。</td>
  </tr>
  <tr>
   <td>範本</td>
   <td>指示頁面所基於的模板。</td>
  </tr>
  <tr>
   <td>在工作流程中</td>
   <td>指示頁面在工作流中的時間。</td>
  </tr>
  <tr>
   <td>鎖定者: </td>
   <td>顯示頁面被鎖定的時間和鎖定該頁面的用戶帳戶。</td>
  </tr>
  <tr>
   <td>Live Copy</td>
   <td>指示頁面是即時副本的一部分的時間。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>要選擇可見列，請將滑鼠懸停在列標題上。 將顯示一個下拉菜單，您可以從此處使用 **列** 的雙曲餘切值。

中頁面旁邊的顏色 **已發佈** 和 **已修改** 列指示發佈狀態：

| **欄** | **彩色** | **說明** |
|---|---|---|
| 已發佈 | 綠色 | 發佈成功。 內容已發佈。 |
| 已發佈 | 黃色 | 發佈掛起。 系統尚未收到發佈確認。 |
| 已發佈 | 紅色 | 發行失敗. 與發佈實例沒有連接。 這也可能意味著內容已停用。 |
| 已發佈 | *blank* | 此頁從未發佈。 |
| 修改時間 | 藍色 | 自上次發佈以來已修改頁面。 |
| 修改時間 | *blank* | 自上次發佈以來，此頁從未被修改過，或未被修改過。 |

## 上下文菜單 {#context-menus}

經典UI使用眾所周知的機制來導航和啟動操作，包括按一下和按兩下。 根據當前情況，還提供了一系列上下文菜單（通常使用滑鼠右鍵開啟）:

![chlimage_1-11](assets/chlimage_1-11a.png)
