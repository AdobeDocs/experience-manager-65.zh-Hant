---
title: 如何在AEM 6.5 Forms上啟用最適化Forms核心元件？
seo-title: How to enable Adaptive Forms Core Components on AEM 6.5 Forms?
description: 逐步指南可協助您在AEM 6.5 Forms環境中啟用最適化Forms核心元件。
seo-description: Step-by-Step guide to help you enable Adaptive Forms Core Components on an AEM 6.5 Forms environment.
keywords: 啟用核心元件、核心元件Adaptive Forms、6.5版上的核心元件、AEM 6.5版上的最適化Forms核心元件、AEM 6.5版上的AF核心元件、AEM 6.5 Forms核心元件
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: 85f423b98ff680d7ed7cdbdde65e2dec1cfe4c03
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 19%

---


# 在AEM 6.5 Forms上啟用最適化Forms核心元件 {#enable-adaptive-forms-core-components}

啟用Adaptive Forms核心元件，讓您開始建立、發佈和傳送內容 [Core Components based Adaptive Forms](create-an-adaptive-form-core-components.md) 和 [Headless最適化Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 來自您的AEM 6.5 Forms環境。

若要在您的AEM 6.5 Forms環境中啟用HAdaptive Forms核心元件，請設定並部署 [AEM Archetype 41或更新版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 根據您所有的Author和Publish執行個體上的專案（已啟用表單選項）。

本文提供在AEM 6.5 Forms環境上設定和部署以AEM Archetype 41或更新版本為基礎的專案的詳細指示，以啟用Adaptive Forms核心元件。


## 必備條件 {#prerequisites}

在AEM 6.5 Forms環境中啟用Adaptive Forms核心元件之前：

* [升級至AEM 6.5 Forms Service Pack 16 (6.5.16.0)或更新版本](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html).

* 安裝最新版本的 [Apache Maven](https://maven.apache.org/download.cgi).

* 安裝純文字編輯器。 例如，Microsoft Visual Studio Code。

## 建立及部署最新的AEM原型專案

若要建立AEM Archetype 41或 [稍後](https://github.com/adobe/aem-project-archetype) 以專案為基礎，並將其部署至所有作者和發佈執行個體：

1. 以管理員身分登入您的電腦，託管並執行AEM 6.5 Forms執行個體。
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
      -D aemVersion="6.5.15" 
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
      -D aemVersion="6.5.15" 
   ```

   執行上述命令時，請務必考慮以下幾點：

   * 請勿變更 `aemVersion` 屬性來源 `6.5.15.0` 至任何其他專案。

   * 設定 `archetypeVersion` 屬性至 `41` 或更新版本。 如需最新版本，請參閱 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 說明檔案。

   * 更新命令以反映環境的特定值，包括 `appTitle`， `appId`、和 `groupId`. 此外，設定  `includeFormsenrollment` 屬性至 `y`. 如果您使用Forms入口網站，請將 `includeExamples=y` 可在您的專案中包含Forms入口網站核心元件的選項。


1. （僅適用於以Archetype版本41為基礎的專案）建立AEM Archetype專案後，請啟用以核心元件為基礎的最適化Forms的主題。 若要啟用主題：

   1. 開啟 [AEM原型專案資料夾]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html進行編輯：

   1. 在第21行新增下列程式碼：

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![在第21行新增上述程式碼](/help/forms/using/assets/code-to-enable-themes.png)

   1. 儲存並關閉檔案。

1. 更新專案以包含最新版Forms核心元件：

   1. 開啟 [AEM原型專案資料夾]/pom.xml進行編輯。
   1. 設定版本 `core.forms.components.version` 和 `core.forms.components.af.version` 至 [最新Forms核心元件](https://github.com/adobe/aem-core-forms-components/tree/release/650) 版本。

   1. 儲存並關閉檔案。


1. 成功建立AEM原型專案後，為您的環境建置部署套件。 若要建置套件：

   1. 導覽至AEM Archetype專案的根目錄。

   1. 執行以下命令，為您的環境建置AEM原型專案：

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   成功建置AEM Archetype專案後，會產生AEM套件。 您可以在下列位置找到套件： [AEM原型專案資料夾]\all\target\[appid].all-[版本].zip

1. 使用 [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant) 以部署 [AEM原型專案資料夾]\all\target\[appid].all-[版本].zip套件（在所有作者和發佈執行個體上）。

>[!NOTE]
>
>
>
> * 如果您在存取發佈執行個體上的登入對話方塊時遇到困難，若要透過封裝管理員安裝套件，請嘗試使用URL： `http://[Publish Server URL]:[PORT]/system/console` 以登入。 這可讓您存取發佈執行個體的登入頁面，讓您繼續安裝程式。
> * 將原型專案部署至您的環境後，請勿刪除或捨棄該專案。 Archetype專案需要將自訂和新的Adaptive Forms核心元件主題新增到您的環境中。

核心元件已針對您的環境啟用。 將空白的Core Components型最適化表單範本和Canvas 3.0主題部署至您的環境，讓您能夠 [建立以核心元件為基礎的最適化Forms](create-an-adaptive-form-core-components.md).

## 常見問答

### 核心元件有哪些？

[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 是一組適用於 AEM 的標準化網站內容管理 (WCM) 元件，可加快開發時間並降低網站的維護成本。

### 啟用核心元件時新增了哪些功能？


當為您的環境啟用調適型表單核心元件時，一個以核心元件為主的調適型表單空白範本和 Canvas 3.0 主題會新增至您的環境中。為您的環境啟用調適型表單核心元件後，您可以：

* 建立以核心元件為主的調適型表單。
* 建立以核心元件為主的調適型表單範本。
* 為以核心元件為主的調適型表單範本建立自訂主題。
* 將以核心元件為主的調適型表單的代表提供給一些管道，例如行動、網頁、本機應用程式和需要表單以 Headless 呈現的服務。。

## 下一步

* [建立以Core Components為基礎的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)
* [建立最適化表單或新增最適化表單至AEM Sites頁面或體驗片段](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [建立以核心元件為基礎的最適化Forms的主題](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [建立以核心元件為基礎的最適化Forms範本](template-editor.md)