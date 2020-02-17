---
title: 如何以程式設計方式存取AEM JCR
seo-title: 如何以程式設計方式存取AEM JCR
description: 您可以程式設計方式修改位於AEM儲存庫中的節點和屬性，而AEM儲存庫是Adobe Marketing cloud的一部分
seo-description: 您可以程式設計方式修改位於AEM儲存庫中的節點和屬性，而AEM儲存庫是Adobe Marketing cloud的一部分
uuid: 2051d03f-430a-4cae-8f6d-e5bc727d733f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 69f62a38-7991-4009-8db7-ee8fd35dc535
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970

---


# 如何以程式設計方式存取AEM JCR{#how-to-programmatically-access-the-aem-jcr}

您可以程式設計方式修改位於Adobe CQ儲存庫中的節點和屬性，此儲存庫是Adobe Marketing cloud的一部分。 若要存取CQ儲存庫，請使用Java內容儲存庫(JCR)API。 您可以使用Java JCR API，對位於Adobe CQ儲存庫中的內容執行建立、取代、更新和刪除(CRUD)作業。 如需Java JCR API的詳細資訊，請參閱 [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html)。

>[!NOTE]
>
>本開發文章會從外部Java應用程式修改Adobe CQ JCR。 相反地，您可以使用JCR API從OSGi套件中修改JCR。 如需詳細資訊，請 [參閱「Java內容儲存庫中的持續CQ資料」](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html)。

>[!NOTE]
>
>若要使用JCR API，請將 `jackrabbit-standalone-2.4.0.jar` 檔案新增至Java應用程式的類別路徑。 您可從Java JCR API網頁(https://jackrabbit.apache.org/jcr/jcr-api.html)取得此JAR [檔案](https://jackrabbit.apache.org/jcr/jcr-api.html)。

>[!NOTE]
>
>如要瞭解如何使用JCR查詢API查詢Adobe CQ JCR，請參 [閱使用JCR API查詢Adobe Experience Manager資料](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)。

## 建立儲存庫實例 {#create-a-repository-instance}

雖然連接儲存庫和建立連接的方式不同，但本開發文章使用屬於類的靜態方 `org.apache.jackrabbit.commons.JcrUtils` 法。 方法的名稱為 `getRepository`。 此方法會使用字串參數，代表Adobe CQ伺服器的URL。 例如 `http://localhost:4503/crx/server`。

方 `getRepository`法傳回 `Repository`例項，如下列程式碼範例所示。

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## 建立會話實例 {#create-a-session-instance}

實 `Repository`例代表CRX儲存庫。 您使用實 `Repository`例與儲存庫建立會話。 若要建立工作階段，請 `Repository`叫用例項的 `login`方法並傳遞 `javax.jcr.SimpleCredentials` 物件。 該方 `login`法返回實 `javax.jcr.Session` 例。

您可使用其 `SimpleCredentials`建構函式並傳遞下列字串值來建立物件：

* 用戶名；
* 對應的密碼

傳遞第二個參數時，請呼叫String物件的方 `toCharArray`法。 下列程式碼說明如何呼叫傳 `login`回的方法 `javax.jcr.Sessioninstance`。

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## 建立節點實例 {#create-a-node-instance}

使用 `Session`例項建立例 `javax.jcr.Node` 項。 實例 `Node`可讓您執行節點操作。 例如，您可以建立新節點。 要建立表示根節點的節點，請調 `Session`用實例的 `getRootNode` 方法，如以下代碼行所示。

```java
//Create a Node
Node root = session.getRootNode();
```

建立實例後， `Node`可以執行諸如建立另一個節點和向其添加值之類的任務。 例如，下列程式碼會建立兩個節點，並新增值至第二個節點。

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## 檢索節點值 {#retrieve-node-values}

若要擷取節點及其值，請叫用 `Node`例項的 `getNode`方法，並傳遞一個字串值，代表節點的完全限定路徑。 請考慮在上一個代碼示例中建立的節點結構。 若要擷取日節點，請指定adobe/day，如下列程式碼所示：

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## 在Adobe CQ Repository中建立節點 {#create-nodes-in-the-adobe-cq-repository}

下列Java程式碼範例代表連線至Adobe CQ、建立例項及新增節 `Session`點的Java類別。 節點被分配一個資料值，然後節點的值及其路徑被寫出到控制台。 完成會話後，請務必註銷。

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

運行完整代碼示例並建立節點後，可以在 **[!UICONTROL CRXDE Lite中查看新節點]**，如下圖所示。

![chlimage_1-68](assets/chlimage_1-68a.png)

