---
title: 運算式產生器中的遠端函式
seo-title: 運算式產生器
description: 「對應管理」中的運算式產生器可讓您建立運算式和遠端函式。
seo-description: 「對應管理」中的運算式產生器可讓您建立運算式和遠端函式。
uuid: 6afb84c0-ad03-4bb1-a154-d46cc47650ae
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 68e3071e-7ce6-4bdc-8561-14bcaeae2b6c
docset: aem65
translation-type: tm+mt
source-git-commit: 5a586758da84f467e075adcc33cdcede2fbf09c7

---


# 運算式產生器中的遠端函式{#remote-functions-in-expression-builder}

使用運算式產生器，您可以建立運算式或條件，對資料字典或使用者提供的資料值執行運算。 「對應管理」會使用運算式評估的結果來選取文字、影像、清單和條件等資產，並視需要將它們插入對應項目中。

## 使用運算式產生器建立運算式和遠端函式 {#creating-expressions-and-remote-functions-with-expression-builder}

運算式產生器內部使用JSP EL程式庫，因此運算式符合JSPEL語法。 如需詳細資訊，請參閱 [範例運算式](#exampleexpressions)。

![運算式產生器](assets/expressionbuilder.png)

### 營運商 {#operators}

運算式中可用的運算子位於運算式產生器的頂端列。

### 範例運算式 {#exampleexpressions}

以下是一些常用的JSP EL示例，可用於您的通信管理解決方案：

* 要添加兩個數字：${number1 + number2}
* 串連兩個字串：${str1} ${str2}
* 要比較兩個數字：${age &lt; 18}

您可以在 [JSP EL規範中找到詳細資訊](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf)。 用戶端運算式管理器不支援JSP EL規格中的某些變數和函式，具體而言：

* 在用戶端上評估的運算式的變 [] 數名稱中，不支援系列索引和對應索引鍵（使用記號）。
* 以下是運算式中使用的函式的參數類型或返回類型：

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * 布林值 (Boolean)
   * java.lang.Integer
   * Int
   * java.util.list
   * java.lang.Short
   * 簡短
   * java.lang.Byte
   * 位元組
   * java.lang.Double
   * 雙精準數
   * java.lang.Long
   * 長整數
   * java.lang.Float
   * 浮點
   * java.util.Calendar
   * java.util.Date
   * java.util.list

### 遠端功能 {#remote-function}

遠端函式提供在運算式中使用自訂邏輯的功能。 您可以編寫自訂邏輯，以便在運算式中以Java方法的形式使用，而在運算式中可使用相同的函式。 可用的遠程函式列在表達式編輯器左側的「遠程函式」頁籤下。

![remotefunction](assets/remotefunction.png)

#### 添加自定義遠程功能 {#adding-custom-remote-functions}

您可以建立自訂搭售，以匯出您自己的遠端函式，以便在運算式內使用。 若要建立自訂套件以匯出您自己的遠端功能，請執行下列工作。 它示範如何編寫自訂函式，以便將其輸入字串大寫。

1. 為OSGi服務定義一個介面，該介麵包含要導出以供「表達式管理器」使用的方法。
1. 在介面A上宣告方法，並使用@ServiceMethod附註(com.adobe.exm.expeval.ServiceMethod)加以註解。 「運算式管理員」會忽略任何未加註的方法。 ServiceMethod批注具有以下可選屬性，也可以指定：

   1. **啟用**:確定是否啟用此方法。 運算式管理員會忽略停用的方法。
   1. **familyId**:指定方法的族（組）。 如果為空，則「表達式管理器」假定該方法屬於預設族。 沒有從中選擇函式的族（預設的族除外）的註冊表。 運算式管理器動態建立註冊表，方法是使用由各種組合導出的所有函式指定的所有族ID的聯合。 請確定他們在此處指定的ID是可讀的，因為它也會顯示在運算式製作使用者介面中。
   1. **displayName**:函式的可人讀名稱。 此名稱用於製作使用者介面中的顯示用途。 如果為空，則表達式管理器使用函式的前置詞和local-name構建預設名稱。
   1. **說明**:函式的詳細說明。 此說明用於編寫使用者介面中的顯示用途。 如果為空，則表達式管理器使用函式的前置詞和local-name構建預設說明。

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   方法的參數也可以選擇性地使用@ServiceMethodParameter註解(com.adobe.exm.expeval.ServiceMethodParameter)加以註解。 此注釋僅用於指定人工可讀的名稱和方法參數的說明，以便用於編寫用戶介面。 確保介面方法的參數和返回值屬於以下類型之一：

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * 布林值 (Boolean)
   * java.lang.Integer
   * Int
   * java.lang.Short
   * 簡短
   * java.lang.Byte
   * 位元組
   * java.lang.Double
   * 雙精準數
   * java.lang.Long
   * 長整數
   * java.lang.Float
   * 浮點
   * java.util.Calendar
   * java.util.Date
   * java.util.list


1. 定義介面的實施、將其配置為OSGI服務並定義以下服務屬性：

```
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "<service_id>"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
```

exm.service=true條目會指示運算式管理員，該服務包含適用於運算式的遠端函式。 &lt;service_id>值必須是有效的Java識別碼（英數字元、$、_，不含其他特殊字元）。 此值加上REMOTE_關鍵字前置詞，構成運算式內使用的首碼。 例如，使用REMOTE_foo:bar()可以在表達式內引用帶有注釋方法bar()和服務屬性中的服務ID foo的介面。

```
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

以下是要使用的範例封存：

* **GoodFunctions.jar.zip** 是包含示例遠程函式定義的包的jar檔案。 下載GoodFunctions.jar.zip檔案並解壓縮以取得jar檔案。
* **GoodFunctions.zip是原始碼套件** ，可用來定義自訂遠端函式並為其建立套件。

GoodFunctions.jar.zip

[取得檔案](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[取得檔案](assets/goodfunctions.zip)
