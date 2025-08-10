<script setup>
import { onMounted, ref } from 'vue'
import { config } from '../config.ts'

// 定义响应式变量
const url = ref('')

onMounted(() => {
  const theme = window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light'
  document.documentElement.classList.remove('dark', 'light')
  document.documentElement.classList.add(theme)

  // 从 URL 参数获取链接
  const urlParams = new URLSearchParams(window.location.search)
  const paramUrl = urlParams.get('url')
  if (paramUrl) {
    url.value = paramUrl
    const el = document.querySelector('div.link')
    if (el) el.textContent = paramUrl
  }
})
</script>

<template>
  <title>未知链接 - {{ config.title }}</title>
  <div class="card-info">
    <img :src="config.favicon" class="avatar" />
    <h1 style="margin-bottom: 0">警告</h1>
    <p>访问未知链接</p>
    <div class="link"></div>
    <p class="tips">
      此链接未通过验证，如果您不知道此链接，请三思后再访问。
      <a class="official" :href="config.defaultLink">点击此处前往 {{ config.linkText }}。</a>
    </p>
    <div class="btns">
      <a href="#" onclick="javascript:history.back(-1);" class="back">返回</a>
      <a :href="url" class="continue">继续</a>
    </div>
  </div>
</template>

<style>
@font-face {
  font-family: 'HYTMR';
  src: url('https://npm.elemecdn.com/fontcdn-ariasaka@1.0.0/HYTangMeiRen55W.woff2');
}

:root {
  --primary: #7287fd;
  --bg: #eff1f5;
  --alt: #e6e9ef;
  --elv: #dce0e8;
  --surface-0: #ccd0da;
  --surface-1: #bcc0cc;
  --surface-2: #acb0be;
  --overlay-0: #9ca0b0;
  --overlay-1: #8c8fa1;
  --overlay-2: #7c7f93;
  --subtext-0: #6c6f85;
  --subtext-1: #5c5f77;
  --text: #4c4f69;
}
:root.dark {
  --primary: #b4befe;
  --bg: #1e1e2e;
  --alt: #181825;
  --elv: #11111b;
  --surface-0: #313244;
  --surface-1: #45475a;
  --surface-2: #585b70;
  --overlay-0: #6c7086;
  --overlay-1: #7f849c;
  --overlay-2: #9399b2;
  --subtext-0: #a6adc8;
  --subtext-1: #bac2de;
  --text: #cdd6f4;
}
body {
  background-color: var(--bg);
  * {
    color: var(--text);
    font-family: 'HYTMR', sans-serif;
    transition: all 0.3s;
  }
}
.card-info {
  width: 500px;
  height: 600px;
  margin: auto;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: var(--alt);
  border-radius: 36px;
  padding: 30px 30px;
  display: flex;
  flex-direction: column;
}
.avatar {
  width: 48px;
  height: 48px;
}
@media screen and (max-width: 650px) {
  .card-info {
    height: -webkit-fill-available;
    width: -webkit-fill-available;
    border-radius: 0px;
  }
}

div.link {
  color: var(--overlay-2);
  border: 1px solid var(--surface-1);
  padding: 18px 24px;
  border-radius: 1rem;
  margin-top: 30px;
}

p.tips {
  color: var(--subtext-0);
  margin-top: 30px;
}

div.btns {
  margin-top: auto;
  display: flex;
  gap: 8px;
}

a.continue {
  flex-grow: 1;
  font-weight: bold;
  background-color: var(--primary);
  color: var(--alt);
  text-decoration: none;
  padding: 10px 20px;
  text-align: center;
  border-radius: 9999em;
  &:hover {
    opacity: .7;
  }
}

a.back {
  flex-grow: 1;
  font-weight: bold;
  background-color: var(--surface-0);
  text-decoration: none;
  padding: 10px 20px;
  text-align: center;
  border-radius: 9999em;
  &:hover {
    opacity: .7;
  }
}

a.official {
  text-decoration: none;
  color: var(--primary);
  &:hover {
    opacity: .7;
  }
}
</style>
