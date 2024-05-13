# 課題5:オブジェクト認識

⏲️ _完了までの時間: 30 min._ ⏲️

## このパートで学ぶこと 🎯

- Azure AI servicesを作成します
- Vision APIサービスをアプリと接続します
- GitHub Secrets を使用してAPIキーをアプリに渡します
- アプリでオブジェクト認識の機能が使えるのを確認します

### 参考情報

- [ Resource / Resource Group / Subscription とは](https://docs.microsoft.com/azure/cloud-adoption-framework/govern/resource-consistency/resource-access-management)
- [Vision API](https://azure.microsoft.com/en-us/products/cognitive-services/vision-services/)
- [可用性ゾーンとは](https://docs.microsoft.com/azure/availability-zones/az-overview)
- [GitHub Encrypted secrets](https://docs.GitHub.com/en/actions/reference/encrypted-secrets)


## Azure AI servicesを作成します
1. Azureポータルを開き、以前のチャレンジで作成したリソースグループに移動します。 **Azure AI services** を検索し、新しいリソース作成します。
  
  ![Screenshot of how to create a resource](./images/createresource1.png)

   -  **Azure AI services** を選択し、**[Create]** をクリックします。
   - サブスクリプションとリソースグループは既に設定する必要があります。ここで、リージョンは **「westeurope」** にします。また、**「Standard S0」** を選択します。
  
  ::: danger 注意
  今回のサンプルアプリではハードコードされているので、必ず **westeurope** にリソースを作成してください。
  :::

- リソースにグローバルで一意の名前を付けます。
- **[Review + create]** をクリックし、内容に誤りが無いかを確認したうえで、**[Create]** をクリックしてリソースを作成します。
  ![Screenshot of Azure Portal create page for vision service](./images/createvisionresource.png)

1. リソースが作成された後、**[Keys and Endpoint]** をクリックし、  **`Key`** と **`Endpoint`** をコピーします。これらの値はあとで**GitHub Secrets** に保存するために必要です。値をひかえておいてください。
   ![Screenshot of Access keys in Computer Vision service](./images/copykeys.png)


## Azure AI servicesの資格情報をGitHub Secretに登録します

Azure AI services を利用できるように、このリソースの情報をWebアプリと共有する必要があります。さらに2つのGitHub Secretを作成し、これをアプリと共有します。

ブラウザでGitHubのリポジトリを開きます。**[GitHub] -> [Settings] -> [Secrets] -> [Actions]** に移動し、**[New repository secret]** を追加します。

  次のシークレットを追加します。
  |Name|Value|
  |-|-|
  |VITE_VISION_API_KEY|Azure AI servicesのKey|
  |VITE_VISION_API_ENDPOINT|Azure AI servicesのEndpoint|


![Screenshot of creating secret](./images/action_custom_vision_secret.png)

![Screenshot of creating secret](./images/vision-api-endpoint-secret.png)


## フロントエンドパイプラインを再実行します

フロントエンドで登録したシークレットを追加するには、ビルドパイプラインを再度実行する必要があります。

 1. ブラウザでGitHubのリポジトリを開き、**[Actions]** タブに移動し、**_pages_** ワークフローを選択して、ワークフローを再実行します。
  ![Screenshot of Actions page of github.com/microsoft/everyonecancode](./images/run-workflow.png)

パイプラインの下にデプロイステップの下に表示されるフロントエンドのURLリンクをクリックするか、スマートフォンでアプリを更新します。

`https://<ご自身のGitHubアカウント名>.github.io/everyonecancode`

フロントエンドアプリケーションには、オブジェクト認識のための新しいボタンが表示されます。

::: tip
この機能ではあなたが取った写真や検出されたものは保存されず、タイムラインやニュースフィードに表示されません。
:::

## あなたのアプリは何を検出できましたか？

何枚か写真を撮り、アプリケーションが画像上のオブジェクトを検出できているかを確認しててみましょう。
その精度に驚かれるかもしれません:heart_eyes:

::: warning
もしうまく動かなかったチームは サンプルの[Milligramアプリケーション](https://codeunicornmartha.github.io/FemaleAIAppInnovationEcosystem/#/?stack-key=a78e2b9a)で動作を見てください。
:::

