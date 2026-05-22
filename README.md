
vite plugin for message declaration generation for [use-intl](https://next-intl.dev/docs/environments/core-library)

TODO: Sunset this package when https://github.com/amannn/next-intl/discussions/2191 is resolved

### installation

install the plugin:

```bash
npm install -D next-intl-vite-plugin
```

add it to your `vite.config.ts`:

```ts
import { defineConfig } from 'vite';
import { intlMessagesDeclaration } from "@dvries/vite-use-intl-messages-declaration"

export default defineConfig({
  plugins: [
    intlMessagesDeclaration({
        messages: [
            "src/locales/en/messages.json",
            "src/locales/fr/messages.json"
        ]
    })
  ]
})
```

Make sure `allowArbitraryExtensions` is enabled in your `tsconfig.json`:

```json
{
  "compilerOptions": {
    "allowArbitraryExtensions": true
  }
}
```

And use the generated types:

```ts
export type IntlMessages = typeof import("src/locales/en/messages.json")["default"]

declare module "use-intl" {
	interface AppConfig {
		Locale: IntlLocale
		Messages: IntlMessages
	}
}
```
