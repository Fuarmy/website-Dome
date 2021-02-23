<template>
<header class="app-header">
  <div class="app-header-topbar dk pc-model">
    <div class="app-header-main">
      <nav class="nav top-bar-nav flex">
        <a href="/bibei" class="nav-link" target="_self">装机必备</a>
        <a href="/bibei" class="nav-link" target="_self">提交应用</a>
        <a href="/bibei" class="nav-link" target="_self">RSS订阅</a>
        <a href="/bibei" class="nav-link" target="_self">留言反馈</a>
      </nav>
      <div class="nav justify-content-end mr-5">
        <a class="nav-link pr-2" :class="{active: animation}">
          <i class="mr-1" :class="`icon-${animation?'check':'nocheck'}`"></i>
          动画
        </a>
      </div>
      <nav class="nav justify-content-end">
        <a class="nav-link px-2" :class="{active: theme === 'light'}" @click="changeTheme('light');">
          <i class="mr-1 icon-check" v-if="theme === 'light'"></i>
          明亮
        </a>
        <a class="nav-link px-2" :class="{active: theme === 'retro'}" @click="changeTheme('retro');">
          <i class="mr-1 icon-check" v-if="theme === 'retro'"></i>
          复古
        </a>
        <a class="nav-link px-2" :class="{active: theme === 'eyeshield'}" @click="changeTheme('eyeshield');">
          <i class="mr-1 icon-check" v-if="theme === 'eyeshield'"></i>
          护眼
        </a>
        <a class="nav-link px-2" :class="{active: theme === 'haitian'}" @click="changeTheme('haitian');">
          <i class="mr-1 icon-check" v-if="theme === 'haitian'"></i>
          海天
        </a>
        <a class="nav-link px-2" :class="{active: theme === 'deep'}" @click="changeTheme('deep');">
          <i class="mr-1 icon-check" v-if="theme === 'deep'"></i>
          深邃
        </a>
        <a class="nav-link px-2" :class="{active: theme === 'dark'}" @click="changeTheme('dark');">
          <i class="mr-1 icon-check" v-if="theme === 'dark'"></i>
          暗黑
        </a>
        <a class="nav-link px-2" :class="{active: theme === 'auto'}" @click="changeTheme('auto');">
          <i class="mr-1 icon-check" v-if="theme === 'auto'"></i>
          自动
        </a>
      </nav>
    </div>
  </div>
  <div class="app-header-navbar bg shadow-4 border-bottom pc-model">
    <div class="app-header-main">
      <a href="/" class="app-header-logo active">
        <i class="icon-logo"></i>
        <span>MacFu</span>
      </a>
      <div class="app-header-nav nav flex">
        <a href="/" class="nav-link active" target="_self">首页</a>
        <a href="/" class="nav-link" target="_self">软件</a>
        <a href="/" class="nav-link" target="_self">文章</a>
        <a href="/" class="nav-link" target="_self">专题</a>
        <a href="/" class="nav-link" target="_self">榜单</a>
        <a href="/" class="nav-link" target="_self">优惠正版</a>
      </div>
      <div class="app-header-search">
        <input class="app-header-search__input" type="text" placeholder="请输入关键词搜索软件或文章...">
        <button class="btn search-to">
          <i class="icon-search"></i>
        </button>
      </div>
      <div class="app-header-user">
        <a href="/" class="d-flex align-items-center">
          <i class="icon-wallet mr-3 active"></i>
          <span class="fs-15">打赏</span>
        </a>
      </div>
    </div>
  </div>
</header>
</template>

