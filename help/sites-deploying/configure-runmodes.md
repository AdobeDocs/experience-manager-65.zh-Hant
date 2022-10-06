---
title: 執行模式
seo-title: Run Modes
description: 了解如何使用執行模式，針對特定用途調整您的AEM執行個體。
seo-description: Learn how to tune your AEM instance for specific purposes by using run modes.
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
feature: Configuring
exl-id: 6d03cb1d-500e-4a23-80e5-347a43dff30e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 1%

---

# 執行模式{#run-modes}

執行模式可讓您針對特定用途調整AEM執行個體；例如，製作或發佈、測試、開發、內部網路或其他。

您可以：

* [為每個運行模式定義配置參數的集合](#defining-configuration-properties-for-a-run-mode).

   所有執行模式都會套用一組基本的設定參數，然後您就可以根據特定環境的用途調整其他設定。 視需要套用。

* [定義要針對特定模式安裝的其他套件組合](#defining-additional-bundles-to-be-installed-for-a-run-mode).

所有設定和定義都儲存在一個存放庫中，並透過設定 **運行模式**.

## 安裝運行模式 {#installation-run-modes}

安裝（或固定）執行模式會在安裝時使用，然後在執行個體的整個存留期中加以修正，則無法變更。

安裝執行模式可立即使用：

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

這是兩對互斥的運行模式；例如，您可以：

* 定義 `author` 或 `publish`，而非同時

* 合併 `author` 為 `samplecontent` 或 `nosamplecontent` （但不能兩者兼有）

>[!CAUTION]
>
>使用上述任一執行模式時（製作、發佈、samplecontent、nosamplecontent），安裝時使用的值會定義 *整個生命期* 那個裝置。
>
>對於這些運行模式，您 *不能* 安裝後進行更改。

## 自訂執行模式 {#customized-run-modes}

您也可以建立自己的自訂執行模式。 可結合這些項目，以涵蓋下列情形：

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* 視需要。..

每次啟動時也可以選擇自訂的執行模式。

## 使用samplecontent和nosamplecontent {#using-samplecontent-and-nosamplecontent}

這些模式可讓您控制範例內容的使用。 在構建快速入門之前定義了示例內容，其中可以包括包、配置等：

* 此 `samplecontent` 運行模式將安裝此內容（預設模式）。

* 此 `nosamplecontent` 模式將不會安裝範例內容。

nosamplecontent執行模式是針對生產安裝而設計。

## 定義運行模式的配置屬性 {#defining-configuration-properties-for-a-run-mode}

配置屬性的值集合（用於特定運行模式）可以保存在儲存庫中。

運行模式由資料夾名稱上的尾碼表示。 這可讓您將所有設定儲存在一個存放庫中。 例如：

* `config`

   適用於所有執行模式

* `config.author`

   用於製作執行模式

* `config.publish`

   用於發佈運行模式

* `config.<run-mode>`

   用於適用的執行模式；例如，設定

請參閱 [儲存庫中的OSGi配置](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) 有關定義這些資料夾中的單個配置節點以及為多個運行模式的組合建立配置的詳細資訊。

>[!NOTE]
>
>針對 [安裝運行模式](#installation-run-modes) （例如作者）安裝後無法變更執行模式。 但是，對單個配置屬性的更改將在重新啟動後生效。

## 定義要為運行模式安裝的其他套件組合 {#defining-additional-bundles-to-be-installed-for-a-run-mode}

還可以指定應為特定運行模式安裝的其他套件。 對於這些定義，安裝資料夾用於保存套件組合。 運行模式再次以前置詞表示：

* `install.author`
* `install.publish`

這些資料夾屬於 `nt:folder` 和應包含適當的套件組合。

## 以特定執行模式啟動CQ {#starting-cq-with-a-specific-run-mode}

如果您已為多個執行模式定義了配置，則需要定義啟動時要使用的配置。 有幾種方法可指定要使用的執行模式；決議的順序是：

1. [ ](#using-the-sling-properties-file)
1. [ ](#using-the-r-option)
1. [系統屬性(](#using-a-system-property-in-the-start-script)

1. [檔案名檢測](#filename-detection-renaming-the-jar-file)

使用應用程式伺服器時，您也可以 [在web.xml中定義運行模式](#defining-the-run-mode-in-web-xml-with-application-server).

### 使用sling.properties檔案 {#using-the-sling-properties-file}

此 `sling.properties` 檔案可用來定義所需的執行模式：

1. 編輯配置檔案：

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. 新增下列屬性；以下範例適用於author:

   `sling.run.modes=author`

### 使用 — r選項 {#using-the-r-option}

自訂執行模式可使用 `-r` 選項。 例如，使用下列命令啟動將執行模式設為dev的AEM例項。&quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### 在啟動指令碼中使用系統屬性 {#using-a-system-property-in-the-start-script}

啟動指令碼中的系統屬性可用於指定運行模式。

* 例如，使用下列工具將執行個體啟動為位於美國的生產發佈執行個體：

   `-Dsling.run.modes=publish,prod,us`

### 檔案名檢測 — 更名jar檔案 {#filename-detection-renaming-the-jar-file}

在安裝之前，可通過更名安裝jar檔案來激活以下兩種安裝運行模式：

* 發佈
* 作者

jar檔案必須使用命名慣例：

`cq5-<run-mode>-p<port-number>`

例如，設定 `publish` 通過命名jar檔案來運行模式：

`cq5-publish-p4503`

### 在web.xml中定義運行模式（使用Application Server） {#defining-the-run-mode-in-web-xml-with-application-server}

使用應用程式伺服器時，您也可以配置屬性：

`sling.run.modes`

檔案中：

`WEB-INF/web.xml`

這是在AEM `war` 檔案和應在部署前更新。

請參閱 [使用應用程式伺服器安裝AEM](/help/sites-deploying/application-server-install.md) 以取得詳細資訊。
