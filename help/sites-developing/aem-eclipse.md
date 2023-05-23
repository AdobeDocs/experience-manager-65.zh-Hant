---
title: Eclipse 適用的 AEM 開發人員工具
seo-title: AEM Developer Tools for Eclipse
description: Eclipse 適用的 AEM 開發人員工具
seo-description: null
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
exl-id: 00473769-c447-4966-a71e-117c669e0151
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 4%

---

# Eclipse 適用的 AEM 開發人員工具{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## 概觀 {#overview}

「開AEM發人員工具」是基於 [Apache Sling的Eclipse插件](https://sling.apache.org/documentation/development/ide-tooling.html) 已在Apache許可證2下發佈。

它提供了幾種使開發更AEM容易的功能：

* 通過Eclipse Server ConnectorAEM與實例無縫整合。
* 內容和OSGI捆綁包的同步。
* 使用代碼熱交換功能調試支援。
* 通過特AEM定項目建立嚮導簡單Bootstrap項目。
* 易於編輯JCR屬性。

## 要求 {#requirements}

使用「開發AEM人員工具」之前，請執行以下操作：

* 下載並安裝 [Eclipse IDE for Java™ EE開發人員](https://www.eclipse.org/downloads/packages/release/luna/r/eclipse-ide-java-ee-developers)。 開發AEM人員工具當前支援EclipseKepler或更新

* 可與5.6.1版或更AEM高版本一起使用
* 配置eclipse安裝，通過編輯 `eclipse.ini` 配置檔案（如所述） [Eclipse常見問題](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F)。

>[!NOTE]
>
>在macOS，按一下右鍵 **Eclipse.app**，然後選擇 **顯示包內容** 查找 `eclipse.ini`。

## 如何安裝EclipseAEM開發人員工具 {#how-to-install-the-aem-developer-tools-for-eclipse}

一旦你完成了 [要求](#requirements) 在上面，可以按如下方式安裝插件：

1. 瀏覽 **開發AEM人員工具** 網站 `https://eclipse.adobe.com/aem/dev-tools/`。

1. 複製 **安裝連結**。

   或者，您可以下載存檔檔案，而不是使用安裝連結。 這樣允許離線安裝，但您會錯過自動更新通知。

1. 在Eclipse中，開啟 **幫助** 的子菜單。
1. 按一下 **安裝新軟體**。
1. 按一下 **添加……**。
1. 在 **名稱** 鍵AEM入Developer Tools。
1. 在 **位置** 複製安裝URL。
1. 按一下 **確定**。
1. 同時檢查 **AEM** 和 **吊帶** 插件。
1. 按一下&#x200B;**下一步**。
1. 按一下&#x200B;**下一步**。
1. 接受臨時協定，然後按一下 **完成**。
1. 按一下 **是** 來重新啟動Eclipse。

## 如何導入現有項目 {#how-to-import-existing-projects}

>[!NOTE]
>
>請參閱 [如何在Eclipse中下載捆綁包時使用它AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407)。

## 透AEM視 {#the-aem-perspective}

EclipseAEM開發工具附帶一個透視，讓您能夠完全控制項AEM目和實例。

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## 示例多模組項目 {#sample-multi-module-project}

「開AEM發人員工具」包括一個示例、多模組項目，可幫助您快速完成Eclipse中的項目設定。 它還可作為幾種功能的最佳實踐指AEM南。 [瞭解有關項目原型的詳細資訊](https://github.com/adobe/aem-project-archetype)。

要建立示例項目，請完成以下步驟：

1. 在 **檔案** > **新建** > **項目** 菜單，瀏覽至 **AEM** 選擇 **多模AEM塊項目示例**。

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 按一下&#x200B;**下一步**。

   >[!NOTE]
   >
   >此步驟可能需要一段時間，因為m2eclipse必須掃描原型目錄。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. 選擇 **com.adobe.granite.archetypes:示例 — 項目 — 原型：（最高數）** ，然後按一下 **下一個**。

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. 填寫 **名稱**。 **組ID**&#x200B;的 **項目ID** 的下界。 您也可以選擇設定一些高級屬性。

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. 現在，配置AEMEclipse可以連接到的伺服器。

   要使用調試器功能，請確AEM保已在調試模式下啟動，這可以通過向命令行添加以下內容來實現：

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. 按一下 **完成**。 將建立項目結構。

   >[!NOTE]
   >
   >在新安裝(更具體地說：從未下載過多個依賴項時)，您可能會建立項目並出現錯誤。 在本例中，請按照中描述的過程操作 [解析無效的項目定義](#resolving-invalid-project-definition)。

## 疑難排解 {#troubleshooting}

### 解析無效的項目定義 {#resolving-invalid-project-definition}

要解決無效的依賴項和項目定義，請按如下步驟進行：

1. 選擇所有已建立的項目。
1. 按一下右鍵。 在菜單中 **馬文**&#x200B;選中 **更新項目**。
1. 檢查 **強制更新快照/版本**。
1. 按一下&#x200B;**「確定」**。Eclipse嘗試下載所需的依賴項。

### 在JSP檔案中啟用標籤庫自動完成 {#enabling-tag-library-autocompletion-in-jsp-files}

標籤庫自動完成功能在項目中添加了適當的依賴關係後即可完成。 使用Uber Jar時有一個已知問題AEM，該問題不包括所需的tld和TagExtraInfo檔案。

要解決此問題，請確保org.apache.sling.scripting.jsp.taglib項目位於AEMUber Jar之前的類路徑中。 對於Maven項目，將以下依賴項放在pom.xml中，然後放在Uber Jar之前。

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

確保為部署添加正確的版本AEM。

## 詳細資訊 {#more-information}

用於Eclipse網站的Apache Sling IDE工具正式為您提供了有用的資訊：

* 的 [**用於Eclipse的Apache Sling IDE工具** 使用手冊](https://sling.apache.org/documentation/development/ide-tooling.html)，本文檔將指導您瞭解開發工具支援的總體概念、伺服器整合和部AEM署功能。
* 的 [「疑難解答」部分](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)。
* 的 [已知問題清單](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)。

以下官員 [日蝕](https://www.eclipse.org/) 文檔可幫助設定環境：

* [Eclipse入門](https://www.eclipse.org/getting-started/)
* [Eclipse Luna幫助系統](https://help.eclipse.org/latest/index.jsp)
* [Maven整合(m2eclipse)](https://www.eclipse.org/m2e/)
