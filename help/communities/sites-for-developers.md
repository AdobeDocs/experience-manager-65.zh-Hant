---
title: 社區網站要點
seo-title: Community Site Essentials
description: 導出和刪除社區網站並建立自定義網站模板
seo-description: Exporting and deleting community sites and creating custom site templates
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
exl-id: 1dc568cd-315c-4944-9a3e-e5d7794e5dc0
source-git-commit: cc0574ae22758d095a3ca6b91f0ceae4a8691f0e
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# 社區網站要點 {#community-site-essentials}

## 自定義網站模板 {#custom-site-template}

可以為社區站點的每個語言副本單獨指定自定義站點模板。

為此：

* 建立自定義模板。
* 覆蓋預設站點模板路徑。
* 將自定義模板添加到覆蓋路徑。
* 通過添加 `page-template` 屬性 `configuration` 的下界。

**預設模板**:

`/libs/social/console/components/hbs/sitepage/sitepage.hbs`

**覆蓋路徑中的自定義模板**:

`/apps/social/console/components/hbs/sitepage/template-name.hbs`

**屬性**:頁面模板

**類型**:字串

**值**: `template-name` （無擴展）

**配置節點**:

`/content/community site path/lang/configuration`

例如：`/content/sites/engage/en/configuration`

>[!NOTE]
>
>重疊路徑中的所有節點只需為類型 `Folder`。

>[!CAUTION]
>
>如果為自定義模板指定名稱 *站點頁面.hbs*，則將自定義所有社區站點。

### 自定義網站模板示例 {#custom-site-template-example}

例如， `vertical-sitepage.hbs` 是一個站點模板，它導致菜單連結在頁面左側垂直放置，而不是橫幅下方水準放置。

[獲取檔案](assets/vertical-sitepage.hbs)
將自定義站點模板置於覆蓋資料夾中：

`/apps/social/console/components/hbs/sitepage/vertical-sitepage.hbs`

通過添加 `page-template` 配置節點的屬性：

`/content/sites/sample/en/configuration`

![crxde站點配置](assets/crxde-siteconfiguration.png)

一定要 **全部保存** 並將自定義代碼複製AEM到所有實例（當從控制台發佈社區站點內容時，不包括自定義代碼）。

複製自定義代碼的建議做法是 [建立包](../../help/sites-administering/package-manager.md#creating-a-new-package) 並在所有實例上部署。

## 導出社區站點 {#exporting-a-community-site}

建立社區站點後，可以將該站點導出為儲存在包管理器AEM中且可供下載和上載的包。

可從 [社區站點控制台](sites-console.md#exporting-the-site)。

請注意，社區網站包中不包含UGC和自定義代碼。

要導出UGC，請使用 [AEM CommunitiesUGC遷移工具](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration),GitHub上提供的開源遷移工具。

## 刪除社區站點 {#deleting-a-community-site}

從AEM Communities6.3 Service Pack 1開始，「刪除站點」表徵圖將出現在社區站點上方 **[!UICONTROL 社區]** > **[!UICONTROL 站點]** 控制台。 在開發過程中，如果希望刪除社區站點並開始刷新，則可以使用此功能。 刪除社區站點，刪除與該站點關聯的以下項目：

* [UGC](#user-generated-content)
* [使用者群組](#community-user-groups)
* [資料庫記錄](#database-records)

### 社區唯一站點ID {#community-unique-site-id}

要使用CRXDE標識與社區站點關聯的唯一站點ID，請執行以下操作：

* 導航到站點的語言根，如 `/content/sites/*<site name>*/en/rep:policy`。

* 查找 `allow<#>` 節點 `rep:principalName` 的 `rep:principalName = *community-enable-nrh9h-members*`。

* 站點ID是 `rep:principalName`

   例如，如果 `rep:principalName = community-enable-nrh9h-members`

   * **站點名稱** = *啟用*
   * **站點ID** = *nh*
   * **唯一站點ID** = *啟用nrh9h*

### 使用者產生的內容 {#user-generated-content}

從Github獲取社區 — srp-tools項目：

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

這包含一個Servlet，用於從任何SRP中刪除所有UGC。

可以刪除所有UGC或特定站點，例如：

* `path=/content/usergenerated/asi/mongo/content/sites/engage`

這只會刪除用戶生成的內容（在發佈時輸入）和未創作的內容（在作者時輸入）。 所以， [陰影節點](srp.md#shadownodes) 不受影響。

### 社區用戶組 {#community-user-groups}

在所有作者和發佈實例上，從 [安全控制台](../../help/sites-administering/security.md)，查找並刪除 [用戶組](users.md) 即：

* 前置詞為 `community`
* 後跟 [唯一站點id](#community-unique-site-id)

比如說， `community-engage-x0e11-members`。
