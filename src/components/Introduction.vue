<template>
  <div class="intro">
      <h3>OpenStickerはMastodon向けのカスタムCSSです</h3>
      <img src="/static/mastodon.png" /><br />
      Faviconを取得します<br />
      <img src="/static/kirishima.png" /><br />
      PleromaやMisskey、PixelFed表示にも対応<br />
      <img src="/static/pleroma.png" /><br />
      <img src="/static/misskey.png" /><br />
      <br />
      <div class="desc">
        OpenStickerは #InstanceTicker に基づいた、
        オープンなカスタムCSSです。インスタンスのデータは
        <a href="https://github.com/cutls/OpenSticker">GitHub</a>
        へのPRにより追加されます。
      </div>
      <h3>リソースURL</h3>
      <ul>
          <li>通常CSS https://s.0px.io/mastodon</li>
          <li>連合のみのCSS https://s.0px.io/mastodon/peers?domain=domain.tld</li>
          <li>JSON https://s.0px.io/json</li>
      </ul>
      <h3>導入(インスタンス管理者)</h3>
      <ul>
        <li>上のジェネレータで作成したものを、管理 > サイト設定 > カスタムCSSに貼り付ける</li>
        <li>CSSのインポートを行いテーマとして提供する(要本体改造。<a href="https://github.com/cutls/mastodon/tree/theme-opensticker">導入例</a>。)</li>
        <li>Reactのコンポーネントとして表示(要本体改造。<a href="https://github.com/cutls/mastodon/tree/opensticker-as-component">導入例</a>。cf: <a href="https://github.com/cutls/os-mastodon-component">Component</a>)</li>
      </ul>
      <h3>導入(一般ユーザ)</h3>
      PC限定で、ユーザースクリプトにより導入することができなくもありませんが、割愛します。
      <h4>Powered by</h4>
      <ul>
        <li>コンテンツ配信: Cloudflare</li>
        <li>画像最適化: images.weserv.nl</li>
        <li>ウェブサーバ: Nginx</li>
        <li>クラウドサービス: OracleCloud</li>
        <li>バックエンド: Deno with TypeScript | json5-deno</li>
        <li>フロントエンド: Vue with JavaScript</li>
        <li>favicon取得API: Node.js with TypeScript | Jimp</li>
        <li>PR鯖缶認証bot(プロプライエタリ): Node.js with JavaScript | GitHub Webhook</li>
      </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      type: 'mastodon',
      instance: '',
      css: ''
    }
  },
  methods: {
    load: async function (event) {
      this.css = 'Loading...'
      if (this.type === 'mastodon') {
        const promise = await fetch('https://s.0px.io/mastodon')
        this.css = await promise.text()
      }
      if (this.type === 'peers') {
        if (this.instance) {
          const promise = await fetch('https://s.0px.io/mastodon/peers?domain=' + this.instance)
          this.css = await promise.text()
        }
      }
    }
  }
}
</script>

<style scoped>
.intro {
    text-align: left;
}
</style>
