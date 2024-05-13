# 課題3：Azureでアプリケーションを動かしてみよう

⏲️ _完了までの時間: 60 min._ ⏲️

## このパートで学ぶこと 🎯

- GitHub Actionsを始めましょう
- MilligramアプリケーションのフロントエンドをGitHub Pagesで公開します
- AzureでPython Webアプリを実行します
- GitHub ActionsでAzureにMilligramアプリケーションのバックエンドをデプロイします

## 目次

- [課題3：Azureでアプリケーションを動かしてみよう](#課題3azureでアプリケーションを動かしてみよう)
  - [このパートで学ぶこと 🎯](#このパートで学ぶこと-)
  - [目次](#目次)
    - [参考情報](#参考情報)
  - [Milligramアプリケーションフロントエンド](#milligramアプリケーションフロントエンド)
    - [GitHub Actions を有効にします](#github-actions-を有効にします)
    - [GitHub Actionsを実行します](#github-actionsを実行します)
    - [プロジェクト設定でGitHub Pagesを有効にします](#プロジェクト設定でgithub-pagesを有効にします)
    - [スマートフォンでMilligramアプリケーションを開きます](#スマートフォンでmilligramアプリケーションを開きます)
    - [ホーム画面にアプリケーションを追加します](#ホーム画面にアプリケーションを追加します)
  - [Milligramアプリケーションバックエンド](#milligramアプリケーションバックエンド)
    - [Azureにログインします](#azureにログインします)
    - [Azure Storage Accountを作成します](#azure-storage-accountを作成します)
    - [コンテナレジストリを作成します](#コンテナレジストリを作成します)
    - [Webアプリを作成します](#webアプリを作成します)
    - [Azure Container Appsの設定変更](#azure-container-appsの設定変更)
    - [GitHub Actionsを使ってMilligramアプリのバックエンドのコードをAzure Webアプリにデプロイします](#github-actionsを使ってmilligramアプリのバックエンドのコードをazure-webアプリにデプロイします)
    - [Milligramアプリが正しく実行されているかどうかを確認しよう](#milligramアプリが正しく実行されているかどうかを確認しよう)
    - [GitHub SecretsにAzure WebアプリURLを連携します](#github-secretsにazure-webアプリurlを連携します)
    - [フロントエンドパイプラインをもう一度実行します](#フロントエンドパイプラインをもう一度実行します)
    - [Milligramアプリケーションを開く](#milligramアプリケーションを開く)

### 参考情報

- [GitHub Actionsとは?](https://github.com/features/actions)
- [GitHub Actions ドキュメント](https://docs.github.com/actions)
- [リポジトリとは?](https://docs.github.com/github/creating-cloning-and-archiving-repositories/creating-a-repository-on-github/about-repositories)
- [Resource / Resource Group / Subscription とは?](https://docs.microsoft.com/azure/cloud-adoption-framework/govern/resource-consistency/resource-access-management)


## Milligramアプリケーションフロントエンド

まず、フロントエンドアプリケーション(スマートフォンまたはWebブラウザーで表示される部分)から始めましょう。

<details>
<summary>フロントエンドとは？</summary>

シンプルな車を想像してみましょう。あなたが見えるものすべて - 座席、屋根、床、ユーザーインターフェイス（ダッシュボード、ステアリングホイールなど） - アプリケーションではそれらを**frontend** と呼びます。

次にボンネットを開きます。エンジン、トランスミッション、その他の要素を見ることができます。 アプリケーションではこれらが **backend** や **API** です。

つまり **frontend** は、ユーザーが**API** を介して**backend** に指示を提供するものです。それは、車のペタルを踏むと、エンジンが加速するのとよく似ています。

</details>

### GitHub Actions を有効にします

GitHubには、Webサイトを作成する機能 **「GitHub Pages」** および更新を自動化する機能 **「GitHub Actions」** があります。

1. ブラウザでGitHubリポジトリを開き **[Actions]** タブに移動します

2. **[_I understand my workflows, go ahead and enable them_]** と書かれたボタンをクリックして、先に進み、GitHubアクションを有効にします

![Enable GitHub Actions](./images/EnableGithubActions.png)


<!-- ::: tip サンプルのリポジトリ
[repository](https://docs.github.com/github/creating-cloning-and-archiving-repositories/creating-a-repository-on-github/about-repositories)にすべてのプロジェクトのファイルと各ファイルのファイルが含まれています。
::: -->


ここで、**GitHub Actions** に読み取り/書き込み許可があることを確認してください。GitHubリポジトリの **[Settings]** -> **[Actions]** -> **[General]** をクリックし、**_WorkFlow Permissions_** セクションまでスクロールします。 **_read and write permissions_** オプションをクリックして、**[save]** ボタンをクリックします。

![Check Settings](./images/gh-actions-read-ex1.png)
![Check Settings](./images/gh-actions-read.png)


### GitHub Actionsを実行します

1. リポジトリの **[Actions]** タブで、**[pages]** ワークフローをクリックします。
   
2. **[Run Workflow]** ドロップダウンを開き、**[Run Workflow]** ボタンをクリックして、ワークフローの実行を確認します。

次に、ワークフローがどのように実行されているかを観察し、GitHubが実行する流れを見てみましょう。

![Run workflow](./images/FrontendRunWorkflow.png)


### プロジェクト設定でGitHub Pagesを有効にします

GitHub Actionsを使用して構築および展開したWebサイトを表示できるようにするには、リポジトリに対してGitHub Pagesを有効にする必要があります。GitHub Pages は、リポジトリに関連する静的Webサイトを簡単に表示する機能です。

GitHub Pages はプロジェクトのドキュメントを作成するのによく使われます。Milligramアプリケーションのフロントエンドを提供するために使用します。


1. **[repository settings]** に移動します 

2. **[Pages]** に移動し、ブランチ `gh-pages` を選択し、**[Save]** ボタンをクリックします。
  ![Enable Pages](./images/FrontendPagesUpdated.png)

 デプロイには1〜2分かかります。その後、Milligramアプリケーションは次のURLで確認できます。

 `
 https://<ご自身のGitHubアカウント名>.github.io/everyonecancode/
 `
 
ブラウザを開いてウェブサイトを確認します。プロファイルをご自身のGitHubアカウント名に変更してみて、プロフィール写真が変更されていることを確認してください。


### スマートフォンでMilligramアプリケーションを開きます

Milligramアプリケーションは、あなたがよく知っているかもしれない写真ベースのソーシャルメディアに似た楽しいアプリです。もちろん、スマートフォンでカメラを使用して写真を撮って投稿できます。

その主な機能は次のとおりです。

- あなた自身のプロフィールからGitHubアカウント情報を表示する
- 写真を撮って画像を表示する
- 写真の画像内のオブジェクトを検出し、画像の説明を作成する
-  Azure Speech Serviceを使用してマイクで話した内容を文字に起こしする

アプリは動くようになりましたが、まだストレージやデータベースはありません。そのため、データを保存できません。そこで次のステップでこれらをインストールします。

最初の変更を行うには、スマートフォンでMilligramアプリケーションを開き、コンテンツを探索します。次に、アプリのプロファイルを編集して、アプリに独自のGitHubプロファイル写真を表示します。

![Add to homescreen 1](./images/FrontendHomescreen0.jpg)


### ホーム画面にアプリケーションを追加します

最新のスマートフォンでは、ホーム画面にWebアプリを「インストール」して、よりアクセスしやすくし、公式アプリのように見せることができます。したがって、アプリをスマートフォンのホーム画面に追加することはありません。

- ブラウザメニューを開いて、ホーム画面にWebサイトを追加します。
  - iOSの場合:
    ![Add to homescreen ios](./images/FrontendHomescreen1.jpg)
  - Androidの場合:
    ![Add to homescreen Android](./images/android/FrontendHomescreen2.jpg)

これで、スマートフォンのホーム画面からアプリのようにウェブサイトを開くことができます。


## Milligramアプリケーションバックエンド

アプリケーションは、フロントエンド（スマートフォンで表示されるもの）とバックエンド（情報を処理するもの）に分割できます。この場合、独自のソーシャルメディアアプリケーションを作成したいため、「ニュースフィード」のために写真を保存する必要があります。つまり、多くのファイルを保存する場所と、アプリケーションロジック（プログラミングコード）を実行する場所が必要です。

アプリケーションバックエンドは、アップロードされた写真を受け取り、それらを保存し、必要に応じて返します。

今回は、ファイルを保存するために、**[Azure Storage Account](https://learn.microsoft.com/ja-jp/azure/storage/common/storage-account-overview)** を使用し、アプリケーションロジックを実行するには、 **[Azure Container Apps](https://azure.microsoft.com/ja-jp/products/container-apps)** を使用します。


### Azureにログインします

ブラウザで[portal.azure.com](https://ms.portal.azure.com/?l=en.en-us#home)にアクセスしてください。

コーチから提供された **Azureアカウント** でログインします。わからない場合は遠慮なく質問してください。

![Log In Azure](./images/light/LogInAzure.png)


### Azure Storage Accountを作成します

Azure Storage Accountは、ニュースフィードの写真を「保存」する場所です。

ストレージアカウント内では、[Azure Blob Storage](https://learn.microsoft.com/en-us/azure/storage/blobs/)を使用します。Azure Blob Storageには、膨大な量のファイルを保持できます。

Azure Blob Storageには好きなだけ多くの写真を保存でき、ストレージスペースを心配する必要がありません。


::: tip Azure Resource
Azureの世界では、「リソース」はAzureが管理するエンティティを指します。たとえば、仮想マシン、仮想ネットワーク、およびストレージアカウントはすべてAzureリソースと呼ばれます。
:::

::: tip Azure Resource Group
リソースグループは、Azureソリューションに関連するリソースを保持するコンテナです。リソースグループには、ソリューション用のすべてのリソース、またはグループとして管理したいリソースのみを含めることができます。
:::

1. Azureポータルのホームページに移動します。
2. **[+ Create a resource]** をクリックしてリソースを作成します。
3. **[Storage Account]**(日本語の場合は「ストレージ アカウント」) を検索し、**[Create]** ボタンをクリックします。
   
  ![](./images/create-storage.png)

   + Azureポータルにログインするために使用した名前で、サブスクリプションとリソースグループを選択します。
   + Azureストレージアカウントの名前はグローバルで一意である必要があります。また、小文字と特殊文字は使用できません。
   + **`Locally-redundant storage (LRS)`** と **`Standard`** を選択してください。
    ![Storage](./images/light/BackendStorage1.png)

4  **[review]** をクリックし、その後 **[create]** をクリックしてストレージアカウントを作成します。

5. ストレージアカウントが作成されたら、**[Go to resource]** ボタンをクリックして、リソースに移動します。

6. これで、ストレージアカウントが表示されます。次に画像を入れるためのコンテナを作ります。左側の **[Containers]** を選択します。
7. **[new container]** ボタンをクリックして、 **`images`** という名前のコンテナを作成します。その他はデフォルトのままで問題ありません。
  ![](./images/blob-container.png)
  
  ここで作成した **`images`**  というコンテナは、Milligramアプリケーションからアップロードされた画像が保存される場所です。

8. ストレージサービスの場所とキー情報を確認します。ストレージアカウントを検索することで作成したリソースを表示します。
   
   ストレージにアクセスするためのキーは **`Access Keys`**、 接続文字列は **`Connection String`** で確認できます。値を見るときは **[ShowKeys👀]** ボタンをおすと、その値をクリップボードにコピーできます。
![Screenshot of Access key page in Azure portal](./images/light/SecretAccessKeys.png)

この接続情報`Connection String`は、後でコンテナアプリケーションに追加する必要があるので、ひかえておいてください。

### コンテナレジストリを作成します

[Azure Container Registry](https://azure.microsoft.com/ja-jp/products/container-apps)は、Microsoftが管理するコンテナレジストリサービスです。コンテナイメージの管理ができます。

1. Azureポータルのホームページにもう一度移動します。
2. **[+ Create a resource]** をクリックして、以前と同じようにリソースを作成します。

3. **「Azure Container Registry」** をクリックします。

4. サブスクリプションとリソースグループを選択し、以下のとおり設定してください。
  
    - Registry Name: `everyonecancodeあなたの名前`
    - Location: `West Europe`
    - Pricing plan: `Standard`

5. 画面の下部にある **[review + create]** ボタンをクリックします。
6. 表示されている情報を確認し、次の画面で **[create]** をクリックしコンテナレジストリを作成します。


### Webアプリを作成します

[Azure Container Apps](https://azure.microsoft.com/ja-jp/products/container-apps)は、Microsoftが管理するコンピューターで、ソフトウェアの更新を心配することなく簡単に独自のコンテナアプリケーションを実行できる便利なサービスです。

1. Azureポータルのホームページにもう一度移動します。
2. **[+ Create a resource]** をクリックして、以前と同じようにリソースを作成します。

3. **「Azure Container Apps」** (コンテナー アプリ)をクリックします。

4. サブスクリプションとリソースグループを選択し、以下のとおり設定してください。
  
    - Container Apps Name: `everyonecancode-あなたの名前`
    - Region: `West Europe`

5. **[Next: Container]** ボタンをクリックします。 
6. クイックスタートイメージを使用するのチェックを外し、イメージソースとしてAzure Container Registryを選択します。

![](./images/container-apps1.png)


7. 環境変数に以下の値を設定します。

  | Name | Value |
  |-|-|
  | `CUSTOMCONNSTR_STORAGE` | `DefaultEndpointsProtocol=https;AccountName=xxx;AccountKey=xxx;EndpointSuffix=xxx` |
  
![](./images/container-apps2.png)

8. **[バインド]** はデフォルトのままで問題ありません。

9. 次に **[イングレス]** の設定をします。イングレスを有効にする、にチェックを入れ、以下のように設定します。
  ![](./images/ingress1.png)
  ![](./images/ingress2.png)

10. 画面の下部にある **[review + create]** ボタンをクリックします。

11.  表示されている情報を確認し、次の画面で **[create]** をクリックしContainer Appsを作成します。


### Azure Container Appsの設定変更

Azureポータルで作成したContainer Appsの左側メニューにある **[CORS]**  タブまでスクロールし、 「許可された配信元」に`https://<ご自身のGitHubアカウント名>.github.io` を入力します。 **[適用]**  ボタンをクリックして設定完了です。

![](./images/cors.png)


### GitHub Actionsを使ってMilligramアプリのバックエンドのコードをAzure Webアプリにデプロイします

ソーシャルメディアアプリケーションが実際に何かを実行できるようにするには、ソースコードをAzure Webアプリに持ち込む必要があります。

そのために、この **「デプロイ」** と呼ばれる作業をGitHub Actionsで自動します。アプリケーションに変更を加える(たとえば、アプリケーションのタイトルを変更するなど)するたびに手動でなにかをする必要はありません。

1. AzureポータルのAzure Container Appsの左側にある **[継続的デプロイ]** タブに移動します。

2.  **[settings]** タブの下で **_source_** として **`github`** を選択し、**[authorize]** をクリックします。

3.  **_organization_** でGitHubのアカウント名を選択し、**_repository_** で`everyonecancode`と`main`ブランチを選択します。
   
4.  **[Save]** ボタンを押すと、サービスはGitHubリポジトリにワークフローファイルを自動的に作成します。

このワークフローはすぐに実行され、約5分後にはコンテナアプリの準備が整います。

GitHubリポジトリの **[Actions]** タブから進捗を確認す​​ることもできます。緑色のアイコンは問題なく進んでいることを表しています。

![GitHub Actions status](./images/actions-status.png)

### Milligramアプリが正しく実行されているかどうかを確認しよう

問題なくデプロイできていることを確認するには、アプリのフロントエンドがバックエンドサービスから応答を取得するかどうかをテストします。

すべてをまとめる前に、バックエンドサービスが期待どおりに機能していることを確認したいと考えています。

1. Azure ポータルからAzure Container Appsの左側の **[Overview]** タブに移動します。

![](./images/defaultdomain-ex.png)
  
  **アプリケーション URL** のURLの後ろに`/docs`を追加し、インタラクティブなドキュメントを使用してWebサイトをテストして、MilligramアプリケーションのAPIが動作するかどうかを確認します。

  `https://xxx.xxx.westeurope.azurecontainerapps.io/docs`

  ブラウザでは、次のように見えるはずです。**_GET/images_** エンドポイントを選択し、**[Try it Out]** をクリックして **[Execute]** をクリックします。200番の応答コードが返ってくると、正しく動いていることが確認できます。おめでとうございます！

  ![Test API Page1](./images/TestAPIGetImages-ex1.png)
  ![Test API Page2](./images/TestAPIGetImages-ex2.png)
  ![Test API Page3](./images/TestAPIGetImages-ex3.png)

  :::tip
  OpenAPI についてさらに知りたいときは [Wikipedia](<https://en.wikipedia.org/wiki/OpenAPI_(software)>)を参考にしてください。
  :::

 

  :::tip
  [Wikipedia](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)のHTTP応答コードを見てください。2xxコードは一般に成功を意味し、4xxおよび5xxコードはさまざまな種類のエラーを示します。あなたはおそらく404をみたことがあるでしょう。これは「ページが見つかりません」という意味になります。
  :::

<!-- ### 振り返り！私たちはこれまで何をしましたか？

おめでとうございます、あなたはあなたのWebアプリケーションにバックエンドを展開しました！これまでに行ったことを要約しましょう。

まず、GitHubページを使用してWebアプリのFrontend（ユーザーインターフェイス）を展開しました。これは、GitHub Pagesに行くときに表示されるものです。フロントエンドは、画像を提供してロジックを実行するためにサーバーを必要としていました。これがAzure部品が入った場所です。最初に、ストレージリソースを作成しました。これは画像を保存する責任があります。次に、Webアプリリソースを作成しました。ここでは、サーバーロジックを実行します。サーバーロジックは、FastAPIと呼ばれるフレームワークを使用してPythonで記述されています。サーバーロジックコードは、EveryOneCancode GitHubリポジトリでホストされています。WebアプリをGitHubリポジトリに接続し、Webアプリを起動すると特定のコマンドを実行するようにサーバーに指示しました。このコマンドはサーバーロジックの実行を開始します。これが、「/docs」の下でブラウザ内のドキュメントを見ることができる理由です。次に、フロントエンドをバックエンドに接続しましょう。 -->

### GitHub SecretsにAzure WebアプリURLを連携します

これでバックエンドサービスが問題なく機能することを確認できたので、バックエンドとフロントエンドすべてをまとめることができます。

ここで、**GitHub Secrets** というGitHubの機能を使用します。ここでは、フロントエンドアプリから呼び出すバックエンドアプリのURLをシークレットとして登録します。

1. ブラウザからGitHubのリポジトリページを開きます。 **[settings]** を選択し、 **[secrets and variables]** -> **[actions]** に移動します。
 
2.  **_New repository secret_** で **`VITE_IMAGE_API_URL`** と`ご自身のバックエンドのURL `を登録します。
  
::: warning
あなたのURLは `https://xxx.xxx.westeurope.azurecontainerapps.io`となっているはずです。忘れてしまった人は、[「Milligramアプリが正しく実行されているかどうかを確認しよう」](#milligram%E3%82%A2%E3%83%95%E3%82%9A%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%83%8F%E3%82%99%E3%83%83%E3%82%AF%E3%82%A8%E3%83%B3%E3%83%88%E3%82%99)の手順を見返してください。かならず最後に`/` を入れるのを忘れないようにしましょう
:::


  ![GitHub Secrets Create](./images/VITE_IMAGE_API_URL-ex1.png)

### フロントエンドパイプラインをもう一度実行します

フロントエンドで登録したシークレットを追加するには、ビルドパイプラインを再度実行する必要があります。

 1. ブラウザでGitHubのリポジトリを開き、**[Actions]** タブに移動し、**_pages_** ワークフローを選択して、ワークフローを再実行します。
  ![GitHub frontend Workflow](./images/light/RunWorkflowFrontend.png)

  ワークフローの実行をクリックすると、以下の画面が表示されます。
  ![GitHub frontend Workflow Progress](./images/light/FrontendInProgress.png)
  
  問題なく完了すると、次の画面になります。
  ![GitHub frontend Workflow Done](./images/light/FrontendDone.png)

### Milligramアプリケーションを開く 

パイプラインの下にデプロイステップの下に表示されるフロントエンドのURLリンクをクリックするか、スマートフォンでアプリを更新します。

`https://<ご自身のGitHubアカウント名>.github.io/everyonecancode`

フロントエンドアプリケーションには、写真を撮ることができるカメラボタンが表示されます。撮った写真は、タイムラインまたはニュースフィードに表示されるのを確認しましょう。

少なくとも5枚の写真を撮って、それらがあなたのアプリに表示されることを確認してください。彼らがあなたのニュースフィードに写真をアップロードできるように、チーム内のメンバーと共有するようにしてください。

おめてとうございます 🎉

次は私たちはあなたの画像内に何が移っているのかをAIを使って識別したり、マイクを使ってアプリと話すことができるような機能を追加していきます。

::: warning
もしうまく動かなかったチームは サンプルの[Milligramアプリケーション](https://codeunicornmartha.github.io/FemaleAIAppInnovationEcosystem/#/?stack-key=a78e2b9a)で動作を見てください。
:::