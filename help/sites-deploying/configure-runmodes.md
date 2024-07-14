---
title: 執行模式
description: 瞭解如何使用執行模式根據特定目的調整AEM執行個體。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Administering
exl-id: 6d03cb1d-500e-4a23-80e5-347a43dff30e
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 1%

---

# 執行模式{#run-modes}

執行模式可讓您針對特定目的調整AEM執行個體；例如，製作或發佈、測試、開發、內部網路或其他。

您可以：

* [定義每個執行模式的組態引數集合](#defining-configuration-properties-for-a-run-mode)。

  所有執行模式都會套用一組基本組態引數，然後您就可以根據特定環境的目的調整其他組。 這些會視需要套用。

* [定義要針對特定模式安裝的其他組合](#defining-additional-bundles-to-be-installed-for-a-run-mode)。

所有設定和定義都儲存在單一存放庫中，並透過設定&#x200B;**執行模式**&#x200B;來啟動。

## 安裝執行模式 {#installation-run-modes}

安裝（或固定）執行模式在安裝時使用，然後在執行個體的整個存留期內固定，因此無法變更。

提供立即可用的安裝執行模式：

* `author`
* `publish`
* `samplecontent`
* `nosamplecontent`

這兩組執行模式互斥；例如，您可以：

* 定義`author`或`publish`，而不是同時定義

* 將`author`與`samplecontent`或`nosamplecontent`結合（但不能兩者皆結合）

>[!CAUTION]
>
>使用上述執行模式之一(author、publish、samplecontent、nosamplecontent)時，安裝時使用的值會定義該安裝的&#x200B;*整個存留期*&#x200B;的執行模式。
>
>對於這些執行模式，您&#x200B;*無法在安裝後*&#x200B;變更它們。

## 自訂的執行模式 {#customized-run-modes}

您也可以建立自己的自訂執行模式。 這些可結合以涵蓋下列案例：

* `author` + `development`

* `publish` + `test`

* `publish` + `test` + `golive`

* `publish` + `intranet`

* 視需要。.

每次啟動時也可以選取自訂的執行模式。

## 使用samplecontent和nosamplecontent {#using-samplecontent-and-nosamplecontent}

這些模式可讓您控制範例內容的使用。 範例內容是在建置快速入門之前定義，可包含套件、設定等：

* `samplecontent`執行模式會安裝此內容（預設模式）。

* `nosamplecontent`模式未安裝範例內容。

nosamplecontent執行模式是針對生產安裝所設計。

## 定義執行模式的設定屬性 {#defining-configuration-properties-for-a-run-mode}

組態屬性的值集合（用於特定執行模式）可儲存在存放庫中。

資料夾名稱上的尾碼表示執行模式。 這可讓您將所有設定作為儲存在單一存放庫中。 例如：

* `config`

  適用於所有執行模式

* `config.author`

  用於作者執行模式

* `config.publish`

  用於發佈執行模式

* `config.<run-mode>`

  用於適用的執行模式；例如，設定

請參閱存放庫中的[OSGi設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)，以取得有關定義這些資料夾中的個別設定節點，以及建立多個執行模式組合之設定的更多詳細資料。

>[!NOTE]
>
>對於[安裝執行模式](#installation-run-modes) （例如，作者），安裝後無法變更執行模式。 但是，個別組態屬性的變更將在重新啟動後生效。

## 定義要針對執行模式安裝的其他組合 {#defining-additional-bundles-to-be-installed-for-a-run-mode}

也可以指定應該針對特定執行模式安裝的其他組合。 對於這些定義，會使用安裝資料夾來儲存組合。 執行模式再次由前置字元表示：

* `install.author`
* `install.publish`

這些資料夾的型別為`nt:folder`，應該包含適當的組合。

## 以特定執行模式啟動CQ {#starting-cq-with-a-specific-run-mode}

如果您已經為多個執行模式定義了配置，則需要定義要在啟動時使用的配置。 有數種方法可指定要使用的執行模式；解析的順序為：

1. [系統屬性(](#using-a-system-property-in-the-start-script)
1. [](#using-the-sling-properties-file)
1. [](#using-the-r-option)
1. [檔案名稱偵測](#filename-detection-renaming-the-jar-file)

當您使用應用程式伺服器時，您也可以[在web.xml](#defining-the-run-mode-in-web-xml-with-application-server)中定義執行模式。

### 使用sling.properties檔案 {#using-the-sling-properties-file}

`sling.properties`檔案可用來定義必要的執行模式：

1. 編輯組態檔：

   `<cq-installation-dir>/crx-quickstart/conf/sling.properties`

1. 新增下列屬性；以下範例適用於作者：

   `sling.run.modes=author`

### 使用 — r選項 {#using-the-r-option}

啟動快速入門時，可使用`-r`選項啟動自訂執行模式。 例如，使用以下命令來啟動執行模式設為dev的AEM執行個體。&quot;

```shell
java -jar cq-56-p4545.jar -r dev
```

### 在啟動指令碼中使用系統屬性 {#using-a-system-property-in-the-start-script}

啟動指令碼中的系統屬性可用來指定執行模式。

* 例如，使用以下專案將執行個體啟動為美國的生產發佈執行個體：

  `-Dsling.run.modes=publish,prod,us`

### 檔案名稱偵測 — 重新命名jar檔案 {#filename-detection-renaming-the-jar-file}

在安裝之前，透過重新命名安裝jar檔案，可以啟用以下兩種安裝執行模式：

* 發佈
* 作者

jar檔案必須使用命名慣例：

`cq5-<run-mode>-p<port-number>`

例如，透過命名jar檔案來設定`publish`執行模式：

`cq5-publish-p4503`

### 在web.xml中定義執行模式（使用應用程式伺服器） {#defining-the-run-mode-in-web-xml-with-application-server}

當您使用應用程式伺服器時，也可以設定屬性：

`sling.run.modes`

在檔案中：

`WEB-INF/web.xml`

此檔案位於AEM `war`檔案中，應在部署前更新。

如需詳細資訊，請參閱[使用應用程式伺服器安裝AEM](/help/sites-deploying/application-server-install.md)。
