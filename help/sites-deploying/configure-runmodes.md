---
title: 執行模式
seo-title: 執行模式
description: 瞭解如何使用執行模式來針對特定用途調整AEM例項。
seo-description: 瞭解如何使用執行模式來針對特定用途調整AEM例項。
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 執行模式{#run-modes}

執行模式可讓您針對特定用途調整AEM實例；例如，作者或發佈、測試、開發、內部網路或其他人。

您可以：

* [定義每個運行模式的配置參數集合](#defining-configuration-properties-for-a-run-mode)。

   基本的配置參數集將應用於所有運行模式，然後您可以根據特定環境的目的調整其它配置參數集。 這些項目會視需要套用。

* [定義要針對特定模式安裝的附加捆綁包](#defining-additional-bundles-to-be-installed-for-a-run-mode)。

所有設定和定義都儲存在一個儲存庫中，並通過設定「運行模式」 **激活**。

## 安裝運行模式 {#installation-run-modes}

安裝（或固定）運行模式在安裝時使用，然後在實例的整個生命週期中固定，這些模式無法更改。

安裝運行模式是現成可用的：

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

這是兩對互斥的運行模式；例如，您可以：

* 同時定 `author` 義或 `publish`（而非同時定義兩者）

* 結合 `author` 使用 `samplecontent` 或 `nosamplecontent` （但不同於兩者）

>[!CAUTION]
>
>當使用上述任一執行模式（作者、發佈、samplecontent、nosamplecontent）時，安裝時使用的值會定義該安裝整個生命週期 *的執行* 模式。
>
>對於這些運行模式，在安 *裝後* ，您無法更改它們。

## 自訂執行模式 {#customized-run-modes}

您也可以建立您自己的自訂執行模式。 這些可結合在一起，以涵蓋下列情況：

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* 視需要。..

每次啟動時也可以選擇自訂的執行模式。

## 使用samplecontent和nosamplecontent {#using-samplecontent-and-nosamplecontent}

這些模式可讓您控制範例內容的使用。 樣例內容在快速啟動構建之前定義，可包括包、配置等：

* 運行 `samplecontent` 模式將安裝此內容（預設模式）。

* 此模 `nosamplecontent` 式將不安裝示例內容。

nosamplecontent執行模式是專為生產安裝而設計。

## 為運行模式定義配置屬性 {#defining-configuration-properties-for-a-run-mode}

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

有關在 [](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) 這些資料夾中定義單個配置節點以及為多種運行模式的組合建立配置的詳細資訊，請參閱儲存庫中的OSGi配置。

>[!NOTE]
>
>對 [於安裝運行模式](#installation-run-modes) （如作者），在安裝後不能更改運行模式。 但是，對單個配置屬性的更改將在重新啟動時生效。

## 定義要為運行模式安裝的附加捆綁 {#defining-additional-bundles-to-be-installed-for-a-run-mode}

還可以指定應為特定運行模式安裝的附加捆綁。 對於這些定義，安裝資料夾用於保存捆綁包。 再次，運行模式由前置詞指示：

* `install.author`
* `install.publish`

這些資料夾類型 `nt:folder` ，應包含適當的套件。

## 使用特定運行模式啟動CQ {#starting-cq-with-a-specific-run-mode}

如果您已為多種運行模式定義了配置，則需要定義啟動時要使用的配置。 指定要使用的運行模式有幾種方法；決議的順序是：

1. [ `sling.properties` 檔案](#using-the-sling-properties-file)
1. [ 選項 `-r`](#using-the-r-option)
1. [系統屬性(`-D`)](#using-a-system-property-in-the-start-script)

1. [檔案名稱偵測](#filename-detection-renaming-the-jar-file)

當您使用應用程式伺服器時，也可 [以在web.xml中定義執行模式](#defining-the-run-mode-in-web-xml-with-application-server)。

### 使用sling.properties檔案 {#using-the-sling-properties-file}

該 `sling.properties` 檔案可用於定義所需的運行模式：

1. 編輯配置檔案：

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. 添加以下屬性；以下範例是供作者使用：

   `sling.run.modes=author`

### 使用-r選項 {#using-the-r-option}

啟動快速啟動時，可使用選 `-r` 項激活自定義運行模式。 例如，使用下列命令啟動執行模式設為dev的AEM例項。&quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### 在啟動指令碼中使用系統屬性 {#using-a-system-property-in-the-start-script}

啟動指令碼中的系統屬性可用於指定運行模式。

* 例如，使用下列功能，將例項啟動為位於美國的生產發佈例項：

   `-Dsling.run.modes=publish,prod,us`

### 檔案名檢測——更名jar檔案 {#filename-detection-renaming-the-jar-file}

在安裝之前，可通過更名安裝jar檔案來激活以下兩種安裝運行模式：

* 發佈
* 作者

jar檔案必須使用命名約定：

`cq5-<run-mode>-p<port-number>`

例如，通過命名 `publish` jar檔案來設定運行模式：

`cq5-publish-p4503`

### 在web.xml中定義運行模式（使用Application Server） {#defining-the-run-mode-in-web-xml-with-application-server}

當您使用應用程式伺服器時，您也可以設定屬性：

`sling.run.modes`

在檔案中：

`WEB-INF/web.xml`

這是在AEM檔案中， `war` 在部署前應先進行更新。

如需詳 [細資訊，請參閱「將AEM與應用程式伺服器一起安裝](/help/sites-deploying/application-server-install.md) 」。
