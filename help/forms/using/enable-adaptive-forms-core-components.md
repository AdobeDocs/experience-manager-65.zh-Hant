---
title: 如何在AEM 6.5 Forms上啟用最適化Forms核心元件？
description: 逐步指南可協助您在AEM 6.5 Forms環境中啟用最適化Forms核心元件。
keywords: 啟用核心元件、核心元件調適Forms、6.5上的核心元件、AEM 6.5上的調適Forms核心元件、AEM 6.5上的AF核心元件、AEM 6.5 Forms核心元件
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms,Core Components
exl-id: 6585ea71-6242-47d3-bc59-6f603cf507b6
solution: Experience Manager, Experience Manager Forms
source-git-commit: c75cd7a0cbd0c19fd10cc7512bbfa14fae1e4f92
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 10%

---

# 在AEM 6.5 Forms上啟用最適化Forms核心元件 {#enable-adaptive-forms-core-components}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html?lang=zh-Hant) |
| AEM 6.5 | 本文 |

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

啟用最適化Forms核心元件可讓您從AEM 6.5 Forms環境開始建立、發佈及傳遞[以核心元件為基礎的最適化Forms](create-an-adaptive-form-core-components.md)和[無頭式最適化Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=zh-Hant)。

若要在您的AEM 6.5 Forms環境中啟用最適化Forms核心元件，請在您的所有製作和發佈執行個體上設定並部署[AEM Archetype 41或更新版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)型專案（啟用表單選項）。

本文提供在您的AEM 6.5 Forms環境中設定和部署AEM Archetype 41或更新版本專案，以啟用最適化Forms核心元件的詳細指示。 您可以參閱下列清單，以取得啟用Forms核心元件的&#x200B;**AEM 6.5**&#x200B;相容版本：

## 先決條件 {#prerequisites}

在AEM 6.5 Forms環境中啟用最適化Forms核心元件之前：

* [升級至AEM 6.5 Forms Service Pack 16 (6.5.16.0)或更新版本](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=zh-Hant)。

