---
title: 基本處理
seo-title: 基本處理
description: 概略說明使用AEM製作環境時的基本處理方式。 它會以Sites主控台為基礎。
seo-description: 概略說明使用AEM製作環境時的基本處理方式。 它會以Sites主控台為基礎。
uuid: ab488d7c-7b7f-4a23-a80c-99d37ac84246
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 9737ead9-e324-43c9-9780-7abd292f4e5b
exl-id: 2981dc20-b2ba-4ea2-a53b-8b5fe526aa9c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 4%

---

# 基本處理{#basic-handling}

>[!NOTE]
>
>* 本頁旨在概述使用AEM製作環境時的基本處理方式。 它以&#x200B;**Sites**&#x200B;控制台為基礎。
   >
   >
* 並非所有主控台都提供某些功能，而/或某些主控台提供其他功能。 有關個別主控台及其相關功能的特定資訊，將在其他頁面上詳細說明。
>* AEM提供鍵盤快速鍵。 尤其是當[使用主控台](/help/sites-classic-ui-authoring/author-env-keyboard-shortcuts.md)和[編輯頁面](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)時。

>



## 歡迎螢幕{#the-welcome-screen}

傳統UI提供一系列控制台，使用眾所周知的機制來導覽和啟動動作，包括點按、按兩下和[內容功能表](#context-menus)。

登入時，將會顯示歡迎畫面，提供主控台與服務的連結清單：

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
   <td>提供AEM主要功能的概述和直接存取（透過連結）。</td>
  </tr>
  <tr>
   <td><strong>數位資產</strong><br /> </td>
   <td>這些主控台可讓您匯入和<a href="/help/sites-classic-ui-authoring/classicui-assets.md">管理數位資產</a>，例如影像、視訊、檔案和音訊檔案。 然後，在相同AEM例項上執行的任何網站都可以使用這些資產。 </td>
  </tr>
  <tr>
   <td><strong>啟動</strong></td>
   <td>這可協助您管理<a href="/help/sites-classic-ui-authoring/classic-launches.md">launches</a>;這些功能可讓您開發內容，以供日後發行一或多個已啟動的網頁使用。<br /> <i>注意：在觸控式UI中，Sites主控台和「參考」邊欄提供大部分相同的功能。</i> <i>如有需要，此控制台可從「工具」控制台使用；依次選擇操作和啟動。</i></td>
  </tr>
  <tr>
   <td><strong>收件匣 </strong></td>
   <td>在許多情況下，許多人都參與了工作流的子任務，每個人必須先完成其步驟，然後才將工作交給下一個人。 收件箱允許您查看與此類任務相關的通知。 請參閱<a href="/help/sites-administering/workflows.md">使用工作流程</a>。 <br /> </td>
  </tr>
  <tr>
   <td><strong>標記</strong></td>
   <td>「標籤」主控台可讓您管理標籤。 標籤是短名稱或片語，您可使用這些名稱或片語來分類及註解內容片段，以便更輕鬆尋找和組織內容。 如需詳細資訊，請參閱<a href="/help/sites-classic-ui-authoring/classic-feature-tags.md">使用和管理標籤</a>。</td>
  </tr>
  <tr>
   <td><strong>工具</strong></td>
   <td><a href="/help/sites-administering/tools-consoles.md">工具主控台</a>提供對多種專用工具和主控台的訪問，這些工具和主控台可幫助您管理您的網站、數字資產和內容儲存庫的其他方面。</td>
  </tr>
  <tr>
   <td><strong>使用者</strong></td>
   <td>這些主控台可讓您管理使用者和群組的存取權限。 如需完整詳細資訊，請參閱<a href="/help/sites-administering/security.md">使用者管理與安全性</a>。<br /> </td>
  </tr>
  <tr>
   <td><strong>網站</strong></td>
   <td>「網站/網站」主控台可讓您<a href="/help/sites-classic-ui-authoring/classic-page-author.md">建立、檢視及管理AEM執行個體上執行的網站</a>。 透過這些主控台，您可以建立、複製、移動和刪除網站頁面、啟動工作流程，以及啟用（發佈）頁面。 您也可以開啟頁面進行編輯。<br /> </td>
  </tr>
  <tr>
   <td><strong>工作流程</strong></td>
   <td>工作流程是一系列已定義的步驟，用於描述完成某些任務的過程。 在許多情況下，許多人參與了一項任務，每個人必須完成其步驟，然後才將工作交給下一個人。 工作流程控制台可讓您建立工作流程模型並管理執行中的工作流程例項。 請參閱<a href="/help/sites-administering/workflows.md">使用工作流程</a>。<br /> </td>
  </tr>
 </tbody>
</table>

**網站**&#x200B;控制台提供兩個窗格，供您導覽和管理您的頁面：

* 左窗格

   這會顯示您網站的樹狀結構，以及這些網站內的頁面。

   它還顯示了其他方面或AEM的資訊，包括項目、藍圖和資產。

* 右窗格

   這會顯示頁面（在左窗格中選取的位置），並可用於執行動作。

從這裡，您可以使用工具列、內容功能表或開啟頁面以執行進一步動作，[管理您的頁面](/help/sites-authoring/managing-pages.md)。

>[!NOTE]
>
>所有主控台的基本處理都相同。 本節將重點放在&#x200B;**Websites**&#x200B;控制台上，因為它是創作時使用的主控制台。

![chlimage_1-9](assets/chlimage_1-9a.png)

## 訪問幫助{#accessing-help}

在各種主控台（例如網站）上，也有&#x200B;**Help**&#x200B;按鈕可供使用，這將會開啟「封裝共用」或檔案網站。

![chlimage_1-10](assets/chlimage_1-10a.png)

編輯頁面時，[sidekick也有一個用於存取help](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#accessing-help)的按鈕。

## 使用網站控制台進行導航{#navigating-with-the-websites-console}

**Websites**&#x200B;控制台以樹結構（左窗格）列出您的內容頁。 為了便於導航，樹結構的部分可以根據需要展開(+)或折疊(-):

* 按一下頁面名稱（位於左窗格）將：

   * 在右窗格中列出子頁
   * 也展開左窗格中的結構。

      由於效能原因，此動作取決於子節點數。 在標準安裝中，當`30`或更少的子節點時，此擴展方法就可工作。

* 按兩下頁面名稱（左窗格）也會展開樹狀結構，但由於頁面同時開啟，因此效果並不明顯。

>[!NOTE]
>
>在網站管理員介面工具集的應用程式特定配置中，此預設值(`30`)可針對每個控制台進行更改：
>
>在網站管理員節點上：
>
>設定屬性的值：
>`treeAutoExpandMax`
>於:
>`/apps/wcm/core/content/siteadmin`
>
>或是全球性的主題：
>設定值：
>`TREE_AUTOEXPAND_MAX`
>在:
>`/apps/cq/ui/widgets/themes/default/widgets/wcm/SiteAdmin.js`
>
>如需詳細資訊，請參閱CQ Widget API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)中的[ SiteAdmin 。

## 網站控制台上的頁面資訊{#page-information-on-the-websites-console}

**Websites**&#x200B;控制台的右窗格提供清單視圖，其中包含有關頁面的資訊：

![頁面資訊](assets/page-info.png)

下列功能可供使用；這些欄位的子集如預設所示：

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
   <td>名稱AEM代表頁面</td>
  </tr>
  <tr>
   <td>已發佈</td>
   <td>指出頁面是否已發佈，並提供發佈日期和時間。</td>
  </tr>
  <tr>
   <td>修改時間</td>
   <td>指出頁面是否已修改，並提供修改日期和時間。 若要儲存任何修改，您必須啟動頁面。</td>
  </tr>
  <tr>
   <td>Scene7 Publish</td>
   <td>指出頁面是否已發佈至Scene7。<br /> </td>
  </tr>
  <tr>
   <td>狀態</td>
   <td>指出頁面的目前狀態，例如頁面是工作流程的一部分還是Live Copy，或頁面目前是否已鎖定。</td>
  </tr>
  <tr>
   <td>印象</td>
   <td>以點擊次數顯示頁面上的活動。</td>
  </tr>
  <tr>
   <td>範本</td>
   <td>指出頁面所依據的範本。</td>
  </tr>
  <tr>
   <td>在工作流程中</td>
   <td>指出頁面何時處於工作流程中。</td>
  </tr>
  <tr>
   <td>鎖定者: </td>
   <td>顯示頁面已鎖定的時間以及已鎖定的使用者帳戶。</td>
  </tr>
  <tr>
   <td>即時副本</td>
   <td>指出頁面是即時副本的一部分。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>若要選取可見欄，請將滑鼠移至欄標題上。 下拉式功能表隨即顯示，您可從此處使用&#x200B;**Columns**&#x200B;選項。

**Published**&#x200B;和&#x200B;**Modified**&#x200B;欄中頁面旁的顏色指示發佈狀態：

| **欄** | **彩色** | **說明** |
|---|---|---|
| 已發佈 | 綠色 | 發佈成功。 內容已發佈。 |
| 已發佈 | 黃色 | 發佈掛起。 系統尚未收到發佈確認。 |
| 已發佈 | 紅色 | 發行失敗. 與發佈執行個體沒有連線。 這也代表內容已停用。 |
| 已發佈 | *blank* | 此頁面從未發佈。 |
| 修改時間 | 藍色 | 自上次發佈後已修改頁面。 |
| 修改時間 | *空白* | 自上次發佈後，此頁從未被修改過，也未被修改過。 |

## 內容菜單{#context-menus}

傳統UI使用眾所周知的機制來導覽和啟動動作，包括點按和點按兩下。 根據當前情況，還提供了一系列上下文菜單（通常使用右鍵開啟）:

![chlimage_1-11](assets/chlimage_1-11a.png)
