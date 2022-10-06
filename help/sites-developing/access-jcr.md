---
title: 如何以程式設計方式存取AEM JCR
seo-title: How to programmatically access the AEM JCR
description: 您可以以程式設計方式修改位於AEM存放庫(屬於Adobe Marketing Cloud的一部分)內的節點和屬性
seo-description: You can programmatically modify nodes and properties located within the AEM repository, which is part of the Adobe Marketing Cloud
uuid: 2051d03f-430a-4cae-8f6d-e5bc727d733f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 69f62a38-7991-4009-8db7-ee8fd35dc535
exl-id: fe946b9a-b29e-4aa5-b973-e2a652417a55
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# 如何以程式設計方式存取AEM JCR{#how-to-programmatically-access-the-aem-jcr}

您可以以程式設計方式修改位於Adobe CQ存放庫(屬於Adobe Marketing Cloud的一部分)內的節點和屬性。 若要存取CQ存放庫，請使用Java Content Repository(JCR)API。 您可以使用Java JCR API對位於Adobe CQ存放庫內的內容執行建立、取代、更新和刪除(CRUD)作業。 如需Java JCR API的詳細資訊，請參閱 [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>本開發文章從外部Java應用程式修改Adobe CQ JCR。 相反地，您可以使用JCR API從OSGi套件組合內修改JCR。 如需詳細資訊，請參閱 [在Java內容存放庫中保留CQ資料](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html).

>[!NOTE]
>
>若要使用JCR API，請新增 `jackrabbit-standalone-2.4.0.jar` 檔案到Java應用程式的類路徑。 您可以從Java JCR API網頁()取得此JAR檔案： [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>若要了解如何使用JCR查詢API查詢Adobe CQ JCR，請參閱 [使用JCR API查詢Adobe Experience Manager資料](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## 建立儲存庫實例 {#create-a-repository-instance}

雖然連接到儲存庫和建立連接有不同的方法，但本開發文章使用屬於的靜態方法 `org.apache.jackrabbit.commons.JcrUtils` 類別。 方法的名稱為 `getRepository`. 此方法會採用代表Adobe CQ伺服器URL的字串參數。 例如 `http://localhost:4503/crx/server`.

此 `getRepository`方法傳回 `Repository`例項，如下列程式碼範例所示。

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## 建立工作階段例項 {#create-a-session-instance}

此 `Repository`例項代表CRX存放庫。 您使用 `Repository`例項，與存放庫建立工作階段。 若要建立工作階段，請叫用 `Repository`instance&#39;s `login`方法和傳遞 `javax.jcr.SimpleCredentials` 物件。 此 `login`方法傳回 `javax.jcr.Session` 例項。

您建立 `SimpleCredentials`物件，方法是使用其建構子並傳遞下列字串值：

* 用戶名；
* 對應的密碼

傳遞第二個參數時，請呼叫 `toCharArray`方法。 下列程式碼顯示如何呼叫 `login`傳回 `javax.jcr.Sessioninstance`.

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## 建立Node例項 {#create-a-node-instance}

使用 `Session`例項來建立 `javax.jcr.Node` 例項。 A `Node`例項可讓您執行節點作業。 例如，您可以建立新節點。 要建立表示根節點的節點，請調用 `Session`instance&#39;s `getRootNode` 方法，如下列程式碼行所示。

```java
//Create a Node
Node root = session.getRootNode();
```

建立 `Node`例項中，您可以執行建立其他節點和新增值等工作。 例如，下列程式碼會建立兩個節點，並將值新增至第二個節點。

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## 檢索節點值 {#retrieve-node-values}

若要擷取節點及其值，請叫用 `Node`instance&#39;s `getNode`方法，並將代表完全限定路徑的字串值傳遞至節點。 請考量上一個程式碼範例中建立的節點結構。 若要擷取day節點，請指定adobe/day，如下列程式碼所示：

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## 在Adobe CQ存放庫中建立節點 {#create-nodes-in-the-adobe-cq-repository}

下列Java程式碼範例代表連線至Adobe CQ的Java類別，會建立 `Session`執行個體，並新增節點。 節點被分配一個資料值，然後節點的值及其路徑被寫入控制台。 完成工作階段後，請務必登出。

```java
/*
 * This Java Quick Start uses the jackrabbit-standalone-2.4.0.jar
 * file. See the previous section for the location of this JAR file
 */

import javax.jcr.Repository;
import javax.jcr.Session;
import javax.jcr.SimpleCredentials;
import javax.jcr.Node;

import org.apache.jackrabbit.commons.JcrUtils;
import org.apache.jackrabbit.core.TransientRepository;

public class GetRepository {

public static void main(String[] args) throws Exception {

try {

    //Create a connection to the CQ repository running on local host
    Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");

   //Create a Session
   javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));

  //Create a node that represents the root node
  Node root = session.getRootNode();

  // Store content
  Node adobe = root.addNode("adobe");
  Node day = adobe.addNode("day");
  day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");

  // Retrieve content
  Node node = root.getNode("adobe/day");
  System.out.println(node.getPath());
  System.out.println(node.getProperty("message").getString());

  // Save the session changes and log out
  session.save();
  session.logout();
  }
 catch(Exception e){
  e.printStackTrace();
  }
 }
}
```

執行完整程式碼範例並建立節點後，即可在 **[!UICONTROL CRXDE Lite]**，如下圖所示。

![chlimage_1-68](assets/chlimage_1-68a.png)
