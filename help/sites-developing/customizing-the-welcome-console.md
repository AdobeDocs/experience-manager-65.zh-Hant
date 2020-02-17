---
title: 自訂歡迎控制台(Classic UI)
seo-title: 自訂歡迎控制台(Classic UI)
description: Welcome console提供AEM中各種主控台與功能的連結清單
seo-description: Welcome console提供AEM中各種主控台與功能的連結清單
uuid: 4ef20cef-2d7a-417d-b36b-ed4fa56cd511
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2e408acb-3802-4837-8619-688cfc3abfa7
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 自訂歡迎控制台(Classic UI){#customizing-the-welcome-console-classic-ui}

>[!CAUTION]
>
>本頁面處理傳統UI。
>
>如需 [標準觸控式UI的詳細資訊，請參閱自訂控制台](/help/sites-developing/customizing-consoles-touch.md) 。

歡迎控制台提供AEM中各控制台和功能的連結清單。

![cq_welcomescreen](assets/cq_welcomescreen.png)

您可以設定可見的連結。 這可針對特定使用者和／或群組定義。 要採取的操作取決於目標類型（與其所在控制台的部分相關）:

* [主控制台](#links-in-main-console-left-pane) -主控制台中的連結（左窗格）
* [資源、檔案和參考、功能](#links-in-sidebar-right-pane) -側邊欄（右窗格）中的連結

## 主控台中的連結（左窗格） {#links-in-main-console-left-pane}

這會列出AEM的主控制台。

![cq_welcomescreenmainconsole](assets/cq_welcomescreenmainconsole.png)

### 配置主控制台連結是否可見 {#configuring-whether-main-console-links-are-visible}

節點層級權限決定連結是否可見。 相關節點包括：

* **** 網站： `/libs/wcm/core/content/siteadmin`

* **數位資產:** `/libs/wcm/core/content/damadmin`

* **** 社群： `/libs/collab/core/content/admin`

* **** 促銷活動： `/libs/mcm/content/admin`

* **** 收件匣： `/libs/cq/workflow/content/inbox`

* **** 使用者： `/libs/cq/security/content/admin`

* **** 工具： `/libs/wcm/core/content/misc`

* **** 標籤： `/libs/cq/tagging/content/tagadmin`

例如：

* 若要限制對「工具」 **的存取**，請移除

   `/libs/wcm/core/content/misc`

如需如何 [設定所需權限的詳細資訊](/help/sites-administering/security.md) ，請參閱「安全性」區段。

### 側欄中的連結（右窗格） {#links-in-sidebar-right-pane}

![cq_welcomescreensidebar](assets/cq_welcomescreensidebar.png)

這些連結基於以下路徑下 *的節點存* 在和讀取訪問權：

`/libs/cq/core/content/welcome`

預設提供三個區段（稍微間隔）:

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
   <td> 複寫</td>
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
   <td> 封裝</td>
   <td><code>/libs/cq/core/content/welcome/features/packages</code></td>
  </tr>
  <tr>
   <td> Package Share</td>
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
   <td> Web 控制台<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/config</code></td>
  </tr>
  <tr>
   <td> Web 控制台狀態傾印<br /> </td>
   <td><code>/libs/cq/core/content/welcome/features/statusdump</code></td>
  </tr>
 </tbody>
</table>

#### 配置邊欄連結是否可見 {#configuring-whether-sidebar-links-are-visible}

移除代表連結之節點的讀取存取權，即可隱藏連結給特定使用者或群組。

* 資源——刪除對以下內容的訪問：

   `/libs/cq/core/content/welcome/resources/<link-target>`

* 文檔——刪除對以下內容的訪問：

   `/libs/cq/core/content/welcome/docs/<link-target>`

* 功能——移除對下列項目的存取權：

   `/libs/cq/core/content/welcome/features/<link-target>`

例如：

* 若要移除報表的連 **結**，請移除

   `/libs/cq/core/content/welcome/resources/reports`

* 要刪除包連結 ****，請從

   `/libs/cq/core/content/welcome/features/packages`

如需如何 [設定所需權限的詳細資訊](/help/sites-administering/security.md) ，請參閱「安全性」區段。

### 連結選擇機制 {#link-selection-mechanism}

使 `/libs/cq/core/components/welcome/welcome.jsp` 用中由 [ConsoleUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/ConsoleUtil.html)組成，它對具有以下屬性的節點執行查詢：

* `jcr:mixinTypes` 值： `cq:Console`

>[!NOTE]
>
>執行下列查詢以查看現有清單：
>
>* `select * from cq:Console`
>



當用戶或組對具有混頻的節點沒有讀取權限時 `cq:Console`，搜索將不檢索該節 `ConsoleUtil` 點，因此該節點不列在控制台中。

### 新增自訂項目 {#adding-a-custom-item}

連結 [選擇機制](#link-selection-mechanism) ，可用來將您自己的自訂項目新增至連結清單。

將混音新增至介面工具集或資源，將自訂 `cq:Console` 項目新增至清單。 通過定義屬性來完成此操作：

* `jcr:mixinTypes` 值： `cq:Console`

