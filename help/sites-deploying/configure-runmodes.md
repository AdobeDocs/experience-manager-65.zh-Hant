---
title: 執行模式
seo-title: 執行模式
description: 了解如何使用執行模式，針對特定用途調整您的AEM執行個體。
seo-description: 了解如何使用執行模式，針對特定用途調整您的AEM執行個體。
uuid: 8a0c6e5c-4fae-43e2-b745-eee58f346ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 12329e26-40bc-4c94-bc60-6d9cbd01345f
feature: 設定
exl-id: 6d03cb1d-500e-4a23-80e5-347a43dff30e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 1%

---

# 執行模式{#run-modes}

執行模式可讓您針對特定用途調整AEM執行個體；例如，製作或發佈、測試、開發、內部網路或其他。

您可以：

* [為每個執行模式定義設定參數的集合](#defining-configuration-properties-for-a-run-mode)。

   所有執行模式都會套用一組基本的設定參數，然後您就可以根據特定環境的用途調整其他設定。 視需要套用。

* [定義要針對特定模式安裝的其他套件組合](#defining-additional-bundles-to-be-installed-for-a-run-mode)。

所有設定和定義都儲存在一個儲存庫中，並通過設定&#x200B;**運行模式**&#x200B;來激活。

## 安裝運行模式{#installation-run-modes}

安裝（或固定）執行模式會在安裝時使用，然後在執行個體的整個存留期中加以修正，則無法變更。

安裝執行模式可立即使用：

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

這是兩對互斥的運行模式；例如，您可以：

* 同時定義`author`或`publish`，而非兩者

* 將`author`與`samplecontent`或`nosamplecontent`組合（但不同於兩者）

>[!CAUTION]
>
>使用上述任一執行模式時（製作、發佈、samplecontent、nosamplecontent），安裝時使用的值會定義該安裝的&#x200B;*整個存留期*&#x200B;的執行模式。
>
>對於這些運行模式，*不能*&#x200B;在安裝後更改它們。

## 自定義運行模式{#customized-run-modes}

您也可以建立自己的自訂執行模式。 可結合這些項目，以涵蓋下列情形：

* `author` + `development`

* `publish` +  `test`

* `publish` +  `test` +  `golive`

* `publish` +  `intranet`

* 視需要。..

每次啟動時也可以選擇自訂的執行模式。

## 使用samplecontent和nosamplecontent {#using-samplecontent-and-nosamplecontent}

這些模式可讓您控制範例內容的使用。 在構建快速入門之前定義了示例內容，其中可以包括包、配置等：

* `samplecontent`運行模式將安裝此內容（預設模式）。

* `nosamplecontent`模式將不安裝示例內容。

nosamplecontent執行模式是針對生產安裝而設計。

## 定義運行模式{#defining-configuration-properties-for-a-run-mode}的配置屬性

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

有關定義這些資料夾中的各個配置節點以及為組合多種運行模式建立配置的詳細資訊，請參閱儲存庫](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)中的[OSGi配置。

>[!NOTE]
>
>對於[安裝運行模式](#installation-run-modes)（例如作者），安裝後無法更改運行模式。 但是，對單個配置屬性的更改將在重新啟動後生效。

## 定義要為運行模式{#defining-additional-bundles-to-be-installed-for-a-run-mode}安裝的其他套件組合

還可以指定應為特定運行模式安裝的其他套件。 對於這些定義，安裝資料夾用於保存套件組合。 運行模式再次以前置詞表示：

* `install.author`
* `install.publish`

這些資料夾的類型為`nt:folder`，應包含適當的捆綁包。

## 以特定執行模式{#starting-cq-with-a-specific-run-mode}啟動CQ

如果您已為多個執行模式定義了配置，則需要定義啟動時要使用的配置。 有幾種方法可指定要使用的執行模式；決議的順序是：

1. [ ](#using-the-sling-properties-file)
1. [ ](#using-the-r-option)
1. [系統屬性(](#using-a-system-property-in-the-start-script)

1. [檔案名檢測](#filename-detection-renaming-the-jar-file)

使用應用程式伺服器時，您也可以[在web.xml](#defining-the-run-mode-in-web-xml-with-application-server)中定義運行模式。

### 使用sling.properties檔案{#using-the-sling-properties-file}

`sling.properties`檔案可用於定義所需的運行模式：

1. 編輯配置檔案：

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. 新增下列屬性；以下範例適用於author:

   `sling.run.modes=author`

### 使用 — r選項{#using-the-r-option}

啟動快速啟動時，可使用`-r`選項激活自定義運行模式。 例如，使用下列命令啟動將執行模式設為dev的AEM例項。&quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### 在啟動指令碼{#using-a-system-property-in-the-start-script}中使用系統屬性

啟動指令碼中的系統屬性可用於指定運行模式。

* 例如，使用下列工具將執行個體啟動為位於美國的生產發佈執行個體：

   `-Dsling.run.modes=publish,prod,us`

### 檔案名檢測 — 更名jar檔案{#filename-detection-renaming-the-jar-file}

在安裝之前，可通過更名安裝jar檔案來激活以下兩種安裝運行模式：

* 發佈
* 作者

jar檔案必須使用命名慣例：

`cq5-<run-mode>-p<port-number>`

例如，通過命名jar檔案來設定`publish`運行模式：

`cq5-publish-p4503`

### 在web.xml中定義運行模式（與應用程式伺服器一起）{#defining-the-run-mode-in-web-xml-with-application-server}

使用應用程式伺服器時，您也可以配置屬性：

`sling.run.modes`

檔案中：

`WEB-INF/web.xml`

此檔案位於AEM `war`檔案中，應在部署前更新。

如需詳細資訊，請參閱[使用應用程式伺服器安裝AEM](/help/sites-deploying/application-server-install.md) 。
