---
title: 如何利用EclipseAEM開發項目
seo-title: How to Develop AEM Projects Using Eclipse
description: 本指南介紹如何使用Eclipse開發基AEM於的項目
seo-description: This guide describes how to use Eclipse for developing AEM based projects
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
exl-id: 9d421599-0417-4329-a528-9cda4e3716f5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# 如何利用EclipseAEM開發項目{#how-to-develop-aem-projects-using-eclipse}

本指南介紹如何使用Eclipse開發基AEM於的項目。

>[!NOTE]
>
>Adobe現在提供 [EclipseAEM開發工具](/help/sites-developing/aem-eclipse.md) 幫助您開發AEMEclipse解決方案。

## 概觀 {#overview}

要開始在AEMEclipse上開發，需要以下步驟。

在本How-To的其餘部分中，對每個How-To進行了更詳細的說明。

* 安裝Eclipse 4.3(Kepler)
* 基於Maven設AEM置項目
* 在Maven POM中為Eclipse準備JSP支援
* 將Maven項目導入Eclipse

>[!NOTE]
>
>本指南基於Eclipse 4.3(Kepler)和AEM5.6.1。

## 安裝Eclipse {#install-eclipse}

從 [Eclipse下載頁](https://www.eclipse.org/downloads/)。

在 [安裝說明](https://wiki.eclipse.org/Eclipse/Installation)。

## 基於Maven設AEM置項目 {#set-up-your-aem-project-based-on-maven}

接下來，使用Maven設定項目，如中所述 [使用Apache Maven構建AEM項目的方法](/help/sites-developing/ht-projects-maven.md)。

## 為Eclipse準備JSP支援 {#prepare-jsp-support-for-eclipse}

Eclipse還可以在使用JSP時提供支援，例如

* 自動完成標籤庫
* 由定義的對象的Eclipse感知 &lt;cq:defineobjects /> 和 &lt;sling:defineobjects />

為了讓這一點奏效：

1. 按照 [如何使用JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) 在 [使用Apache Maven構建AEM項目的方法](/help/sites-developing/ht-projects-maven.md)。
1. 將以下內容添加到 &lt;build /> 的子菜單。

   Eclipse的Maven支援插件m2e不支援maven-jspc插件，此配置指示m2e忽略插件和清理臨時編譯結果的相關任務。

   這不是問題：如所述 [如何使用JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)，此設定中的maven-jspc-plugin僅用於驗證JSP是否作為生成過程的一部分進行編譯。 Eclipse已報告JSP中的任何問題，並且不依賴此Maven插件來執行。

   **myproject/content/pom.xml**

   ```xml
   <build>
     <!-- ... -->
     <pluginManagement>
       <plugins>
         <!--This plugin's configuration is used to store Eclipse m2e settings only. It has no influence on the Maven build itself.-->
         <plugin>
           <groupId>org.eclipse.m2e</groupId>
           <artifactId>lifecycle-mapping</artifactId>
           <version>1.0.0</version>
           <configuration>
             <lifecycleMappingMetadata>
               <pluginExecutions>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.sling</groupId>
                     <artifactId>maven-jspc-plugin</artifactId>
                     <versionRange>[2.0.6,)</versionRange>
                     <goals>
                       <goal>jspc</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.maven.plugins</groupId>
                     <artifactId>maven-clean-plugin</artifactId>
                     <versionRange>[2.4.1,)</versionRange>
                     <goals>
                       <goal>clean</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
               </pluginExecutions>
             </lifecycleMappingMetadata>
           </configuration>
         </plugin>
       </plugins>
     </pluginManagement>
   </build>
   ```

### 將Maven項目導入Eclipse {#import-the-maven-project-into-eclipse}

1. 在Eclipse中，選擇「檔案」>「導入……」
1. 在「導入」對話框中，選擇「Maven」>「現有Maven項目」，然後按一下「下一步」。

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. 輸入項目頂級資料夾的路徑，然後按一下「全選」和「完成」。

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 現在，您已準備好使用Eclipse開發項目，AEM包括JSP自動完成。

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >如果包括 `/libs/foundation/global.jsp` 或其他JSP `/libs`，您需要將其複製到您的項目中，以便Eclipse能夠解決包含問題。 同時，您需要確保Maven未將其捆綁到您的內容包中。 如中所述，如何實現此目標 [如何使用Apache AEM Maven生成項目](/help/sites-developing/ht-projects-maven.md)。
