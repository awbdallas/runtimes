---

copyright:
  years: 2017, 2018
lastupdated: "2018-02-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# 入門指導教學
{: #getting_started}

* {: download} 恭喜，您已在 {{site.data.keyword.Bluemix}} 上部署 Hello World 範例應用程式！若要開始使用，請遵循本逐步手冊。或者，<a class="xref" href="http://bluemix.net" target="_blank" title="（下載範例程式碼）"><img class="hidden" src="../../images/btn_starter-code.svg" alt="下載應用程式碼" />下載範例程式碼</a>，並自行探索。

遵循 Dotnet 入門指導教學，您將設定開發環境、在本端及 {{site.data.keyword.Bluemix}} 上部署應用程式，以及在應用程式中整合 {{site.data.keyword.Bluemix}} 資料庫服務。

## 開始之前
{: #prereqs}

您需要下列各項：
* [{{site.data.keyword.Bluemix_notm}} 帳戶](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git-scm.com/downloads){: new_window}
* 依 [dot.net 網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.microsoft.com/net/download/core) 指示安裝 .NET Core 1.1 SDK 1.0.4。

## 步驟 1：複製範例應用程式
{: #clone}

現在您可以開始使用應用程式。複製儲存庫，並切換至範例應用程式所在的目錄。
  ```
git clone https://github.com/IBM-Bluemix/get-started-aspnet-core
  ```
  {: pre}
  ```
cd get-started-aspnet-core
  ```
  {: pre}

## 步驟 2：在本端執行應用程式
{: #run_locally}

執行應用程式。
  ```
cd src/GetStartedDotnet
  ```
  {: pre}
  ```
dotnet restore
  ```
  {: pre}
  ```
dotnet run
  ```
  {: pre}

在下列網址檢視您的應用程式：http://localhost:5000/

## 步驟 3：準備應用程式以進行部署
{: #prepare}

若要部署至 {{site.data.keyword.Bluemix_notm}}，它有助於設定 manifest.yml 檔案。manifest.yml 包括應用程式的基本資訊（例如名稱、配置給每一個實例的記憶體數量，以及路徑）。我們已在 `get-started-dotnet` 目錄中提供範例 manifest.yml 檔案。

開啟 manifest.yml 檔案，然後將 `name` 從 `GetStartedDotnet` 變更為您的應用程式名稱 <var class="keyword varname" data-hd-keyref="app_name">app_name</var>。
{: download}

  ```
 applications:
 - name: GetStartedDotnet
   random-route: true
   memory: 512M
  ```
  {: codeblock}

在此 manifest.yml 檔案中，**random-route: true** 會為應用程式產生隨機路徑，以防止您的路徑與其他人發生衝突。如果您選擇這樣做，則可以將 **random-route: true** 取代為 **host: myChosenHostName**，並提供您選擇的主機名稱。[進一步瞭解...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 步驟 4：部署應用程式
{: #deploy}

您可以使用 Cloud Foundry CLI 來部署應用程式。

若要開始，請登入您的 {{site.data.keyword.Bluemix_notm}} 帳戶：
  ```
cf login
  ```
  {: pre}

  如果您無法使用 `cf login` 或 `bx login` 指令登入，因為您已有聯合使用者 ID，請使用 `cf login --sso` 或 `bx login --sso` 指令，用您的單一登入 ID 登入。若要進一步瞭解，請參閱[使用聯合 ID 登入](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id)。

選擇您的 API 端點
  ```
cf api <API-endpoint>
  ```
  {: pre}

將指令中的 *API-endpoint* 取代為下列清單中的 API 端點。

| **地區名稱** | **地理位置** | **API 端點** |
|-----------------|-------------------------|-------------------|
| 美國南部地區 | 美國達拉斯 | api.ng.bluemix.net |
| 美國東部地區 | 美國華盛頓州特區 | api.us-east.bluemix.net |
| 英國地區 | 英國倫敦 | api.eu-gb.bluemix.net |
| 雪梨地區 | 澳洲雪梨 | api.au-syd.bluemix.net |
| 德國地區 | 德國法蘭克福 | api.eu-de.bluemix.net |
{: caption="表 1. {{site.data.keyword.cloud_notm}} 地區清單" caption-side="top"}

**請確定您位於應用程式的主要目錄 `get-started-aspnet-core` 中**，然後將應用程式推送至 {{site.data.keyword.Bluemix_notm}}。
  ```
cf push
  ```
  {: pre}

這可能需要一分鐘。如果部署程序發生錯誤，則您可以使用指令 `cf logs <Your-App-Name> --recent` 進行疑難排解。

部署完成之後，您應該會看到一則訊息，指出應用程式正在執行。在 push 指令輸出中所列的 URL 檢視應用程式。您也可以發出 
  ```
cf apps
  ```
  {: pre}
  指令來檢視應用程式狀態，並且查看 URL。



## 步驟 5：連接 MySQL 資料庫
{: connect_mysql}

接下來，我們會將 ClearDB MySQL 資料庫新增至此應用程式並設定應用程式，因此，它可以在本端及 {{site.data.keyword.Bluemix_notm}} 上執行。

1. 在瀏覽器中，登入 {{site.data.keyword.Bluemix_notm}}，並移至「儀表板」。選取**建立資源**。
2. 選擇**資料及分析**區段，然後選取 **ClearDB MySQL** 並建立服務。
3. 移至**連線**視圖並選取應用程式，然後**建立連線**。
4. 系統提示時，請選取**重新編譯打包**。{{site.data.keyword.Bluemix_notm}} 將重新啟動應用程式，並使用 `VCAP_SERVICES` 環境變數將資料庫認證提供給應用程式。只有在應用程式於 {{site.data.keyword.Bluemix_notm}} 上執行時，才能使用此環境變數。

環境變數可讓您分開部署設定與原始碼。例如，您可以將資料庫密碼儲存在原始碼中所參考的環境變數內，而不要將資料庫密碼寫在程式中。[進一步瞭解...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 步驟 6：在本端使用資料庫
{: #use_database}

我們現在即將更新本端程式碼，使其指向此資料庫。我們會將服務的認證儲存在 json 檔中。只有在應用程式於本端執行時，才會使用此檔案。在 {{site.data.keyword.Bluemix_notm}} 中執行時，將會從 VCAP_SERVICES 環境變數中讀取認證。

1. 建立檔案 src/GetStartedDotnet/vcap-local.json

2. 在瀏覽器中，開啟 {{site.data.keyword.Bluemix_notm}} 使用者介面，選取您的應用程式 ->「連線」-> ClearDB Managed MySQL Database ->「檢視認證」

3. 將整個 json 物件從認證複製並貼入 `vcap-local.json` 檔案中，並儲存變更。結果將如下：
  ```
  {
  "cleardb": [
    {
      "credentials": {
        ...
        "uri": "mysql://user:password@some-hostname.cleardb.net:3306/database-name?reconnect=true",
        ...
      },
      ...
      "name": "My ClearDB service instance name",
      ...
    }
  ]
}
  ```

4. 使用	`dotnet run` 指令，從 `get-started-aspnet-core/src/GetStartedDotnet` 目錄中重新啟動您的應用程式。

  重新整理瀏覽器視圖：http://localhost:5000/ 您輸入至應用程式的任何名稱，現在都會新增至資料庫。

  本端應用程式及 {{site.data.keyword.Bluemix_notm}} 應用程式將會共用資料庫。在上述 push 指令輸出中所列的 URL 檢視 {{site.data.keyword.Bluemix_notm}} 應用程式。當您重新整理瀏覽器時，從任一應用程式新增的名稱應該會出現在這兩個應用程式中。

請記住，如果您不需要應用程式維持執行中，請停止它以避免產生任何非預期的費用。
{: tip}

## 後續步驟

* [指導教學](/docs/tutorials/index.html)
* [範例 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://ibm-cloud.github.io){: new_window}
* [架構中心 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/cloud/garage/category/architectures){: new_window}
