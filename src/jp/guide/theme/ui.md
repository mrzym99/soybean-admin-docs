# コンポーネントライブラリのテーマ

## NaiveUI のテーマ設定

**テーマカラーに基づいてコンポーネントライブラリのテーマ変数を生成する**

```ts
/**
 * Get naive theme
 *
 * @param colors Theme colors
 */
function getNaiveTheme(colors: App.Theme.ThemeColor) {
  const { primary: colorLoading } = colors;

  const theme: GlobalThemeOverrides = {
    common: {
      ...getNaiveThemeColors(colors)
    },
    LoadingBar: {
      colorLoading
    }
  };

  return theme;
}

/** Naive theme */
const naiveTheme = computed(() => getNaiveTheme(themeColors.value));
```

::: tip 代码位置
src/store/modules/theme/shared.ts

src/store/modules/theme/index.ts
:::

**テーマ変数を適用する**

```vue
<template>
  <NConfigProvider
    :theme="naiveDarkTheme"
    :theme-overrides="themeStore.naiveTheme"
    :locale="naiveLocale"
    :date-locale="naiveDateLocale"
    class="h-full"
  >
    <AppProvider>
      <RouterView class="bg-layout" />
    </AppProvider>
  </NConfigProvider>
</template>
```

::: tip 代码位置
src/App.vue
:::

## AntDesignVue のテーマ設定

**テーマカラーに基づいてコンポーネントライブラリのテーマ変数を生成する**

```ts
/**
 * Get antd theme
 *
 * @param colors Theme colors
 * @param darkMode Is dark mode
 */
function getAntdTheme(colors: App.Theme.ThemeColor, darkMode: boolean) {
  const { defaultAlgorithm, darkAlgorithm } = antdTheme;

  const { primary, info, success, warning, error } = colors;

  const theme: ConfigProviderProps['theme'] = {
    token: {
      colorPrimary: primary,
      colorInfo: info,
      colorSuccess: success,
      colorWarning: warning,
      colorError: error
    },
    algorithm: [darkMode ? darkAlgorithm : defaultAlgorithm],
    components: {
      Menu: {
        colorSubItemBg: 'transparent'
      }
    }
  };

  return theme;
}

/** Antd theme */
const antdTheme = computed(() => getAntdTheme(themeColors.value, darkMode.value));
```

::: tip 代码位置
src/store/modules/theme/shared.ts

src/store/modules/theme/index.ts
:::

**テーマ変数を適用する**

```vue
<template>
  <ConfigProvider :theme="themeStore.antdTheme" :locale="antdLocale">
    <AppProvider>
      <RouterView class="bg-layout" />
    </AppProvider>
  </ConfigProvider>
</template>
```