<script lang="ts">
import { onMounted, onUnmounted, ref, watch } from 'vue';
export default {
  name: 'Header',
  setup() {
    const animation = ref(true);
    const theme = ref('auto');
    const changeTheme = (name: string) => {
      theme.value = name;
    }
    const media = window.matchMedia('(prefers-color-scheme: dark)');
    const callback = (e) => {
      let theme_value = theme.value;
      if (e.matches && theme.value === 'auto') {
        theme_value = 'dark';
      } else if(theme.value === 'auto'){
        theme_value = 'light';
      }
      document.getElementsByTagName("body")[0].className = theme_value;
    }
    // 监听 ref
    watch(theme, (newVal, oldVal) => {
      callback(media);
    })
    onMounted(() => {
      if (typeof media.addEventListener === 'function') {
        media.addEventListener('change', callback);
      } else if (typeof media.addListener === 'function') {
        media.addListener(callback);
      }
      callback(media);
    });
    onUnmounted(()=> {
      document.body.removeAttribute("class");
    });
    return { animation, theme, changeTheme }
  }
}
</script>
<style lang="scss" scoped>
@media (min-width: 768px) and (max-width: 991.98px)
{
  .app-header .app-header-main, .app-main {
    width: 738px;
  }
  .app-header .app-header-main .app-header-search {
    width: 260px;
    margin-right: 0;
  }
  .app-header .app-header-main .app-header-user {
    display: none!important;
  }
}
@media (min-width: 768px) and (max-width: 1259.98px)
{
  .app-header {
    &-main {
      .app-header-logo {
        width: 150px;
        min-width: 150px;
      }
      .app-header-nav .nav-link {
        padding-left: 1rem;
        padding-right: 1rem;
      }
    }
  }
}
@media (min-width: 992px) and (max-width: 1259.98px)
{
  .app-header-main, .app-main {
    width: 962px;
  }
  .app-header .app-header-main .app-header-search {
    width: 300px;
    margin-right: 20px;
  }
}
@media (min-width: 1260px) and (max-width: 1499.98px)
{
  .app-header-main, .app-main {
    width: 1170px;
  }
}
@media (min-width: 1500px)
{
  .app-header-main, .app-main {
    width: 1410px;
  }
}
a {
  color: inherit;
}
.app-header {
  position: relative;
  width: 100%;
  &-topbar {
    position: relative;
    z-index: 100;
    height: 40px;
    font-size: 12px;
    top: 0;
    left: 0;
    width: 100%;
    border-bottom: 1px solid hsla(210,8%,51%,.09);
  }
  &-main {
    display: flex;
    align-items: center;
    height: inherit;
    margin: 0 auto;
    .nav {
      display: flex;
      flex-wrap: wrap;
      padding-left: 0;
      margin-bottom: 0;
      list-style: none;
      &-link {
        display: block;
        padding: .5rem 1rem;
      }
    }
    .top-bar-nav {
      &:first-child {
          padding-left: 0;
        }
    }
    .app-header-logo {
      display: flex;
      align-items: center;
      width: 180px;
      min-width: 180px;
      .icon-logo {
        font-size: 32px;
        margin-right: 15px;
      }
      span {
        font-size: 24px;
        font-weight: 700;
        flex-grow: 1;
        // color: #3c4248;
      }
    }
    .app-header-search {
      width: 360px;
      margin-right: 30px;
      position: relative;
      &__input {
        outline: none;
        position: relative;
        display: block;
        border: 1px solid hsla(210,8%,51%,.09);
        padding: 5px 25px;
        width: 100%;
        border-radius: 500px;
        background-color: transparent;
        transition: all .3s ease-out;
      }
      .search-to {
        font-size: 16px;
        right: 8px;
      }
      .search-clear, .search-to {
        position: absolute;
        right: 8px;
        top: -1px;
        font-weight: 700;
        width: 38px;
        height: 38px;
        line-height: 36px;
        text-align: center;
        background: transparent;
      }
    }
    .app-header-user {
      width: 100px;
      display: flex;
      justify-content: flex-end;
      .icon-wallet {
        font-size: 36px;
      }
    }
  }
  &-navbar {
    position: relative;
    height: 60px;
    z-index: 99;
  }
  &-nav {
    .nav-link {
      font-size: .9375rem;
      font-weight: 600;
      word-spacing: 2px;
      padding-left: 1.125rem;
      padding-right: 1.125rem;
      text-transform: uppercase;
      letter-spacing: 1px;
    }
  }
}
</style>
