---
title: 運算式產生器中的遠端函式
seo-title: Expression Builder
description: 通信管理中的運算式產生器可讓您建立運算式和遠端函式。
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

# 運算式產生器中的遠端函式{#remote-functions-in-expression-builder}

使用運算式產生器，您可以建立運算式或條件，對資料字典或一般使用者提供的資料值執行運算。 通信管理使用運算式評估的結果來選取資產（例如文字、影像、清單和條件），並視需要將其插入通信中。

## 使用運算式產生器建立運算式和遠端函式 {#creating-expressions-and-remote-functions-with-expression-builder}

運算式產生器內部使用JSP EL程式庫，因此運算式遵循JSPEL語法。 如需詳細資訊，請參閱 [範例運算式](#exampleexpressions).

![運算式產生器](assets/expressionbuilder.png)

### 運算子 {#operators}

運算式中可用的運算子位於運算式產生器的頂端列。

### 範例運算式 {#exampleexpressions}

以下是一些常用的JSP EL示例，可用於通信管理解決方案：

* 若要新增兩個數字：${number1 + number2}
* 串連兩個字串：${str1} ${str2}
* 要比較兩個數字：${age &lt; 18}

您可以在 [JSP EL規範](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf). 客戶端表達式管理器不支援JSP EL規範中的某些變數和函式，具體來說：

* 集合索引和映射鍵(使用 [] 變數名稱中不支援在用戶端上評估的運算式。
* 以下是運算式中使用的函式的參數類型或傳回類型：

   * java.lang.String
   * java.lang.Character
   * 字元
   * java.lang.Boolean
   * 布林值
   * java.lang.Integer
   * 整數
   * java.util.list
   * java.lang.Short
   * 簡短
   * java.lang.Byte
   * 位元組
   * java.lang.Double
   * 雙精度
   * java.lang.Long
   * 長整數
   * java.lang.Float
   * 浮點數
   * java.util.Calendar
   * java.util.Date
   * java.util.List

### 遠程函式 {#remote-function}

遠端函式提供在運算式中使用自訂邏輯的功能。 您可以撰寫自訂邏輯，以在運算式中作為Java中的方法使用，而在運算式內也可使用相同的函式。 可用的遠程函式列在運算式編輯器左側的「遠程函式」頁簽下。

![remotefunction](assets/remotefunction.png)

#### 添加自定義遠程函式 {#adding-custom-remote-functions}

您可以建立自訂套件組合，以匯出您自己的遠端函式，以便在運算式內使用。 要建立自定義套件以導出自己的遠程功能，請執行以下任務。 它示範如何撰寫自訂函式，將其輸入字串大寫。

1. 為OSGi服務定義介面，其中包含要匯出供運算式管理器使用的方法。
1. 在介面A上宣告方法，並以@ServiceMethod注(com.adobe.exm.expeval.ServiceMethod)加以註解。 「運算式管理器」會忽略任何未加註的方法。 ServiceMethod批注具有以下可選屬性，也可以指定這些屬性：

   1. **已啟用**:確定是否啟用此方法。 運算式管理器會忽略已停用的方法。
   1. **familyId**:指定方法的族（組）。 如果為空，則表達式管理器假定該方法屬於預設族。 沒有從中選擇函式的家族（預設家族除外）的登記。 運算式管理器通過採用由各種套件導出的所有函式指定的所有族ID的聯合來動態建立註冊表。 請確定他們在此處指定的ID可合理讀取，因為它也會顯示在運算式編寫使用者介面中。
   1. **displayName**:人類看得懂的函式名稱。 此名稱用於製作使用者介面中的顯示用途。 如果為空，則表達式管理器使用函式的前置詞和local-name構建預設名稱。
   1. **說明**:函式的詳細說明。 此說明用於製作使用者介面中的顯示用途。 如果為空，則表達式管理器使用函式的前置詞和local-name構建預設說明。

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   也可選擇使用@ServiceMethodParameter注釋(com.adobe.exm.exval.ServiceMethodParameter)來註解方法的參數。 此注釋僅用於指定在創作用戶介面中使用的人類可讀名稱和方法參數的說明。 確保介面方法的參數和返回值屬於以下類型之一：

   * java.lang.String
   * java.lang.Character
   * 字元
   * java.lang.Boolean
   * 布林值
   * java.lang.Integer
   * 整數
   * java.lang.Short
   * 簡短
   * java.lang.Byte
   * 位元組
   * java.lang.Double
   * 雙精度
   * java.lang.Long
   * 長整數
   * java.lang.Float
   * 浮點數
   * java.util.Calendar
   * java.util.Date
   * java.util.List


1. 定義介面的實作、將其設為OSGI服務，並定義下列服務屬性：

```jsp
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "<service_id>"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
```

exm.service=true項目會指示運算式管理器，指出服務包含適合在運算式中使用的遠端函式。 此 &lt;service_id> 值必須是有效的Java標識符（英數字元、$、_，不含其他特殊字元）。 此值的前置詞為REMOTE_關鍵字，會形成運算式內使用的前置詞。 例如，在服務屬性中具有帶注釋的方法bar()和服務ID foo的介面，可以使用REMOTE_foo:bar()在表達式中引用。

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

以下是要使用的封存範例：

* **GoodFunctions.jar.zip** 是jar檔案，其套件包含範例遠端函式定義。 下載GoodFunctions.jar.zip檔案，然後將其解壓縮以取得jar檔案。
* **GoodFunctions.zip** 是原始碼套件，用於定義自訂遠端函式並為其建立套件組合。

GoodFunctions.jar.zip

[取得檔案](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[取得檔案](assets/goodfunctions.zip)
