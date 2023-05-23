---
title: 執行模式
seo-title: Run Modes
description: 瞭解如何使用運AEM行模式來調整實例以達到特定目的。
seo-description: Learn how to tune your AEM instance for specific purposes by using run modes.
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
feature: Configuring
exl-id: 6d03cb1d-500e-4a23-80e5-347a43dff30e
source-git-commit: 7d91fbdaae7ade27e9d6bf42bbcd5b16d3f6e358
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 1%

---

# 執行模式{#run-modes}

運行模式允許您針對AEM特定目的調整實例；例如，作者或發佈、test、開發、內部網或其他。

您可以：

* [為每個運行模式定義配置參數的集合](#defining-configuration-properties-for-a-run-mode)。

   所有運行模式都應用了一組基本的配置參數，然後您可以根據特定環境的目的調整其它設定。 這些將根據需要應用。

* [定義要針對特定模式安裝的附加捆綁包](#defining-additional-bundles-to-be-installed-for-a-run-mode)。

所有設定和定義都儲存在一個儲存庫中，並通過設定 **運行模式**。

## 安裝運行模式 {#installation-run-modes}

安裝（或固定）運行模式在安裝時使用，然後在實例的整個生命週期內對其進行固定，這些模式不能更改。

安裝運行模式是現成的：

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

這是兩對相互排斥的運行模式；例如，您可以：

* 定義 `author` 或 `publish`，不同時進行

* 聯合 `author` 或 `samplecontent` 或 `nosamplecontent` （但不是兩者兼有）

>[!CAUTION]
>
>使用上述運行模式之一（作者、發佈、示例、nosamplecontent）時，在安裝時使用的值定義了 *整整一生* 那個裝置。
>
>對於這些運行模式， *不能* 安裝後更改。

## 自定義運行模式 {#customized-run-modes}

您還可以建立自己的、自定義的運行模式。 這些可以合併，以涵蓋以下情形：

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* 按鈕。。。

在每次啟動時也可以選擇自定義運行模式。

## 使用樣本和無示例 {#using-samplecontent-and-nosamplecontent}

這些模式允許您控制示例內容的使用。 示例內容在快速啟動構建之前定義，可包括包、配置等：

* 的 `samplecontent` 運行模式將安裝此內容（預設模式）。

* 的 `nosamplecontent` 模式將不安裝示例內容。

無標準運行模式是為生產安裝而設計的。

## 定義運行模式的配置屬性 {#defining-configuration-properties-for-a-run-mode}

配置屬性的值集合（用於特定運行模式）可以保存在儲存庫中。

運行模式由資料夾名稱上的尾碼指示。 這允許您將所有配置儲存在一個儲存庫中。 例如：

* `config`

   適用於所有運行模式

* `config.author`

   用於作者運行模式

* `config.publish`

   用於發佈運行模式

* `config.<run-mode>`

   用於適用的運行模式；例如，config

請參閱 [儲存庫中的OSGi配置](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) 有關定義這些資料夾中的單個配置節點以及建立多個運行模式組合的配置的詳細資訊。

>[!NOTE]
>
>對於 [安裝運行模式](#installation-run-modes) （例如作者）安裝後無法更改運行模式。 但是，對單個配置屬性的更改將在重新啟動後生效。

## 定義要為運行模式安裝的附加捆綁包 {#defining-additional-bundles-to-be-installed-for-a-run-mode}

還可以指定應為特定運行模式安裝的其他捆綁包。 對於這些定義，安裝資料夾用於保存捆綁包。 運行模式再次由前置詞指示：

* `install.author`
* `install.publish`

這些資料夾的類型 `nt:folder` 應包含相應的捆綁包。

## 使用特定運行模式啟動CQ {#starting-cq-with-a-specific-run-mode}

如果已為多個運行模式定義了配置，則需要定義啟動時要使用的配置。 指定使用哪種運行模式有幾種方法；決議的順序是：

1. [系統屬性(](#using-a-system-property-in-the-start-script)
1. [ ](#using-the-sling-properties-file)
1. [ ](#using-the-r-option)
1. [檔案名檢測](#filename-detection-renaming-the-jar-file)

使用應用程式伺服器時，您還可以 [在web.xml中定義運行模式](#defining-the-run-mode-in-web-xml-with-application-server)。

### 使用sling.properties檔案 {#using-the-sling-properties-file}

的 `sling.properties` 檔案可用於定義所需的運行模式：

1. 編輯配置檔案：

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. 添加以下屬性；以下示例適用於作者：

   `sling.run.modes=author`

### 使用 — r選項 {#using-the-r-option}

可以使用 `-r` 頁籤 例如，使用以下命令啟動AEM運行模式設定為dev的實例。&quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### 在啟動指令碼中使用系統屬性 {#using-a-system-property-in-the-start-script}

啟動指令碼中的系統屬性可用於指定運行模式。

* 例如，使用以下方法將實例作為位於美國的生產發佈實例啟動：

   `-Dsling.run.modes=publish,prod,us`

### 檔案名檢測 — 更名jar檔案 {#filename-detection-renaming-the-jar-file}

通過在安裝前更名安裝jar檔案，可以激活以下兩種安裝運行模式：

* 發佈
* 作者

jar檔案必須使用命名約定：

`cq5-<run-mode>-p<port-number>`

例如，設定 `publish` 通過命名jar檔案運行模式：

`cq5-publish-p4503`

### 在web.xml中定義運行模式（使用Application Server） {#defining-the-run-mode-in-web-xml-with-application-server}

使用應用程式伺服器時，您還可以配置屬性：

`sling.run.modes`

檔案：

`WEB-INF/web.xml`

在AEM `war` 檔案，在部署之前應更新。

請參閱 [使用應AEM用程式伺服器安裝](/help/sites-deploying/application-server-install.md) 的上界。
