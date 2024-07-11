## 使い方
```
yarn install
PORT=3003 yarn run dev
```

Access to http://localhsot:3003

pages
- http://localhost:3003/index2
  - http://localhost:3003/test2
  - http://localhost:3003/test-noprefetch
- http://localhost:3003/index
  - http://localhost:3003/test


## /index2 のページで確認できる
- NuxtLinkによって指定されるパスのPageはPrefetchが行われる https://nuxt.com/docs/api/components/nuxt-link
  - /index2 において、TypeIがPrefetchされているがTypeAがprefetchされないのはnoPrefetchオプションによるもの

## /index (または/) のページで確認できる
- DynamicImportがあるので、基本的にComponentをImportする必要はない(=TypeCの Importを書いていない)
  - Component内で使ってるComponent(TypeC)や明示的にImportしているコンポーネント(J,H)は
    (/ ページの)prefetchの時点でそのComponent自体も取得される

## /indexのリンクから/testへ移動して確認できる
- defineAsyncComponentをすると、prefetch時点でページで使われているコンポーネントを読まなくて済む  
  (=TypeA,E,F,Kがtestページ読み込み時=必要になった時に取得される)
  - ただその用途で使うならLazyPrefixをつけるだけでもできる  
    (=TypeD, TypeLが表示されるまで読み込まれていない)
- Suspenseを使うと、Componentの取得完了まで変更を待ってくれる(TypeA/Bのトグル)
  - ネットワークを「低速3G」などにしてTypeF/GのToggleをすると、当該コンポーネント部分がなくなった状態でComponentを取得し始める
