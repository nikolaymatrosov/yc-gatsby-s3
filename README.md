### Как этот репозиторий сделан
```shell
npm install -g gatsby-cli
gatsby new gatsby-site
cd gatsby-site
npm i gatsby-plugin-s3
```

Дальше создаем ключ Статический ключ доступа для Сервисного Аккаунта в Yandex.Cloud.

Затем соответственно инструкциям с сайта плагина [gatsby-s3](https://www.gatsbyjs.com/plugins/gatsby-plugin-s3/#globally) и
с [сайта Облака](https://cloud.yandex.ru/docs/storage/tools/aws-cli) настраиваем консольный клиент к S3.

Дальше я добавил следующий код в секцию `plugins` файла `gatsby-config.js`. Подставить вместо `<bucket-name>` имя вашего бакета.
```js
{
  resolve: 'gatsby-plugin-s3',
  options: {
    bucketName: '<bucket-name>',
    region: 'us-east-1',
    customAwsEndpointHostname: 'storage.yandexcloud.net'
  }
}
```

В `package.json` в секцию `scripts` добавляем `"deploy"`.

```json
{
  "scripts": {
    "deploy": "gatsby-plugin-s3 deploy --yes"
  }
}
```

Всё теперь запускаем и наш сайт будет сбилжен и загружен в бакет.

```shell
npm run build && npm run deploy
```

Не обращайте внимания на вывод в консоли. Там будет указан адрес для AWS S3 несмотря на то какой хост указан в переменной `customAwsEndpointHostname`.
