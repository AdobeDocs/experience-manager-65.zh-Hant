---
title: 提取用於翻譯的字串
seo-title: Extracting Strings for Translating
description: 使用xgettext-maven-plugin從需要翻譯的原始碼中提取字串
seo-description: Use xgettext-maven-plugin to extract strings from your source code that need translating
uuid: 2c586ecb-8494-4f8f-b31a-1ed73644d611
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 034f70f1-fbd2-4f6b-b07a-5758f0461a5b
exl-id: 4acc5f7f-0bcb-4b5a-8531-52e146cffeae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# 提取用於翻譯的字串{#extracting-strings-for-translating}

使用xgettext-maven-plugin從需要轉換的原始碼中提取字串。 Maven插件將字串提取到您發送的用於翻譯的XLIFF檔案。 字串從以下位置提取：

* Java源檔案
* Javascript源檔案
* SVN資源（JCR節點）的XML表示

## 配置字串提取 {#configuring-string-extraction}

配置xgettext-maven-plugin工具如何為項目提取字串。

```xml
/filter { }
/parsers {
   /vaultxml { }
   /javascript { }
   /regexp {
      /files {
         /java { }
         /jsp { }
         /extjstemplate { }
      }
   }
}
/potentials { }
```

| 章節 | 說明 |
|---|---|
| /filter | 標識已分析的檔案。 |
| /parsers/vaultxml | 配置Vault檔案的分析。 標識包含外部字串和本地化提示的JCR節點。 還標識要忽略的JCR節點。 |
| /parsers/javascript | 標識將字串外部化的Javascript函式。 您不需要更改此分區。 |
| /parsers/regexp | 配置Java、JSP和ExtJS模板檔案的分析。 您不需要更改此分區。 |
| /電位 | 用於檢測要國際化的字串的公式。 |

### 標識要分析的檔案 {#identifying-the-files-to-parse}

i18n.any檔案的/filter部分標識xgettext-maven-plugin工具解析的檔案。 添加多個包含和排除規則，這些規則分別標識被分析和忽略的檔案。 您應包括所有檔案，然後排除不想分析的檔案。 通常，您會排除不對UI有貢獻的檔案類型，或排除定義UI但未轉換的檔案。 包含和排除規則的格式如下：

```
{ /include "pattern" }
{ /exclude "pattern" }
```

規則的陣列部分用於匹配要包括或排除的檔案的名稱。 模式前置詞指示您是匹配JCR節點（其在Vault中的表示法）還是檔案系統。

| 字首 | 效果 |
|---|---|
| / | 指示JCR路徑。 因此，此前置詞與jcr_root目錄下的檔案匹配。 |
| &amp;ast; | 指示檔案系統上的常規檔案。 |
| 無 | 沒有前置詞或以資料夾或檔案名開頭的模式表示檔案系統上的常規檔案。 |

在陣列中使用時， /字元表示子目錄和&amp;ast;字元與所有字元匹配。 下表列出了幾個示例規則。

<table>
 <tbody>
  <tr>
   <th>示例規則</th>
   <th>效果</th>
  </tr>
  <tr>
   <td><code>{ /include "*" }</code></td>
   <td>包括所有檔案。</td>
  </tr>
  <tr>
   <td><code>{ /exclude "*.pdf" }</code></td>
   <td>排除所有PDF檔案。</td>
  </tr>
  <tr>
   <td><code> { /exclude "*/pom.xml" }</code></td>
   <td>排除POM檔案。</td>
  </tr>
  <tr>
   <td><code class="code">{ /exclude "/content/*" }
      { /include "/content/catalogs/geometrixx/templatepages" }
      { /include "/content/catalogs/geometrixx/templatepages/*" }</code></td>
   <td><p>排除/content節點下的所有檔案。</p> <p>包括/content/catalogs/geometrixx/templatepages節點。</p> <p>包括/content/catalogs/geometrixx/templatepages的所有子節點。</p> </td>
  </tr>
 </tbody>
</table>

### 提取字串  {#extracting-the-strings}

沒有POM:

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

使用POM:將此項添加到POM:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.adobe.granite.maven</groupId>
            <artifactId>xgettext-maven-plugin</artifactId>
            <version>1.1</version>
            <configuration>
                <rules>i18n.any</rules>
                <root>jcr_root</root>
                <xliff>cq.xliff</xliff>
                <verbose>true</verbose>
            </configuration>
        </plugin>
    </plugins>
</build>
```

命令：

```shell
mvn xgettext:extract
```

### 輸出檔案 {#output-files}

* `raw.xliff`:提取字串
* `warn.log`:警告（如果有），如果 `CQ.I18n.getMessage()` API使用不正確。 這些總是需要修復，然後重新運行。

* `parserwarn.log`:分析器警告（如果有），例如js分析器發出
* `potentials.xliff`:未提取的「潛在」候選項，但可能是需要翻譯的人可讀字串（可以忽略，仍會產生大量誤報）
* `strings.xliff`:平整的xliff檔案，要導入到ALF
* `backrefs.txt`:允許快速查找給定字串的原始碼位置
