---
title: 自訂歡迎控制台（傳統UI）
seo-title: Customizing the Welcome Console (Classic UI)
description: 歡迎控制台提供AEM中各種控制台和功能的連結清單
seo-description: The Welcome console provides a list of links to the various consoles and functionality within AEM
uuid: 4ef20cef-2d7a-417d-b36b-ed4fa56cd511
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2e408acb-3802-4837-8619-688cfc3abfa7
exl-id: 9e171b62-8efb-4143-a202-ba6555658d4b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 8%

---

# 自訂歡迎控制台（傳統UI）{#customizing-the-welcome-console-classic-ui}

>[!CAUTION]
>
>本頁面說明傳統UI。
>
>請參閱 [自訂主控台](/help/sites-developing/customizing-consoles-touch.md) 如需標準觸控式UI的詳細資訊。

歡迎控制台提供AEM中各種控制台和功能的連結清單。

![cq_welcomescreen](assets/cq_welcomescreen.png)

您可以設定可見的連結。 可為特定使用者和/或群組定義。 要採取的動作取決於目標類型（這與其所在控制台的區段相關）:

* [主控制台](#links-in-main-console-left-pane)  — 主控制台中的連結（左窗格）
* [資源、文檔和參考、功能](#links-in-sidebar-right-pane)  — 側欄中的連結（右窗格）

## 主控台中的連結（左窗格） {#links-in-main-console-left-pane}

這會列出AEM的主要主控台。

![cq_welcomescreenmainconsole](assets/cq_welcomescreenmainconsole.png)

### 設定主控台連結是否可見 {#configuring-whether-main-console-links-are-visible}

節點層級權限會決定該連結是否可見。 相關節點包括：

* **網站：** `/libs/wcm/core/content/siteadmin`

* **數位資產:** `/libs/wcm/core/content/damadmin`

* **社群：** `/libs/collab/core/content/admin`

* **促銷活動：** `/libs/mcm/content/admin`

* **收件匣：** `/libs/cq/workflow/content/inbox`

* **使用者:** `/libs/cq/security/content/admin`

* **工具：** `/libs/wcm/core/content/misc`

* **標籤：** `/libs/cq/tagging/content/tagadmin`

例如：

* 若要限制 **工具**，從中刪除讀訪問

   `/libs/wcm/core/content/misc`

請參閱 [安全性部分](/help/sites-administering/security.md) 以取得如何設定所需權限的詳細資訊。

### 側欄中的連結（右窗格） {#links-in-sidebar-right-pane}

![cq_welcomcreensidebar](assets/cq_welcomescreensidebar.png)

這些連結是以 *和* 讀取以下路徑下的節點訪問權限：

`/libs/cq/core/content/welcome`

預設會提供三個區段（稍微間隔）:

<table>
 <tbody>
  <tr>
   <td><strong>資源</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> 雲端服務</td>
   <td><code>/libs/cq/core/content/welcome/resources/cloudservices</code></td>
  </tr>
  <tr>
   <td> 工作流程</td>
   <td><code>/libs/cq/core/content/welcome/resources/workflows</code></td>
  </tr>
  <tr>
   <td> 任務管理</td>
   <td><code>/libs/cq/core/content/welcome/resources/taskmanager</code></td>
  </tr>
  <tr>
   <td> 複製</td>
   <td><code>/libs/cq/core/content/welcome/resources/replication</code></td>
  </tr>
  <tr>
   <td> 報表</td>
   <td><code>/libs/cq/core/content/welcome/resources/reports</code></td>
  </tr>
  <tr>
   <td> 出版物</td>
   <td><code>/libs/cq/core/content/welcome/resources/publishingadmin</code></td>
  </tr>
  <tr>
   <td> 手稿</td>
   <td><code>/libs/cq/core/content/welcome/resources/manuscriptsadmin</code></td>
  </tr>
  <tr>
   <td><strong>檔案與參考</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> 文件</td>
   <td><code>/libs/cq/core/content/welcome/docs/docs</code></td>
  </tr>
  <tr>
   <td> 開發人員資源</td>
   <td><code>/libs/cq/core/content/welcome/docs/dev</code></td>
  </tr>
  <tr>
   <td><strong>功能</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td> CRXDE Lite</td>
   <td><code>/libs/cq/core/content/welcome/features/crxde</code></td>
  </tr>
  <tr>
   <td> 套件</td>
   <td><code>/libs/cq/core/content/welcome/features/packages</code></td>
  </tr>
  <tr>
   <td> 套件共用</td>
   <td><code>/libs/cq/core/content/welcome/features/share</code></td>
  </tr>
  <tr>
   <td> 叢集</td>
   <td><code>/libs/cq/core/content/welcome/features/cluster</code></td>
  </tr>
  <tr>
   <td> 備份</td>
   <td><code>/libs/cq/core/content/welcome/features/backup</code></td>
  </tr>
  <tr>
   <td> Web 主控台<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/config</code></td>
  </tr>
  <tr>
   <td> Web 控制台狀態傾印<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/statusdump</code></td>
  </tr>
 </tbody>
</table>

#### 配置是否顯示側欄連結 {#configuring-whether-sidebar-links-are-visible}

您可以移除對代表連結之節點的讀取存取權，以隱藏連結，不讓特定使用者或群組看到。

* 資源 — 移除以下項目的存取權：

   `/libs/cq/core/content/welcome/resources/<link-target>`

* 檔案 — 移除下列項目的存取權：

   `/libs/cq/core/content/welcome/docs/<link-target>`

* 功能 — 移除下列項目的存取權：

   `/libs/cq/core/content/welcome/features/<link-target>`

例如：

* 移除連結至 **報表**，從中刪除讀訪問

   `/libs/cq/core/content/welcome/resources/reports`

* 移除連結至 **套件**，從中刪除讀訪問

   `/libs/cq/core/content/welcome/features/packages`

請參閱 [安全性部分](/help/sites-administering/security.md) 以取得如何設定所需權限的詳細資訊。

### 連結選擇機制 {#link-selection-mechanism}

在 `/libs/cq/core/components/welcome/welcome.jsp` 使用 [ConsoleUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ConsoleUtil.html)，會對具有屬性的節點執行查詢：

* `jcr:mixinTypes` 值為: `cq:Console`

>[!NOTE]
>
>執行以下查詢以查看現有清單：
>
>* `select * from cq:Console`
>


當使用者或群組對具有mixin的節點沒有讀取權限時 `cq:Console`，則該節點不會被 `ConsoleUtil` 搜尋，因此控制台不會列出它。

### 新增自訂項目 {#adding-a-custom-item}

此 [連結選擇機制](#link-selection-mechanism) 可用來將您自己的自訂項目新增至連結清單。

新增自訂項目至清單 `cq:Console` 混合至您的介面工具集或資源。 這可透過定義屬性來完成：

* `jcr:mixinTypes` 值為: `cq:Console`
