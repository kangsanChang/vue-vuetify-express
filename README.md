## Vue-Vuetify-Express 연동

### Install

- Node.js
- VueCLI (Version 3.x)
  - Standard tooling for Vue.js development
  - Provides the vue command in your terminal
    - `vue create`
    - `vue serve`
    - `vue ui`
  - Node Version Requirement (8.9 or above)
    ``` bash
    npm i -g @vue/cli
    # OR
    yarn global add @vue/cli
    ```
- express-generator
  ```bash
  npm i -g express-generator
  ```


### Vue project 생성

```bash
vue create frontend
# OR
vue ui
```
create 설정 사항
![create setting](https://user-images.githubusercontent.com/15089420/53781436-31f95900-3f4c-11e9-86f7-ab36f8c26fad.png)

### Express Project 생성

```bash
express --view=pug backend
# 설치 후 backend 에서
npm i
```

### Vuetify 추가

```bash
# frontend directory 에서
vue add vuetify
```
## 프로젝트(front,back) 통합

1. `[backend] ` connect-history-api-fallback 설치 (vue-router 와 연동 위함)
    ```bash
    npm i --save connect-history-api-fallback
    ```
2. `[backend] ` app.js 에 connect-history-api-fallback 추가
    ```js
    // app.js
    app.use(require('connect-history-api-fallback')());
    ```
3. `[frontend]` App.vue 에서 router-view 사용하도록 v-content 수정
    ```vue
    // App.vue
    <template>
      ...
        <v-content>
          <router-view></router-view>
        </v-content>
      ...
    </template>
    ```
4. `[frontend]` npm build 결과 파일 경로 수정 (backend 의 public으로)
    ```json
    // packeage.json
    ...
    "scripts": {
        "serve": "vue-cli-service serve",
        "build": "vue-cli-service build --dest ../backend/public",
        "lint": "vue-cli-service lint"
      },
    ...
    ```

5. front 개발 후 npm run build 하면 express server 에서 실행가능 (localhost:3000)
