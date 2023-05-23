---
title: 如何以寫程式方式訪問AEMJCR
seo-title: How to programmatically access the AEM JCR
description: 可以以寫程式方式修改位於儲存庫AEM(屬於Adobe Marketing Cloud)中的節點和屬性
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

# 如何以寫程式方式訪問AEMJCR{#how-to-programmatically-access-the-aem-jcr}

可以以寫程式方式修改位於Adobe CQ系統資訊庫內的節點和屬性，該系統是Adobe Marketing Cloud的一部分。 要訪問CQ儲存庫，請使用Java內容儲存庫(JCR)API。 可以使用Java JCR API對位於Adobe CQ儲存庫中的內容執行建立、替換、更新和刪除(CRUD)操作。 有關Java JCR API的詳細資訊，請參見 [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html)。

>[!NOTE]
>
>本開發文章從外部Java應用程式修改Adobe CQJCR。 相反，您可以使用JCR API從OSGi捆綁包內修改JCR。 有關詳細資訊，請參閱 [將CQ資料保留在Java內容儲存庫中](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html)。

>[!NOTE]
>
>要使用JCR API，請添加 `jackrabbit-standalone-2.4.0.jar` 檔案到Java應用程式的類路徑。 可以從Java JCR API網頁獲取此JAR檔案，網址為 [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html)。

>[!NOTE]
>
>要瞭解如何使用JCR查詢API查詢Adobe CQJCR，請參閱 [使用JCR API查詢Adobe Experience Manager資料](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)。

## 建立儲存庫實例 {#create-a-repository-instance}

雖然連接儲存庫和建立連接的方法不同，但本開發文章使用的靜態方法屬於 `org.apache.jackrabbit.commons.JcrUtils` 類。 方法的名稱為 `getRepository`。 此方法採用一個字串參數，該參數表示Adobe CQ伺服器的URL。 例如 `http://localhost:4503/crx/server`。

的 `getRepository`方法返回 `Repository`實例，如以下代碼示例所示。

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## 建立會話實例 {#create-a-session-instance}

的 `Repository`實例表示CRX儲存庫。 使用 `Repository`與儲存庫建立會話的實例。 要建立會話，請調用 `Repository`實例 `login`方法和通過 `javax.jcr.SimpleCredentials` 的雙曲餘切值。 的 `login`方法返回 `javax.jcr.Session` 實例。

建立 `SimpleCredentials`對象，並傳遞以下字串值：

* 用戶名；
* 相應的密碼

傳遞第二個參數時，調用String對象 `toCharArray`的雙曲餘切值。 以下代碼顯示如何調用 `login`方法返回 `javax.jcr.Sessioninstance`。

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## 建立節點實例 {#create-a-node-instance}

使用 `Session`建立實例 `javax.jcr.Node` 實例。 A `Node`實例允許您執行節點操作。 例如，可以建立新節點。 要建立表示根節點的節點，請調用 `Session`實例 `getRootNode` 方法，如下面的代碼行所示。

```java
//Create a Node
Node root = session.getRootNode();
```

建立 `Node`實例中，您可以執行任務，如建立另一個節點並為其添加值。 例如，以下代碼建立兩個節點，並向第二個節點添加一個值。

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## 檢索節點值 {#retrieve-node-values}

要檢索節點及其值，請調用 `Node`實例 `getNode`方法，並將表示完全限定路徑的字串值傳遞給節點。 請考慮在上一個代碼示例中建立的節點結構。 要檢索日節點，請指定adobe/day，如以下代碼所示：

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## 在Adobe CQ儲存庫中建立節點 {#create-nodes-in-the-adobe-cq-repository}

以下Java代碼示例表示連接到Adobe CQ的Java類，建立 `Session`實例，並添加新節點。 為節點分配資料值，然後將節點的值及其路徑寫出到控制台。 完成會話後，請確保註銷。

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

運行完整代碼示例並建立節點後，可以在 **[!UICONTROL CRXDE Lite]**，如下圖所示。

![chlimage_1-68](assets/chlimage_1-68a.png)
