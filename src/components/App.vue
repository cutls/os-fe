<template>
  <div>
    <select v-model="type">
      <option value="mastodon">Mastodon向けCSS</option>
      <option value="peers">Mastodon向け連合先だけCSS(peers)</option>
    </select><br />
    <input v-model="instance" v-if="this.type == 'peers'" placeholder="インスタンス名(cutls.comなど)"><br />
    <button v-on:click="load()">読み込む</button><br />
    60KB程度
    <br />
    <textarea v-model="css" /><br />
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
textarea {
  max-width: 500px;
  width: 100%;
  height: 500px;
}
</style>