* 安裝最新版的[Apache Maven](https://maven.apache.org/download.cgi)。

* 安裝純文字編輯器。 例如，Microsoft Visual Studio Code。

## 建立及部署最新的AEM原型專案

若要建立以AEM Archetype 41或[稍後](https://github.com/adobe/aem-project-archetype)為基礎的專案，並將其部署至您的所有作者與發佈執行個體：

1. 以管理員身分登入電腦，託管並執行AEM 6.5 Forms執行個體。
1. 開啟命令提示字元或終端機，然後執行下列命令以建立AEM Archetype專案（並啟用表單選項）：

   * Microsoft Windows

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate ^
      -D archetypeGroupId=com.adobe.aem ^
      -D archetypeArtifactId=aem-project-archetype ^
      -D archetypeVersion=41 ^
      -D appTitle="My Form" ^
      -D appId="myform" ^
      -D groupId="com.myform" ^
      -D includeFormsenrollment="y" ^
      -D aemVersion="6.5.23" 
   ```

   * Linux或Apple macOS

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
      -D archetypeGroupId=com.adobe.aem \
      -D archetypeArtifactId=aem-project-archetype \
      -D archetypeVersion=41 \
      -D appTitle="My Form" \
      -D appId="myform" \
      -D groupId="com.myform" \
      -D includeFormsenrollment="y" \
      -D aemVersion="6.5.23" 
   ```

   執行上述命令時，請務必考慮以下幾點：

   * 將`archetypeVersion`屬性設定為`41`或更新版本。 如需最新版本，請參閱[AEM專案原型](https://github.com/adobe/aem-project-archetype)檔案中的系統需求一節。

   * 更新命令以反映您環境的特定值，包括`appTitle`、`appId`和`groupId`。 另外，將`includeFormsenrollment`屬性的值設定為`y`。 如果您使用Forms入口網站，請設定`includeExamples=y`選項以在您的專案中包含Forms入口網站核心元件。


1. （僅適用於以Archetype版本41為基礎的專案）在AEM Archetype專案建立後，請啟用以核心元件為基礎的最適化Forms的主題。 若要啟用主題：

   1. 開啟[AEM原型專案資料夾]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html以進行編輯：

   1. 在第21行新增下列程式碼：

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![在第21](/help/forms/using/assets/code-to-enable-themes.png)行新增上述程式碼

   1. 儲存並關閉檔案。

1. 更新專案以包含最新版Forms核心元件：

   1. 開啟[AEM原型專案資料夾]/pom.xml以進行編輯。
   1. 將`core.forms.components.version`和`core.forms.components.af.version`的版本設定為[最新的Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html?lang=zh-Hant#aem-as-form-version-history)版本，並確認兩者版本與表格中提及的&#x200B;**Forms核心元件**&#x200B;相同，並設定`core.wcm.components.version`的版本，如[WCM核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/versions.html?lang=zh-Hant)所指定。

      >[!WARNING]
      >
      >* 使用版本45建立Archetype專案時，`[AEM Archetype Project Folder]/pom.xml`一開始會將forms核心元件版本設定為1.1.28。在建立或部署Archetype專案之前，請將Forms核心元件版本更新為1.1.26。您可以在[AEM 6.5 Forms版本記錄](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html?lang=zh-Hant#aem-as-form-version-history)中找到最新版本。

      >[!NOTE]
      >
      >* 如果您設定其他任何拓撲，請確定您將提交、預填和其他URL新增到Dispatcher層的允許清單。

   1. 儲存並關閉檔案。


1. 成功建立AEM原型專案後，為您的環境建置部署套件。 若要建置套件：

   1. 導覽至AEM Archetype專案的根目錄。

   1. 執行以下命令，為您的環境建置AEM原型專案：

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   成功建立AEM原型專案後，就會產生AEM套件。 您可以在[AEM原型專案資料夾]\all\target\[appid].all-[version].zip中找到該套件

1. 使用[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant)，在所有製作和發佈執行個體上部署[AEM Archetype專案資料夾]\all\target\[appid].all-[version].zip封裝。

>[!NOTE]
>
>
>
> * 如果您在存取發佈執行個體的登入對話方塊時遇到困難，若要透過封裝管理員安裝封裝，請嘗試使用URL： `http://[Publish Server URL]:[PORT]/system/console`登入。 這可讓您存取發佈執行個體的登入頁面，讓您繼續安裝程式。
> * 將原型專案部署到您的環境後，請勿刪除或捨棄該專案。 Archetype專案需要將自訂和新的最適化Forms核心元件主題新增到您的環境。

核心元件已針對您的環境啟用。 將空白的Core Components based Adaptive Form範本和Canvas 3.0主題部署到您的環境，讓您能夠[建立Core Components based Adaptive Forms](create-an-adaptive-form-core-components.md)。

## 常見問答

### 核心元件有哪些？

[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 是一組適用於 AEM 的標準化網站內容管理 (WCM) 元件，可加快開發時間並降低網站的維護成本。

### 啟用核心元件時新增了哪些功能？


當為您的環境啟用調適型表單核心元件時，一個以核心元件為主的調適型表單空白範本和 Canvas 3.0 主題會新增至您的環境中。為您的環境啟用調適型表單核心元件後，您可以：

* 建立以最適化Forms為基礎的核心元件。
* 建立以核心元件為基礎的最適化表單範本。
* 建立核心元件型最適化表單範本的自訂主題。
* 為行動、網路、原生應用程式等需要表單Headless呈現的管道和服務提供核心元件型最適化表單的JSON呈現。

## 後續步驟

* [建立以核心元件為基礎的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)
* [建立最適化表單或新增最適化表單至AEM Sites頁面或體驗片段](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [建立核心元件型最適化Forms的主題](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [建立核心元件型最適化Forms的範本](template-editor.md)
