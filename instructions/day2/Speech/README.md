# 課題6: 音声認識

⏲️ _完了までの時間: 30 min._ ⏲️

## このパートで学ぶこと 🎯

- Azure AI servicesをアプリと接続します
- Pass the API key to you app using GitHub Secrets
- GitHub Secrets を使用してAPIキーをアプリに渡します
- アプリで音声認識の機能が使えるのを確認します

## 目次

### 参考になる情報

- [Resource / Resource Group / Subscription とは](https://docs.microsoft.com/azure/cloud-adoption-framework/govern/resource-consistency/resource-access-management)
- [Speech API](https://azure.microsoft.com/services/cognitive-services/speech-services/#overview)
- [可用性ゾーンとは](https://docs.microsoft.com/azure/availability-zones/az-overview)
- [GitHub Encrypted secrets](https://docs.GitHub.com/en/actions/reference/encrypted-secrets)

## はじめましょう

-  [Vision challenge](../Vision/README.md)で作成したのと同じAzure AI servicesを使用します


## Azure AI servicesの資格情報をGithub Secretに統合します

繰り返しますが、このリソースの情報をWebアプリと共有して、Speech Serviceを利用できるようにする必要があります。したがって、別のGitHub Secretを作成し、これをアプリと共有します。

-  **GitHub -> Settings -> Secrets -> Actions** に移動し、**`New repository secret`** を追加します。
- Name: `VITE_SPEECH_API_KEY`
- Value: Azure AI servicesのキー
- シークレットを追加します。

  ![Screenshot of creating secret](./images/light/vue-app-speech-api-key-secret.png)


## フロントエンドパイプラインを再実行します

- **Actions -> Pages** を開き **Run workflow** に移動します。
  ![Run a workflow](./images/light/runworkflow.png)
  ![Run all jobs](./images/light/rerunalljobs.png)


パイプラインの下にデプロイステップの下に表示されるフロントエンドリンクをクリックします 。
`https://<ご自身のGitHubアカウント名>.github.io/...`
またはスマートフォンでアプリを開きます。

フロントエンドアプリケーションには、英語とドイツ語でアプリと通信し、音声を入力できるマイクボタンが必要です。

※ この機能ではマイクから入力されたデータは保存されず、タイムラインやニュースフィードに表示されません。


## 試してみてください！あなたの音声はテキストに文字起こしされますかか？

アプリになにかを喋ってみて、その内容をテキストで確認してみましょう。
その精度に驚かれるかもしれません😊


デフォルトでは、ドイツ語と英語のみに対応しています。言語を変更したい場合は、**`Frontend` -> `scr` -> `views` -> `Microphone.vue`** を変更します。

例えば追加します。日本語を追加する場合は、以下のように変更します。

```html
<select name="lang" @change="onChange($event)" class="custom-select">
  <option value="de-DE" selected>German</option>
  <option value="en-US">English</option>
  <option value="ja-JP">日本語</option>
</select>
```

設定できる言語は[こちら](https://docs.microsoft.com/en-us/azure/cognitive-services/speech-service/language-support) から確認できます。


※ もしうまく動かなかったチームは サンプルのアプリケーション[Milligram](https://codeunicornmartha.github.io/FemaleAIAppInnovationEcosystem/#/?stack-key=a78e2b9a)で動作を見てください。


### 次は何ですか？

おつかれさまでした！！

今すぐコーディングを開始するか、Udacity、Udemy、PluralSight、EDXなどを使用してAzure認定を試してみてください。

  :::tip
  - [Programming course on Udacity](https://www.udacity.com/course/intro-to-programming-nanodegree--nd000)
  - [Microsoft Azure AI Fundamentals learning path (with optional certification)](https://learn.microsoft.com/en-us/training/paths/get-started-with-artificial-intelligence-on-azure/)
  - [Microsoft Azure Fundamentals learning path (with optional certification)](https://learn.microsoft.com/en-gb/certifications/exams/az-900)
  :::

また、Microsoftのサイトもチェックしてください。

- [Microsoft Aspire Program for early in career hires](https://www.microsoft.com/en-ie/earlycareers/aspire-program)
- Internships at MS
- [Professional Careers at Microsoft](https://careers.microsoft.com/)



[◀ Previous challenge](../Vision/README.md) | [🔼 Home](../../../README.md)
