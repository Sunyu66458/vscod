## `less-loader` 版本过高导致的报错
报错信息
```javascript
this.getOptions is not a function
```
建议 `less` 和 `less-loader` 版本
```javascript
"less": "^4.1.1",
"less-loader": "^5.0.0",
```

## 打包项目后预览
`npm install -g serve`  
打开 `dist` 目录，运行 `serve -s`


## 使用 `vue-router`
```javascript
import { useRouter } from 'vue-router'

setup() {
    const router = useRouter()
    const goPath = () => {
      router.push('/count')
    }

    return {
      goPath,
    }
  },
```
## 移动端去每个路由再回去保持离开时的位置

在主页面监听滚动事件,获取每次滚动距离顶部的位置, 并存入一个容器(`loacalStorage`, `sessionStorage`, `vuex`)中, 路由切换时获取这个数据,并创建一个对象,为每个路由创建一个对应的位置,切换时取这个数据

## 移动端实现左右滑动切换路由


## `ts` 项目中 `path`模块找不到 `__dirname` 报错
```javascript
yarn add @types/node -D
```

## `main.ts` 中引入插件报错
```typescript
import VueTouch from 'vue-touch'
```
报错如下
```typescript
// 无法找到模块“vue-touch”的声明文件。“d:/code/node/weibo_h5/node_modules/vue-touch/dist/vue-touch.js”隐式拥有 "any" 类型。
  尝试使用 `npm i --save-dev @types/vue-touch` (如果存在)，或者添加一个包含 `declare module 'vue-touch';` 的新声明(.d.ts)文件ts(7016)
```

## 路由跳转层级错误
使用 `router.push('home')` `name`做参数 跳转可能会出现层级错误问题  
建议使用 `router.push({ path: 'register', query: { plan: 'private' }})`, `path` 做参数进行路由跳转

## vite.config.js配置
```javascript
import { createVuePlugin } from 'vite-plugin-vue2'
import path from 'path'
import styleImport from 'vite-plugin-style-import'
import px2viewport from 'postcss-px-to-viewport'

export default {
  plugins: [
    createVuePlugin(),
    styleImport({
      libs: [
        {
          libraryName: 'vant',
          esModule: true,
          resolveStyle: (name) => `vant/es/${name}/style`,
        },
      ],
    }),
  ],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, 'src'),
    },
  },
  css: {
    postcss: {
      plugins: [
        px2viewport({
          viewportWidth: 375,
          unitPrecision: 3,
          viewportUnit: 'vw',
          minPixelValue: 1,
          mediaQuery: false,
          selectorBlackList: [/not2vw$/],
        }),
      ],
    },
  },
  server: {
    proxy: {
      '/api': {
        target: 'http://www.bsteel.com.cn/newexchange/webmove',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, ''),
      },
    },
  },
}

```