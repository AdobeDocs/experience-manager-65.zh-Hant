---
title: 應用程式伺服器安裝的升級步驟
description: 瞭解如何升級通過應用AEM程式伺服器部署的實例。
feature: Upgrading
exl-id: 86dd10ae-7f16-40c8-84b6-91ff2973a523
source-git-commit: c0574b50f3504a4792405d6fcd8aa3a2e8e6c686
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# 應用程式伺服器安裝的升級步驟{#upgrade-steps-for-application-server-installations}

本節介紹為更新Application Server安裝而需要遵循的AEM步驟。

此過程中的所有示例都使用Tomcat作為應用程式伺服器，並暗示您已部署了工作AEM版本。 該過程用於記錄從 **AEM版本6.4至6.5**。

1. 首先，啟動TomCat。 在大多數情況下，您可以通過運行 `./catalina.sh` 啟動啟動指令碼，從終端運行此命令：

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. 如AEM果已部署6.4，請通過訪問以下內容來檢查捆綁包是否正常運行：

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 下一步，取AEM消部署6.4。這可以從TomCat應用管理器(`http://serveraddress:serverport/manager/html`)

1. 現在，使用crx2oak遷移工具遷移儲存庫。 為此，請從以下網站下載最新版本的crx2oak [此位置](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)。

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -jar crx2oak.jar --load-profile segment-fds
   ```

1. 通過執行以下操作，刪除sling.properties檔案中的必要屬性：

   1. 開啟位於 `crx-quickstart/launchpad/sling.properties`
   1. 步驟文本刪除以下屬性並保存檔案：

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. 刪除不再需要的檔案和資料夾。 您需要具體刪除的項目包括：

   * 的 **啟動板/啟動資料夾**。 可以在終端中運行以下命令來刪除它： `rm -rf crx-quickstart/launchpad/startup`

   * 的 **base.jar檔案**: `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * 的 **BootstrapCommandFile_timestamp.txt檔案**: `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * 刪除 **sling.options.file** 通過運行： `find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. 現在，建立將與6.5一起使用的節點儲存和AEM資料儲存。可以通過以下方式建立兩個檔案來執行此操作： `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   這兩個檔案將配AEM置為使用TarMK節點儲存和檔案資料儲存。

1. 編輯配置檔案，使其可供使用。 具體來說：

   * 將以下行添加到 `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

      `customBlobStore=true`

   * 然後將以下行添加到 `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

      ```
      path=./crx-quickstart/repository/datastore
      minRecordLength=4096
      ```

1. 現在，您需要更改6.5戰爭文AEM件中的運行模式。 為此，首先建立一個臨時資料夾，該資料夾將容納6.5AEM戰爭。 此示例中資料夾的名稱將是 `temp`。 複製戰爭檔案後，從臨時資料夾內運行以提取其內容：

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. 內容被提取後，轉到 **WEB-INF** 資料夾和編輯web.xml檔案以更改運行模式。 要查找在XML中設定它們的位置，請查找 `sling.run.modes` 的下界。 找到後，請更改下一行代碼中的運行模式，預設情況下，該代碼設定為作者：

   ```bash
   <param-value >author</param-value>
   ```

1. 更改上述作者值，並將運行模式設定為： `author,crx3,crx3tar`。 最後一個代碼塊應如下所示：

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. 使用已修改的內容重新建立jar:

   ```bash
   jar cvf aem65.war
   ```

1. 最後，在TomCat中部署新的戰爭檔案。
