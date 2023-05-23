---
title: 自定義歡迎控制台(Classic UI)
seo-title: Customizing the Welcome Console (Classic UI)
description: 「歡迎」控制台提供指向以下各種控制台和功能的連結列AEM表
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

# 自定義歡迎控制台(Classic UI){#customizing-the-welcome-console-classic-ui}

>[!CAUTION]
>
>此頁面處理經典UI。
>
>請參閱 [自定義控制台](/help/sites-developing/customizing-consoles-touch.md) 的子菜單。

「歡迎」控制台提供指向中各種控制台和功能的鏈AEM接。

![cq_welcomscreen](assets/cq_welcomescreen.png)

可以配置可見的連結。 這可以為特定用戶和/或組定義。 要執行的操作取決於目標類型（與其所在控制台的部分相關）:

* [主控制台](#links-in-main-console-left-pane)  — 主控制台（左窗格）中的連結
* [資源、文檔和參考、功能](#links-in-sidebar-right-pane)  — 提要欄（右窗格）中的連結

## 主控制台中的連結（左窗格） {#links-in-main-console-left-pane}

這列出了的主控制AEM台。

![cq_welcomcreenmainconsole](assets/cq_welcomescreenmainconsole.png)

### 配置主控制台連結是否可見 {#configuring-whether-main-console-links-are-visible}

節點級別權限決定連結是否可見。 所討論的節點是：

* **網站：** `/libs/wcm/core/content/siteadmin`

* **數位資產:** `/libs/wcm/core/content/damadmin`

* **社區：** `/libs/collab/core/content/admin`

* **市場活動：** `/libs/mcm/content/admin`

* **收件箱：** `/libs/cq/workflow/content/inbox`

* **使用者:** `/libs/cq/security/content/admin`

* **工具：** `/libs/wcm/core/content/misc`

* **標籤：** `/libs/cq/tagging/content/tagadmin`

例如：

* 要限制訪問 **工具**，刪除讀取訪問

   `/libs/wcm/core/content/misc`

查看 [安全科](/help/sites-administering/security.md) 的子菜單。

### 提要欄中的連結（右窗格） {#links-in-sidebar-right-pane}

![cq_welcomcreen邊欄](assets/cq_welcomescreensidebar.png)

這些連結是基於 *和* 讀取對以下路徑下節點的訪問：

`/libs/cq/core/content/welcome`

預設情況下，有三個部分（稍微間隔）:

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
   <td> 報告</td>
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
   <td><strong>文檔和參考</strong></td>
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

#### 配置邊欄連結是否可見 {#configuring-whether-sidebar-links-are-visible}

通過刪除對代表連結的節點的讀取訪問，可以隱藏特定用戶或組的連結。

* 資源 — 刪除對以下項的訪問：

   `/libs/cq/core/content/welcome/resources/<link-target>`

* 文檔 — 刪除對以下內容的訪問：

   `/libs/cq/core/content/welcome/docs/<link-target>`

* 功能 — 刪除對以下內容的訪問：

   `/libs/cq/core/content/welcome/features/<link-target>`

例如：

* 刪除到的連結 **報告**，刪除讀取訪問

   `/libs/cq/core/content/welcome/resources/reports`

* 刪除到的連結 **包**，刪除讀取訪問

   `/libs/cq/core/content/welcome/features/packages`

查看 [安全科](/help/sites-administering/security.md) 的子菜單。

### 連結選擇機制 {#link-selection-mechanism}

在 `/libs/cq/core/components/welcome/welcome.jsp` 使用 [ConsoleUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ConsoleUtil.html)，它對具有以下屬性的節點執行查詢：

* `jcr:mixinTypes` 值為: `cq:Console`

>[!NOTE]
>
>執行以下查詢以查看現有清單：
>
>* `select * from cq:Console`
>


當用戶或組對具有混合的節點沒有讀取權限時 `cq:Console`，該節點不由 `ConsoleUtil` 搜索，因此它未列在控制台中。

### 添加自定義項 {#adding-a-custom-item}

的 [鏈路選擇機制](#link-selection-mechanism) 可用於將您自己的自定義項添加到連結清單。

通過添加 `cq:Console` 混合到小部件或資源。 這可以通過定義屬性來完成：

* `jcr:mixinTypes` 值為: `cq:Console`
