---
title: 如何使用VLT工具
seo-title: 如何使用VLT工具
description: Jackrabbit FileVault工具(VLT)由Apache Foundation開發，可將Jackrabbit/AEM例項的內容對應至您的檔案系統
seo-description: Jackrabbit FileVault工具(VLT)由Apache Foundation開發，可將Jackrabbit/AEM例項的內容對應至您的檔案系統
uuid: 579e7785-8b50-4366-b562-8e79b6451464
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a76425e9-fd3b-4c73-80f9-0ebabb8fd94f
translation-type: tm+mt
source-git-commit: a7c3848704ee2b4b984fafcd82e29a75ea8d3443

---


# 如何使用VLT工具 {#how-to-use-the-vlt-tool}

Jackrabbit FileVault工具(VLT)是 [Apache Foundation](https://www.apache.org/) (Apache Foundation)開發的工具，可將Jackrabbit/AEM例項的內容對應至您的檔案系統。 VLT工具具有與源控制系統客戶端(如Subversion(SVN)客戶端)類似的功能，提供正常的簽入、簽出和管理操作，以及用於靈活呈現項目內容的配置選項。

從命令行運行VLT工具。 本檔案說明如何使用此工具，包括如何開始使用和取得說明，以及所有命令和可用選 [項](#vlt-commands) 的清 [單](#vlt-global-options)。

## 概念與架構 {#concepts-and-architecture}

如需Filevault工具 [的概念與結構的完整概觀，請參閱官方](https://jackrabbit.apache.org/filevault/overview.html) Apache Jackrabbit Filevault檔案中的「Filevault概觀 [」和「](https://jackrabbit.apache.org/filevault/vaultfs.html)[](https://jackrabbit.apache.org/filevault/index.html) Vault FS」頁面。

## VLT快速入門 {#getting-started-with-vlt}

若要開始使用VLT，您必須執行下列動作：

1. 安裝VLT、更新環境變數和更新全局忽略的subversion檔案。
1. 設定AEM存放庫（如果您尚未這麼做）。
1. 查看AEM存放庫。
1. 與儲存庫同步。
1. 測試同步是否有效。

### 安裝VLT工具 {#installing-the-vlt-tool}

若要使用VLT工具，您必須先安裝它。 由於它是額外的工具，因此預設不會安裝它。 此外，您還需要設定系統的環境變數。

1. 從 [Apache Jackrabbit網站下載FileVault封存檔。](https://jackrabbit.apache.org/jcr/downloads.html#vlt)
   >[!NOTE]
   >
   >VLT工具的來源可在GitHub [上使用。](https://github.com/apache/jackrabbit-filevault)
1. 解壓縮檔案。
1. 將命 `<archive-dir>/vault-cli-<version>/bin` 令檔案添加到 `PATH` 您的環境中，以便 `vlt` 根據需要訪問命令 `vlt.bat` 檔案。 例如：

   `<aem-installation-dir>/crx-quickstart/opt/helpers/vault-cli-3.1.16/bin>`

1. 開啟命令行shell並執行 `vlt --help`。 請確定輸出類似下列說明畫面：

   ```shell
   vlt --help
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   Usage:
     vlt [options] <command> [arg1 [arg2 [arg3] ..]]
   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   
   Global options:
   
     -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
     -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
     --credentials <arg>      The default credentials to use
     --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
     --config <arg>           The JcrFs config to use
     -v (--verbose)           verbose output
     -q (--quiet)             print as little as possible
     --version                print the version information and exit
     --log-level <level>      the log4j log level
     -h (--help) <command>    print this help
   ```

安裝後，您需要更新全局忽略的subversion檔案。 編輯svn設定並新增下列項目：

```xml
[miscellany]
### Set global-ignores to a set of whitespace-delimited globs
### which Subversion will ignore in its 'status' output, and
### while importing or adding files and directories.
global-ignores = .vlt
```

### 設定行尾字元 {#configuring-the-end-of-line-character}

VLT會根據下列規則自動處理行尾(EOF):

* 在Windows端以 `CRLF`
* 在Linux/Unix上以 `LF`
* 儲存庫的檔案行以 `LF`

為確保VLT和SVN配置匹配，應將屬 `svn:eol-style` 性設定 `native` 為，以擴展儲存在儲存庫中的檔案。 編輯svn設定並新增下列項目：

```xml
[auto-props]
*.css = svn:eol-style=native
*.cnd = svn:eol-style=native
*.java = svn:eol-style=native
*.js = svn:eol-style=native
*.json = svn:eol-style=native
*.xjson = svn:eol-style=native
*.jsp = svn:eol-style=native
*.txt = svn:eol-style=native
*.html = svn:eol-style=native
*.xml = svn:eol-style=native
*.properties = svn:eol-style=native
```

### 簽出儲存庫 {#checking-out-the-repository}

使用源控制系統簽出儲存庫。 例如，在svn中鍵入以下內容（用儲存庫替換URI和路徑）:

```shell
svn co https://svn.server.com/repos/myproject
```

### 與儲存庫同步 {#synchronizing-with-the-repository}

您需要將檔案與儲存庫同步。 要執行此操作：

1. 在命令行中，導航至 `content/jcr_root`。
1. 通過鍵入以下內容(將埠號替換為 **4502** 和管理員密碼)來檢查儲存庫：

   ```shell
   vlt --credentials admin:admin co --force http://localhost:4502/crx
   ```

   >[!NOTE]
   >
   >初次結帳時，必須只指定一次認證。 然後，這些檔案將儲存在您的主目錄中 `.vault/auth.xml`。

### 測試同步是否有效 {#testing-whether-the-synchronization-worked}

簽出儲存庫並同步後，您應進行測試，以確保所有操作都正常運行。 要執行此操作，一個簡單的方法是編輯 **.jsp檔案** ，並查看提交更改後是否反映您的更改。

要測試同步，請執行以下操作：

1. 導航到 `.../jcr_content/libs/foundation/components/text`.
1. 在中編輯內 `text.jsp`容。
1. 透過輸入 `vlt st`
1. 透過輸入 `vlt diff text.jsp`
1. 提交更改： `vlt ci test.jsp`。
1. 重新載入包含文字元件的頁面，並查看您的變更是否存在。

## 取得VLT工具的協助 {#getting-help-with-the-vlt-tool}

安裝VLT工具後，可從命令行訪問其幫助檔案：

```shell
vlt --help
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Jackrabbit FileVault [version 3.1.16] Copyright 2013 by Apache Software Foundation. See LICENSE.txt for more information.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Usage:
  vlt [options] <command> [arg1 [arg2 [arg3] ..]]
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Global options:
  -Xjcrlog <arg>           Extended JcrLog options (omit argument for help)
  -Xdavex <arg>            Extended JCR remoting options (omit argument for help)
  --credentials <arg>      The default credentials to use
  --update-credentials     if present the credentials-to-host list is updated in the ~/.vault/auth.xml
  --config <arg>           The JcrFs config to use
  -v (--verbose)           verbose output
  -q (--quiet)             print as little as possible
  --version                print the version information and exit
  --log-level <level>      the log4j log level
  -h (--help) <command>    print this help
Commands:
  export                   Export the Vault filesystem
  import                   Import a Vault filesystem
  checkout (co)            Checkout a Vault file system
  status (st)              Print the status of working copy files and directories.
  update (up)              Bring changes from the repository into the working copy.
  info                     Displays information about a local file.
  commit (ci)              Send changes from your working copy to the repository.
  revert (rev)             Restore pristine working copy file (undo most local edits).
  resolved (res)           Remove 'conflicted' state on working copy files or directories.
  propget (pg)             Print the value of a property on files or directories.
  proplist (pl)            Print the properties on files or directories.
  propset (ps)             Set the value of a property on files or directories.
  add                      Put files and directories under version control.
  delete (del,rm)          Remove files and directories from version control.
  diff (di)                Display the differences between two paths.
  rcp                      Remote copy of repository content.
  sync                     Control vault sync service
  console                  Run an interactive console
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
```

有關特定命令的幫助，請鍵入help命令，後跟命令的名稱。 例如：

```shell
vlt --help export
Usage:
 export -v|-t <arg>|-p <uri> <jcr-path> <local-path>

Description:
  Export the Vault filesystem mounted at <uri> to the local filesystem at <local-path>. An optional <jcr-path> can be specified in order to export just a sub tree.
  Example:
    vlt export http://localhost:4502/crx /apps/geometrixx myproject

Options:
  -v (--verbose)          verbose output
  -t (--type) <arg>       specifies the export type. either 'platform' or 'jar'.
  -p (--prune-missing)    specifies if missing local files should be deleted.
  <uri>                   mountpoint uri
  <jcr-path>              the jcr path
  <local-path>            the local path
```

## 在VLT中執行的常見任務 {#common-tasks-performed-in-vlt}

以下是在VLT中執行的一些常見任務。 有關每個命令的詳細資訊，請參見各 [個命令](#vlt-commands)。

### 檢出子樹 {#checking-out-a-subtree}

例如，如果只想簽出儲存庫的子樹， `/apps/geometrixx`則可通過鍵入以下內容來執行此操作：

```shell
vlt co http://localhost:4502/crx/-/jcr:root/apps/geometrixx geo
```

這樣做會建立包含和目錄 `geo` 的新匯 `META-INF` 出根 `jcr_root` 目錄，並將下方的所有檔案 `/apps/geometrixx` 放入 `geo/jcr_root`。

### 執行篩選結帳 {#performing-a-filtered-checkout}

如果您有現有的工作區篩選器，並且想要使用它進行檢出，則可以先建立目錄並將篩選器放在該目錄，或者按如下方式在命令行中指定該篩選器： `META-INF/vault`

```shell
$ vlt co --filter filter.xml http://localhost:4502/crx/-/jcr:root geo
```

範例篩選：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/etc/designs/geometrixx" />
    <filter root="/apps/geometrixx"/>
</workspaceFilter>
```

### 使用匯入／匯出，而非。vlt控制 {#using-import-export-instead-of-vlt-control}

您可以在JCR儲存庫和本地檔案系統之間導入和導出內容，而無需使用控制檔案。

若要匯入和匯出內容而不使用控 `.vlt` 制項：

1. 初始設定儲存庫：

   ```shell
   $ cd /projects
   $ svn mkdir https://svn.server.com/repos/myproject
   $ svn co https://svn.server.com/repos/myproject
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx geometrixx
   $ cd geometrixx/
   $ svn add META-INF/ jcr_root/
   $ svn ci
   ```

1. 更改遠程拷貝並更新JCR:

   ```shell
   $ cd /projects/geometrixx
   $ vlt -v import http://localhost:4502/crx . /
   ```

1. 更改遠程副本並更新檔案伺服器：

   ```shell
   $ cd /projects/geometrixx
   $ vlt export -v http://localhost:4502/crx /apps/geometrixx .
   $ svn st
   M      META-INF/vault/properties.xml
   M      jcr_root/apps/geometrixx/components/contentpage/.content.xml
   $ svn ci
   ```

## 使用VLT {#using-vlt}

要在VLT中發出命令，請在命令行中鍵入以下命令：

```shell
vlt [options] <command> [arg1 [arg2 [arg3] ..]]  
```

以下各節將詳細說明選項和命令。

## VLT全局選項 {#vlt-global-options}

以下是VLT選項清單，這些選項可用於所有命令。 有關其他可用選項的資訊，請參見各個命令。

|  |  |
|--- |--- |
| 選項 | 說明 |
| `-Xjcrlog <arg>` | 擴充的JcrLog選項 |
| `-Xdavex <arg>` | 擴充的JCR遠端選項 |
| `--credentials <arg>` | 要使用的預設憑據 |
| `--config <arg>` | 要使用的JcrFs組態 |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 盡可能少地打印 |
| `--version` | 列印版本資訊並退出VLT |
| `--log-level <level>` | 指示日誌級別，例如log4j日誌級別。 |
| `-h (--help) <command>` | 列印該特定命令的說明 |

## VLT命令 {#vlt-commands}

下表說明所有可用的VLT命令。 有關語法、可用選項和示例的詳細資訊，請參見各個命令。

|  |  |  |
|--- |--- |--- |
| 命令 | 縮寫命令 | 說明 |
| `export` |  | 從JCR儲存庫（Vault檔案系統）導出到本地檔案系統，而無控制檔案。 |
| `import` |  | 將本地檔案系統導入JCR儲存庫（Vault檔案系統）。 |
| `checkout` | `co` | 檢出Vault檔案系統。 將它用於本地檔案系統的初始JCR儲存庫。 (注意：您必須首先在subversion中籤出儲存庫。) |
| `analyze` |  | 分析包。 |
| `status` | `st` | 打印工作副本檔案和目錄的狀態。 |
| `update` | `up` | 將更改從儲存庫導入工作副本。 |
| `info` |  | 顯示有關本機檔案的資訊。 |
| `commit` | `ci` | 將工作副本中的更改發送到儲存庫。 |
| `revert` | `rev` | 將工作副本檔案還原為原始狀態，並取消大部分的本機編輯。 |
| `resolved` | `res` | 刪除工作副本檔案或目錄上的衝突狀態。 |
| `propget` | `pg` | 在檔案或目錄上打印屬性的值。 |
| `proplist` | `pl` | 在檔案或目錄上打印屬性。 |
| `propset` | `ps` | 在檔案或目錄上設定屬性的值。 |
| `add` |  | 將檔案和目錄置於版本控制之下。 |
| `delete` | `del` 或 `rm` | 從版本控制中移除檔案和目錄。 |
| `diff` | `di` | 顯示兩個路徑之間的差異。 |
| `console` |  | 執行互動式主控台。 |
| `rcp` |  | 將一個節點樹從一個遠程儲存庫複製到另一個遠程儲存庫。 |
| `sync` |  | 允許控制保險儲存同步服務。 |

### 匯出 {#export}

將裝載在&lt;uri>的Vault檔案系統導出到位於&lt;local-path>的本地檔案系統。 可以指定可選&lt;jcr-path>，以便僅導出子樹。

#### 語法 {#syntax}

```shell
export -v|-t <arg>|-p <uri> <jcr-path> <local-path>
```

#### 選項 {#options}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-t (--type) <arg>` | 指定導出類型，平台或jar。 |
| `-p (--prune-missing)` | 指定是否應刪除缺少的本地檔案 |
| `<uri>` | mountpoint uri |
| `<jcrPath>` | JCR路徑 |
| `<localPath>` | 本地路徑 |

#### 範例 {#examples}

```shell
vlt export http://localhost:4502/crx /apps/geometrixx myproject
```

### 匯入 {#import}

導入本地檔案系統(從 `<local-path>` 開始到電子倉庫檔案系統 `<uri>`)。 您可以指定 `<jcr-path>` 為匯入根目錄。 如果 `--sync` 已指定，則導入的檔案將自動置於保險儲存控制下。

#### 語法 {#syntax-1}

```shell
import -v|-s <uri> <local-path> <jcr-path>
```

#### 選項 {#options-1}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-s (-- sync)` | 將本地檔案置於保險儲存控制之下 |
| `<uri>` | mountpoint uri |
| `<jcrPath>` | JCR路徑 |
| `<localPath>` | 本地路徑 |

#### 範例 {#examples-1}

```shell
vlt import http://localhost:4502/crx . /
```

### 結帳(co) {#checkout-co}

從JCR儲存庫對本地檔案系統執行初始簽出，從&lt;uri>開始，對&lt;local-path>的本地檔案系統執行初始簽出。 您也可以添加&lt;jcrPath>參數來檢出遠程樹的子目錄。 可以指定將其複製到META-INF目錄中的工作區篩選器。

#### 語法 {#syntax-2}

```shell
checkout --force|-v|-q|-f <file> <uri> <jcrPath> <localPath>  
```

#### 選項 {#options-2}

|  |  |
|--- |--- |
| `--force` | 強制簽出以覆蓋本地檔案（如果檔案已存在） |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `-f (--filter) <file>` | 指定如果未定義自動篩選 |
| `<uri>` | mountpoint uri |
| `<jcrPath>` | （可選）遠程路徑 |
| `<localPath>` | （可選）本機路徑 |

#### 範例 {#examples-2}

使用JCR Remoting:

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/crx.default/jcr_root/
```

使用預設工作區：

```shell
vlt --credentials admin:admin co http://localhost:8080/crx/server/-/jcr_root/
```

如果URI不完整，則將展開它：

```shell
vlt --credentials admin:admin co http://localhost:8080/crx
```

### 分析 {#analyze}

分析包。

#### 語法 {#syntax-3}

```shell
analyze -l <format>|-v|-q <localPaths1> [<localPaths2> ...]
```

#### 選項 {#options-3}

|  |  |
|--- |--- |
| `-l (--linkFormat) <format>` | 修補程式連結的printf格式（名稱、id），例如 `[CQ520_HF_%s|%s]` |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `<localPaths> [<localPaths> ...]` | 本地路徑 |

### 狀態 {#status}

打印工作副本檔案和目錄的狀態。

如果 `--show-update` 已指定，則會根據遠程版本檢查每個檔案。 然後，第二字母指定更新操作將執行哪些操作。

#### 語法 {#syntax-4}

```shell
status -v|-q|-u|-N <file1> [<file2> ...]
```

#### 選項 {#options-4}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `-u (--show-update)` | 顯示更新資訊 |
| `-N (--non-recursive)` | 在單個目錄上運行 |
| `<file> [<file> ...]` | 顯示狀態的檔案或目錄 |

### 更新 {#update}

將更改從儲存庫複製到工作副本中。

#### 語法 {#syntax-5}

```shell
update -v|-q|--force|-N <file1> [<file2> ...]
```

#### 選項 {#options-5}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `--force` | 強制覆寫本機檔案 |
| `-N (--non-recursive)` | 在單個目錄上運行 |
| `<file> [<file> ...]` | 要更新的檔案或目錄 |

### 資訊 {#info}

顯示有關本機檔案的資訊。

#### 語法 {#syntax-6}

```shell
info -v|-q|-R <file1> [<file2> ...]
```

#### 選項 {#options-6}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `-R (--recursive)` | 運算遞歸 |
| `<file> [<file> ...]` | 顯示資訊的檔案或目錄 |

### 提交 {#commit}

將工作副本中的更改發送到儲存庫。

#### 語法 {#syntax-7}

```shell
commit -v|-q|--force|-N <file1> [<file2> ...]
```

#### 選項 {#options-7}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `--force` | 即使修改了遠程副本，也強制提交 |
| `-N (--non-recursive)` | 在單個目錄上運行 |
| `<file> [<file> ...]` | 提交檔案或目錄 |

### 回復 {#revert}

將工作副本檔案還原為原始狀態，並取消大部分的本機編輯。

#### 語法 {#syntax-8}

```shell
revert -q|-R <file1> [<file2> ...]
```

#### 選項 {#options-8}

|  |  |
|--- |--- |
| `-q (--quiet)` | 打印盡可能少 |
| `-R (--recursive)` | 遞歸降階 |
| `<file> [<file> ...]` | 提交檔案或目錄 |

### 已解決 {#resolved}

刪除 **工作副本** 檔案或目錄上的衝突狀態。

>[!NOTE]
>
>該命令不會在語義上解決衝突或刪除衝突標籤；它只會刪除與衝突相關的對象檔案，並允許再次提交PATH。

#### 語法 {#syntax-9}

```shell
resolved -q|-R|--force <file1> [<file2> ...]  
```

#### 選項 {#options-9}

|  |  |
|--- |--- |
| `-q (--quiet)` | 打印盡可能少 |
| `-R (--recursive)` | 遞歸降階 |
| `--force` | 解析，即使有衝突標籤 |
| `<file> [<file> ...]` | 解析檔案或目錄 |

### 普羅佩 {#propget}

在檔案或目錄上打印屬性的值。

#### 語法 {#syntax-10}

```shell
propget -q|-R <propname> <file1> [<file2> ...]
```

#### 選項 {#options-10}

|  |  |
|--- |--- |
| `-q (--quiet)` | 打印盡可能少 |
| `-R (--recursive)` | 遞歸降階 |
| `<propname>` | 屬性名稱 |
| `<file> [<file> ...]` | 檔案或目錄，以從 |

### Proplist {#proplist}

在檔案或目錄上打印屬性。

#### 語法 {#syntax-11}

```shell
proplist -q|-R <file1> [<file2> ...]
```

#### 選項 {#options-11}

|  |  |
|--- |--- |
| `-q (--quiet)` | 打印盡可能少 |
| `-R (--recursive)` | 遞歸降階 |
| `<file> [<file> ...]` | 檔案或目錄，以列出 |

### Propset {#propset}

在檔案或目錄上設定屬性的值。

>[!NOTE]
>
>VLT可識別下列特殊版本控制屬性：
>
>`vlt:mime-type`
>
>檔案的mimetype。 用於確定是否合併檔案。 以&#39;text/&#39;（或缺少的mimetype）開頭的mimetype會視為文字。 其他任何項目則視為二進位。

#### 語法 {#syntax-12}

```shell
propset -q|-R <propname> <propval> <file1> [<file2> ...]
```

#### 選項 {#options-12}

|  |  |
|--- |--- |
| `-q (--quiet)` | 打印盡可能少 |
| `-R (--recursive)` | 遞歸降階 |
| `<propname>` | 屬性名稱 |
| `<propval>` | 屬性值 |
| `<file> [<file> ...]` | 檔案或目錄，將屬性設定為 |

### 新增 {#add}

將檔案和目錄置於版本控制之下，並安排它們以添加到儲存庫。 將在下次提交時添加它們。

#### 語法 {#syntax-13}

```shell
add -v|-q|-N|--force <file1> [<file2> ...]
```

#### 選項 {#options-13}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `-N (--non-recursive)` | 在單個目錄上運行 |
| `--force` | 迫使行動進行 |
| `<file> [<file> ...]` | 添加本地檔案或目錄 |

### 刪除 {#delete}

從版本控制中移除檔案和目錄。

#### 語法 {#syntax-14}

```shell
delete -v|-q|--force <file1> [<file2> ...]
```

#### 選項 {#options-14}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出 |
| `-q (--quiet)` | 打印盡可能少 |
| `--force` | 迫使行動進行 |
| `<file> [<file> ...]` | 刪除本地檔案或目錄 |

### 差異 {#diff}

顯示兩個路徑之間的差異。

#### 語法 {#syntax-15}

```shell
diff -N <file1> [<file2> ...]
```

#### 選項 {#options-15}

|  |  |
|--- |--- |
| `-N (--non-recursive)` | 在單個目錄上運行 |
| `<file> [<file> ...]` | 顯示 |

### 主控台 {#console}

執行互動式主控台。

#### 語法 {#syntax-16}

```shell
console -F <file>
```

#### 選項 {#options-16}

|  |  |
|--- |--- |
| `-F (--console-settings) <file>` | 指定控制台設定檔案。 預設檔案為console.properties。 |

### Rcp {#rcp}

將一個節點樹從一個遠程儲存庫複製到另一個遠程儲存庫。 `<src>` 指向源節點並指 `<dst>` 定父節點必須存在的目標路徑。 Rcp通過流化資料來處理節點。

#### 語法 {#syntax-17}

```shell
rcp -q|-r|-b <size>|-t <seconds>|-u|-n|-e <arg1> [<arg2> ...] <src> <dst>
```

#### 選項 {#options-17}

|  |  |
|--- |--- |
| `-q (--quiet)` | 盡可能少地打印。 |
| `-r (--recursive)` | 遞歸降。 |
| `-b (--batchSize) <size>` | 中間保存前要處理的節點數。 |
| `-t (--throttle) <seconds>` | 中間儲存後要等待的秒數。 |
| `-u (--update)` | 覆寫／刪除現有節點。 |
| `-n (--newer)` | 請遵守lastModified屬性以進行更新。 |
| `-e (--exclude) <arg> [<arg> ...]` | 排除的源路徑的Regexp。 |
| `<src>` | 源樹的儲存庫地址。 |
| `<dst>` | 目標節點的儲存庫地址。 |

#### 範例 {#examples-3}

```shell
vlt rcp http://localhost:4502/crx/-/jcr:root/content  https://admin:admin@localhost:4503/crx/-/jcr:root/content_copy  
```

>[!NOTE]
>
>在 `--exclude` 和參數之前，選項後面必須加上另 `<src>` 一個選 `<dst>` 項。 例如：
>
>`vlt rcp -e ".*\.txt" -r`

### 同步 {#sync}

允許控制保險儲存同步服務。 如果沒有任何引數，此命令將嘗試將當前工作目錄置於同步控制下。 如果在vlt結帳中執行，則會使用各自的篩選器和主機來設定同步。 如果在vlt檢出外執行，則僅當目錄為空時，才會註冊當前資料夾以進行同步。

#### 語法 {#syntax-18}

```shell
sync -v|--force|-u <uri> <command> <localPath>
```

#### 選項 {#options-18}

|  |  |
|--- |--- |
| `-v (--verbose)` | 詳細輸出。 |
| `--force` | 強制執行某些命令。 |
| `-u (--uri) <uri>` | 指定同步主機的URI。 |
| `<command>` | sync命令執行。 |
| `<localPath>` | 要同步的本機資料夾。 |

### 狀態代碼 {#status-codes}

VLT使用的狀態代碼為：

* &#39; &#39;無修改
* 已新增&#39;A&#39;
* &#39;C&#39;衝突
* &#39;D&#39;已刪除
* &#39;I&#39;已忽略
* &#39;M&#39;已修改
* &#39;R&#39;已取代
* &#39;?&#39; 項目不在版本控制之下
* &#39;!&#39; 項目遺失（由非svn命令移除）或不完整
* 「~」版本化項目被不同類型的項目阻擋

## 設定FileVault同步 {#setting-up-filevault-sync}

儲存庫同步服務用於將儲存庫內容與本地檔案系統表示同步，反之亦然。 這是通過安裝OSGi服務來實現的，該服務將監聽儲存庫更改並將定期掃描檔案系統內容。 它使用與儲存庫相同的序列化格式將儲存庫內容映射到磁碟。

>[!NOTE]
>
>保險儲存同步服務是一種開發工具，非常不鼓勵在生產系統上使用它。 另請注意，服務只能與本地檔案系統同步，不能用於遠程開發。

### 使用vlt安裝服務 {#installing-the-service-using-vlt}

此命 `vlt sync install` 令可用於自動安裝保險儲存同步服務捆綁和配置。

The bundle is installed below `/libs/crx/vault/install` and the config node is created at `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`. 服務最初是啟用的，但未配置同步根。

下面的示例將同步服務安裝到給定URI可訪問的CRX實例。

```shell
$ vlt --credentials admin:admin sync --uri http://localhost:4502/crx install
```

### 顯示服務狀態 {#displaying-the-service-status}

該命 `status` 令可用於顯示有關正在運行的同步服務的資訊。&quot;

```shell
$ vlt sync status --uri http://localhost:4502/crx
Connecting via JCR remoting to http://localhost:4502/crx/server
Listing sync status for http://localhost:4502/crx/server/-/jcr:root
- Sync service is enabled.
- No sync directories configured.
```

>[!NOTE]
>
>該命 `status` 令不會從服務中提取任何即時資料，而是讀取位於的配置 `/libs/crx/vault/com.day.jcr.sync.impl.VaultSyncServiceImpl`。

### 添加同步資料夾 {#adding-a-sync-folder}

該 `register` 命令用於添加要與配置同步的資料夾。

```shell
$ vlt sync register
Connecting via JCR remoting to http://localhost:4502/crx/server
Added new sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>在配 `register` 置配置之前，命令不會觸發同 `sync-once` 步。

### 刪除同步資料夾 {#removing-a-sync-folder}

該 `unregister` 命令用於從配置中刪除要同步的資料夾。

```shell
$  vlt sync unregister
Connecting via JCR remoting to http://localhost:4502/crx/server
Removed sync directory: /tmp/workspace/vltsync/jcr_root
```

>[!NOTE]
>
>您必須先註銷同步資料夾，然後才能刪除該資料夾本身。

### 配置同步 {#configuring-synchronization}

#### Service configuration {#service-configuration}

在服務運行後，可以使用以下參數對其進行配置：

* `vault.sync.syncroots`:定義同步根的一個或多個本地檔案系統路徑。

* `vault.sync.fscheckinterval`:應掃描其檔案系統以進行更改的頻率（以秒為單位）。 預設值為5秒。
* `vault.sync.enabled`:啟用／禁用服務的常規標誌。

>[!NOTE]
>
>服務可以使用Web控制台或儲存庫中 `sling:OsgiConfig` 的節點(使用 `com.day.jcr.sync.impl.VaultSyncServiceImpl`名稱)進行配置。
>
>使用AEM時，有幾種方法可管理此類服務的組態設定；如需 [完整詳細資訊](/help/sites-deploying/configuring-osgi.md) ，請參閱設定OSGi。

#### 同步資料夾設定 {#sync-folder-configuration}

每個同步資料夾都將配置和狀態儲存在三個檔案中：

* `.vlt-sync-config.properties`:配置檔案。

* `.vlt-sync.log`:包含同步期間所執行操作相關資訊的記錄檔。
* `.vlt-sync-filter.xml`:篩選器，用於定義同步的儲存庫的哪些部分。 此檔案的格式由「執行已過濾的 [檢出」部分描述](#performing-a-filtered-checkout) 。

該 `.vlt-sync-config.properties` 檔案允許您配置以下屬性：

**禁用** ：開啟或關閉同步。 預設情況下，此參數設定為false以允許同步。

**sync-once** 如果非空，下次掃描將按給定方向同步資料夾，則會清除參數。 支援兩個值：

* `JCR2FS`:將JCR儲存庫中的所有內容導出並寫入本地磁碟。
* `FS2JCR`:將所有內容從磁碟導入JCR儲存庫。

**sync-log** 定義日誌檔案名。 依預設，值為。vlt-sync.log

### 使用VLT同步進行開發 {#using-vlt-sync-for-development}

要根據同步資料夾設定開發環境，請按如下步驟操作：

1. 使用vlt命令行簽出儲存庫：

   ```shell
   $ vlt --credentials admin:admin co --force http://localhost:4502/crx dev
   ```

   >[!NOTE]
   >
   >您可以使用篩選器來僅結帳適當的路徑。 如需詳細 [資訊，請參閱執行篩選的結帳](#performing-a-filtered-checkout) 一節。

1. 轉至工作副本的根資料夾：

   ```shell
   $ cd dev/jcr_root/
   ```

1. 將同步服務安裝到您的儲存庫：

   ```xml
   $ vlt sync install
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Preparing to install vault-sync-2.4.24.jar...
   Updated bundle: vault-sync-2.4.24.jar
   Created new config at /libs/crx/vault/config/com.day.jcr.sync.impl.VaultSyncServiceImpl
   ```

1. 初始化同步服務：

   ```shell
   $ vlt sync
   Connecting via JCR remoting to http://localhost:4502/crx/server
   Starting initialization of sync service in existing vlt checkout /Users/colligno/Applications/cq5/vltsync/sandbox/dev/jcr_root for http://localhost:4502/crx/server/-/jcr:root
   Added new sync directory: /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root
   
   The directory /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root is now enabled for syncing.
   You might perform a 'sync-once' by setting the
   appropriate flag in the /Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/.vlt-sync-config.properties file.
   ```

1. 編輯隱 `.vlt-sync-config.properties` 藏的檔案並配置同步以同步儲存庫的內容：

   ```xml
   sync-once=JCR2FS
   ```

   >[!NOTE]
   >
   >此步驟會根據您的篩選器配置下載整個儲存庫。

1. 檢查日誌檔案 `.vlt-sync.log` 以查看進度：

   ```xml
   ***
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/
   30.04.2017 14:39:10 A file:///Users/trushton/Applications/aem/vltsync/sandbox/dev/jcr_root/apps/geometrixx-outdoors/src/core/src/main/java/info/geometrixx/outdoors/core/product/GeoProduct.java
   ***
   ```

您的本地資料夾現在與儲存庫同步。 同步是雙向的，因此從儲存庫進行的修改將應用於本地同步資料夾，反之亦然。

>[!NOTE]
>
>VLT同步功能僅支援簡單檔案和資料夾，但檢測特殊的電子倉庫序列化檔案（.content.xml、dialog.xml等），並以無提示方式忽略它們。 因此，可在預設vlt結帳時使用vault同步。
