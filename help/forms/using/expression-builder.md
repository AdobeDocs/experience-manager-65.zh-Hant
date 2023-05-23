---
title: Expression Builder中的遠程函式
seo-title: Expression Builder
description: Oracle Tergement中的Expression Builder允許您建立表達式和遠程函式。
seo-description: Expression Builder in Correspondence Management lets you create expressions and remote functions.
uuid: 6afb84c0-ad03-4bb1-a154-d46cc47650ae
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 68e3071e-7ce6-4bdc-8561-14bcaeae2b6c
docset: aem65
feature: Correspondence Management
exl-id: b41af9fe-c698-44b3-9ac6-97d42cdc02d4
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# Expression Builder中的遠程函式{#remote-functions-in-expression-builder}

使用表達式生成器，可以建立對資料字典或最終用戶提供的資料值執行計算的表達式或條件。 Oracle Tergement使用表達式評估的結果來選擇文本、影像、清單和條件等資產，並根據需要將它們插入對應中。

## 使用表達式生成器建立表達式和遠程函式 {#creating-expressions-and-remote-functions-with-expression-builder}

表達式生成器內部使用JSP EL庫，因此表達式遵循JSPEL語法。 有關詳細資訊，請參見 [示例表達式](#exampleexpressions)。

![運算式產生器](assets/expressionbuilder.png)

### 運算子 {#operators}

在表達式中可用的運算子在表達式生成器的頂欄中可用。

### 示例表達式 {#exampleexpressions}

以下是幾個常用的JSP EL示例，您可以在「通信管理」解決方案中使用：

* 要添加兩個數字：${number1 +數字2}
* 要連接兩個字串：${str1} ${str2}
* 要比較兩個數字：${age &lt; 18}

您可以在 [JSP EL規範](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf)。 客戶端表達式管理器不支援JSP EL規範中的某些變數和函式，具體是：

* 集合索引和映射鍵(使用 [] 在客戶端上計算的表達式的變數名稱中不支援符號)。
* 以下是表達式中使用的函式的參數類型或返回類型：

   * java.lang.String
   * java.lang.Character
   * 查爾
   * java.lang.Boolean
   * 布林值
   * java.lang.Integer
   * 整型
   * java.util.list
   * java.lang.Short
   * 短
   * java.lang.Byte
   * 位元組
   * java.lang.Double
   * 雙精度
   * java.lang.Long
   * 長整數
   * java.lang.Float
   * 浮動
   * java.util.Calendar
   * java.util.Date
   * java.util.List

### 遠程函式 {#remote-function}

遠程函式提供了在表達式中使用自定義邏輯的功能。 可以將自定義邏輯寫入表達式中用作Java中的方法，而同一函式可以在表達式中使用。 可用的遠程函式列在表達式編輯器左側的「遠程函式」頁籤下。

![remote函式](assets/remotefunction.png)

#### 添加自定義遠程函式 {#adding-custom-remote-functions}

您可以建立自定義捆綁包以導出自己的遠程函式以在表達式內部使用。 要建立自定義捆綁包以導出您自己的遠程功能，請執行以下任務。 它演示了如何編寫自定義函式來使其輸入字串大寫。

1. 為OSGi服務定義一個介面，該介麵包含要導出以供表達式管理器使用的方法。
1. 在介面A上聲明方法，並使用@ServiceMethod注釋(com.adobe.exm.expaval.ServiceMethod)對其進行注釋。 表達式管理器忽略任何未注釋的方法。 ServiceMethod批注具有以下可選屬性，也可以指定這些屬性：

   1. **已啟用**:確定是否啟用此方法。 表達式管理器忽略禁用的方法。
   1. **家庭ID**:指定方法的族（組）。 如果為空，則表達式管理器假定該方法屬於預設族。 沒有從中選擇函式的族（預設的族除外）的註冊表。 Expression Manager通過採用由各個捆綁包導出的所有函式指定的所有族ID的聯合來動態建立註冊表。 請確保他們在此處指定的ID是可讀的，因為它也顯示在表達式創作用戶介面中。
   1. **displayName**:函式的可讀名稱。 此名稱用於創作用戶介面中的顯示目的。 如果為空，則表達式管理器使用函式的前置詞和local-name構建預設名稱。
   1. **說明**:函式的詳細說明。 此說明用於創作用戶介面中的顯示目的。 如果為空，則表達式管理器使用函式的前置詞和local-name構建預設說明。

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   也可以選擇使用@ServiceMethodParameter注釋(com.adobe.exm.expeval.ServiceMethodParameter)對方法的參數進行注釋。 此注釋僅用於指定在創作用戶介面中使用的方法參數的人可讀名稱和說明。 確保介面方法的參數和返回值屬於以下類型之一：

   * java.lang.String
   * java.lang.Character
   * 查爾
   * java.lang.Boolean
   * 布林值
   * java.lang.Integer
   * 整型
   * java.lang.Short
   * 短
   * java.lang.Byte
   * 位元組
   * java.lang.Double
   * 雙精度
   * java.lang.Long
   * 長整數
   * java.lang.Float
   * 浮動
   * java.util.Calendar
   * java.util.Date
   * java.util.List


1. 定義介面的實現，將其配置為OSGI服務，並定義以下服務屬性：

```jsp
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "<service_id>"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
```

exm.service=true條目指示表達式管理器，該服務包含適合在表達式中使用的遠程函式。 的 &lt;service_id> 值必須是有效的Java標識符（字母數字、$、_，沒有其他特殊字元）。 此值以REMOTE_關鍵字為前置詞，構成表達式內使用的前置詞。 例如，可在使用REMOTE_foo:bar()的表達式內引用帶有注釋方法bar()和服務屬性中的服務ID foo的介面。

```java
package mergeandfuse.com;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = true, immediate = true, label = "RemoteFunctionImpl")
@Service(value = RemoteFunction.class)
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "test1"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
public class RemoteFuntionImpl implements RemoteFunction {

 @Override
 public String toAllCaps(String name) {
  System.out.println("######Got######"+name);
  
  return name.toUpperCase();
 }
 
}
```

以下是要使用的示例存檔：

* **GoodFunctions.jar.zip** 是包含示例遠程函式定義的包的jar檔案。 下載GoodFunctions.jar.zip檔案並解壓縮它以獲取jar檔案。
* **GoodFunctions.zip** 是原始碼的包，用於定義自定義遠程函式並為其建立包。

GoodFunctions.jar.zip

[取得檔案](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[取得檔案](assets/goodfunctions.zip)
