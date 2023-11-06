---
title: 如何在AEM 6.5 Forms上啟用最適化Forms核心元件？
description: 逐步指南可協助您在AEM 6.5 Forms環境中啟用最適化Forms核心元件。
keywords: 啟用核心元件、核心元件調適型Forms、6.5上的核心元件、AEM 6.5上的調適型Forms核心元件、AEM 6.5上的AF核心元件、AEM 6.5 Forms核心元件
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
exl-id: 6585ea71-6242-47d3-bc59-6f603cf507b6
source-git-commit: 1da3abac8a7f09d41127818a5abacf29524f1365
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 18%

---

# 在AEM 6.5 Forms上啟用最適化Forms核心元件 {#enable-adaptive-forms-core-components}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html) |
| AEM 6.5 | 本文 |

**套用至：** ✅立最適化表單核心元件❎最適化表單基礎元件。

啟用最適化Forms核心元件可讓您開始建立、發佈和傳遞 [Core Components based Adaptive Forms](create-an-adaptive-form-core-components.md) 和 [Headless最適化Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 從您的AEM 6.5 Forms環境。

若要在您的AEM 6.5 Forms環境中啟用最適化Forms核心元件，請設定並部署 [AEM Archetype 41或更新版本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 根據您所有作者和發佈執行個體上的專案（已啟用表單選項）。

本文提供在您的AEM 6.5 Forms環境中設定和部署AEM Archetype 41或更新版本專案，以啟用最適化Forms核心元件的詳細指示。 您可以參閱下列清單，以瞭解 **AEM 6.5** 啟用Forms核心元件的相容版本：

## 先決條件 {#prerequisites}

在AEM 6.5 Forms環境中啟用最適化Forms核心元件之前：

* [升級至AEM 6.5 Forms Service Pack 16 (6.5.16.0)或更新版本](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html).

* 安裝最新版本的 [Apache Maven](https://maven.apache.org/download.cgi).

* 安裝純文字編輯器。 例如，Microsoft Visual Studio Code。

## 建立及部署最新的AEM原型專案

若要建立AEM Archetype 41或 [稍後](https://github.com/adobe/aem-project-archetype) 根據專案並將其部署至所有作者和發佈執行個體：

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

   * 請勿變更的值 `aemVersion` 屬性來源 `6.5.15.0` 至任何其他專案。

   * 設定 `archetypeVersion` 屬性至 `41` 或更新版本。 如需最新版本的相關資訊，請參閱以下章節的系統需求一節： [AEM專案原型](https://github.com/adobe/aem-project-archetype) 檔案。

   * 更新命令以反映環境的特定值，包括 `appTitle`， `appId`、和 `groupId`. 此外，設定  `includeFormsenrollment` 屬性至 `y`. 如果您使用Forms入口網站，請設定 `includeExamples=y` 可在您的專案中包含Forms Portal核心元件的選項。


1. （僅適用於以Archetype版本41為基礎的專案）在AEM Archetype專案建立後，請為以核心元件為基礎的最適化Forms啟用主題。 若要啟用主題：

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
   1. 設定版本 `core.forms.components.version` 和 `core.forms.components.af.version` 至 [最新Forms核心元件](https://github.com/adobe/aem-core-forms-components/tree/release/650#system-requirements) 版本，並確認兩者版本相同 **Forms核心元件** 在表格中提及，並設定版本 `core.wcm.components.version` 如中所述 **WCM核心元件**.

      >[!WARNING]
      >
      >* 使用建立原型專案時 `version 45`，則 [AEM原型專案資料夾]/pom.xml一開始將forms核心元件版本設定為 `1.1.28`. 在建立或部署Archetype專案之前，請將Forms核心元件版本更新為 `1.1.26`.


      >[!NOTE]
      >
      >* 如果您設定任何其他拓撲，請確定您將提交、預填和其他URL新增到Dispatcher層的允許清單。

   1. 儲存並關閉檔案。


1. 成功建立AEM原型專案後，為您的環境建置部署套件。 若要建置套件：

   1. 導覽至AEM Archetype專案的根目錄。

   1. 執行以下命令，為您的環境建置AEM原型專案：

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   成功建置AEM Archetype專案後，會產生AEM套件。 您可以在下列位置找到此套件： [AEM原型專案資料夾]\all\target\[appid].all-[版本].zip

1. 使用 [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hant) 以部署 [AEM原型專案資料夾]\all\target\[appid].all-[版本].zip套件。

>[!NOTE]
>
>
>
> * 如果您在存取發佈執行個體的登入對話方塊時遇到困難，若要透過封裝管理員安裝套件，請嘗試使用URL： `http://[Publish Server URL]:[PORT]/system/console` 以登入。 這可讓您存取發佈執行個體的登入頁面，讓您繼續安裝程式。
> * 將原型專案部署到您的環境後，請勿刪除或捨棄該專案。 Archetype專案需要將自訂和新的最適化Forms核心元件主題新增到您的環境。

核心元件已針對您的環境啟用。 將空白的Core Components型最適化表單範本和畫布3.0主題部署到您的環境，讓您能夠 [建立以核心元件為基礎的最適化Forms](create-an-adaptive-form-core-components.md).

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

* [建立以核心元件為基礎的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)
* [建立最適化表單或新增最適化表單至AEM Sites頁面或體驗片段](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [建立核心元件型最適化Forms的主題](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [建立核心元件型最適化Forms的範本](template-editor.md)
