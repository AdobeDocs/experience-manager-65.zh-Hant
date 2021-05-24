---
title: 如何使用Eclipse開發AEM專案
seo-title: 如何使用Eclipse開發AEM專案
description: 本指南說明如何使用Eclipse來開發AEM型專案
seo-description: 本指南說明如何使用Eclipse來開發AEM型專案
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
exl-id: 9d421599-0417-4329-a528-9cda4e3716f5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# 如何使用Eclipse{#how-to-develop-aem-projects-using-eclipse}開發AEM專案

本指南說明如何使用Eclipse來開發AEM型專案。

>[!NOTE]
>
>Adobe現在提供適用於Eclipse的[AEM開發工具](/help/sites-developing/aem-eclipse.md)，可協助您使用Eclipse開發AEM解決方案。

## 概覽 {#overview}

若要開始使用AEM on Eclipse開發，需執行下列步驟。

在本操作說明的其餘部分中，將更詳細地說明每個操作。

* 安裝Eclipse 4.3(Kepler)
* 根據Maven設定AEM專案
* 在Maven POM中為Eclipse準備JSP支援
* 將Maven專案匯入Eclipse

>[!NOTE]
>
>本指南以Eclipse 4.3(Kepler)和AEM 5.6.1為基礎。

## 安裝Eclipse {#install-eclipse}

從[Eclipse下載頁面](https://www.eclipse.org/downloads/)下載「Eclipse IDE for Java EE Developers」。

按照[安裝說明](https://wiki.eclipse.org/Eclipse/Installation)安裝Eclipse。

## 根據Maven {#set-up-your-aem-project-based-on-maven}設定AEM專案

接下來，使用Maven設定專案，如[How-To Build AEM Projects using Apache Maven](/help/sites-developing/ht-projects-maven.md)中所述。

## 準備Eclipse {#prepare-jsp-support-for-eclipse}的JSP支援

Eclipse也可提供使用JSP的支援，例如

* 自動完成標籤庫
* &lt;cq:defineObjects />和&lt;sling:defineObjects />所定義物件的Eclipse感知

讓其發揮作用：

1. 按照[How-To Work with JSPs](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)中的說明，使用Apache Maven](/help/sites-developing/ht-projects-maven.md)建立AEM專案。[
1. 將下列項目新增至內容模組POM的&lt;build />區段。

   Eclipse的Maven支援外掛程式m2e不提供對maven-jspc-plugin的支援，此配置指示m2e忽略外掛程式以及清理臨時編譯結果的相關任務。

   這不是問題：如[How-To Work with JSPs](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)中所述，此設定中的maven-jspc-plugin僅用於驗證JSP編譯為構建過程的一部分。 Eclipse已報告JSP中的任何問題，並且不依賴此Maven插件才能執行此操作。

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

### 將Maven專案匯入Eclipse {#import-the-maven-project-into-eclipse}

1. 在Eclipse中，選擇檔案>導入……
1. 在「匯入」對話方塊中，選擇「Maven >現有Maven專案」，然後按一下「下一步」。

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. 輸入項目頂級資料夾的路徑，然後按一下「全部選擇」和「完成」。

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 您現在都可以使用Eclipse來開發AEM專案，包括JSP自動完成。

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >如果您在`/libs`中包含`/libs/foundation/global.jsp`或其他JSP，則需要將其複製到您的項目，以便Eclipse能夠解析包含。 同時，您必須確定Maven未將其整合至您的內容套件中。 如何達成此目標，請參閱[如何使用Apache Maven](/help/sites-developing/ht-projects-maven.md)建立AEM專案。
