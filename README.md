# GraphCMSオンラインストア

GraphCMS, Next.js, Stripe, Tailwind CSSを使って、モダンでSEO対策済みのオンラインストアを構築できます。

このスターターは、バックエンドにGraphCMSとStripe、フロントにNext.jsを使用した、完全に機能するショッピングサイトのサンプルです。実際に動作しているデモは[こちら](https://commerce.withheadlesscms.com/)でご覧いただけます。

## 機能

- [GraphCMS ローカライゼーション](https://graphcms.com/content-localization)と[Next.js](https://nextjs.org/docs/advanced-features/i18n-routing)で完全にローカライズした製品カタログ
- [`getStaticProps`](https://nextjs.org/docs/basic-features/data-fetching#getstaticprops-static-generation)と[`getStaticPaths`](https://nextjs.org/docs/basic-features/data-fetching#getstaticpaths-static-generation)により、プレレンダリングしたカタログページ
- [SWR](https://swr.vercel.app)で動的にクライアントサイドのデータ取得
- [`react-use-cart`](https://github.com/notrab/react-use-cart)を使ってショッピングカートをローカライズ
- [Stripe Checkout](https://stripe.com/jp/docs/payments/checkout)を使って、ホストによるチェックアウトと支払いフロー
- [GraphCMS mutation API](https://graphcms.com/mutation-api) と [API Routes](https://nextjs.org/docs/api-routes/introduction) を使って、チェックアウトが成功したときに注文を作成（Webhook経由）
- 複数の通貨をサポート

## 使用方法

> このリファレンスアプリケーションには、Stripeアカウントが必要です

1. [`degit`](https://github.com/Rich-Harris/degit)でリポジトリをクローンし、プロジェクトの依存関係をインストールします。

```
npx degit GraphCMS/graphcms-commerce-starter#main graphcms-commerce-starter
cd graphcms-commerce-starter
yarn
```

2. `Commerce Starter` テンプレートを使って、新しい GraphCMS プロジェクトを作成します。

3. `.env.sample` をクローンして `.env` ファイルを追加し、必要な変数値を指定します。

> GraphCMSの[auth tokens](https://graphcms.com/docs/authorization#permanent-auth-tokens)を別途作成して、データの照会や変更を行うことをお勧めします。

```
graphcms_mutation_token=
next_public_graphcms_token=
next_public_graphcms_url=
next_public_stripe_publishable_key=
stripe_secret_key=
```

4. [Stripe webhook](https://stripe.com/docs/payments/handling-payment-events)を`checkout.session.completed`イベントを設定し、mutation APIを介してGraphCMSのフルフィルメントを有効にします。

5. 必要に応じて、[`graphcms.config.js`](graphcms.config.js)で、より多くのロケールや通貨のサポートを設定します。詳しくは[こちら](#設定)をご覧ください。

6. `yarn dev` を実行します。

## 設定
<div id="設定" />

プロジェクトがサポートするロケールや通貨の設定は、[`graphcms.config.js`](graphcms.config.js)で管理します。

> `locales`の配列に、GraphCMSプロジェクトで有効になっているロケールが反映されていることが重要です。

```js
module.exports = {
  locales: [
    {
      value: 'en',
      label: 'English',
      default: true
    },
    {
      value: 'de',
      label: 'German'
    }
  ],
  currencies: [
    {
      code: 'GBP',
      default: true
    },
    {
      code: 'EUR'
    }
  ]
}
``` 

## ライセンス

オリジナルのコードと同様にMTIライセンスを採用しています。

https://github.com/btahir/next-shopify-starter

## 注意事項

コード自体のローカライズはWIPです。また、準備でき次第公開して参ります。
