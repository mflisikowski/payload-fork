# Payload Translations Extended Documentation

![NPM Version](https://img.shields.io/npm/v/@payloadcms/translations)
![Bundle Size](https://img.shields.io/bundlephobia/minzip/@payloadcms/translations)

## Original Documentation

<Banner type="warning">
**Original Documentation**: The content below comes from the original package README.md.
Further in the document, you'll find an extended, more detailed version of this documentation.
</Banner>

# Payload Translations

The home of Payloads API and Admin Panel translations.

## How to contribute

#### Updating a translation

1. Update the translation value
2. Run one of the following:
   ```sh
   yarn build
   // or
   npm build
   // or
   pnpm build
   ```

#### Adding a new translation

1. Add the new translation key/value pair for **all** languages located in the `<payload-repo-root>/packages/translations/src/languages` folder
2. Run one of the following:
   ```sh
   yarn build
   // or
   npm build
   // or
   pnpm build
   ```

#### Adding a new language

1. Create a new TS file in the `<payload-repo-root>/packages/translations/src/languages` folder, use the language code as the file name (e.g. `<payload-repo-root>/packages/translations/src/languages/en.ts` for English)
2. Copy all translations from an existing language file and update all of the translations to match your new language. Make sure the translation object containing all the translations is type `DefaultTranslationsObject`.
3. Run one of the following:
   ```sh
   yarn build
   // or
   npm build
   // or
   pnpm build
   ```
4. Import and export your new language file from within `<payload-repo-root>/packages/translations/src/exports/all.ts`
5. Re-export the file from within `<payload-repo-root>/packages/payload/src/exports/i18n/[your-new-language].ts`

---

## 📚 Extended Documentation

<Banner type="success">
**Note**: The documentation below has been automatically generated based on source code analysis and contains more detailed information than the original documentation above.
</Banner>

## Detailed Overview

The `@payloadcms/translations` package is PayloadCMS's comprehensive internationalization (i18n) system that provides translations for the admin panel and API messages across 46+ supported languages. This package serves as the foundation for multilingual PayloadCMS applications, handling everything from UI text translation to date formatting and pluralization rules.

The package addresses several key challenges in building multilingual applications:
- Consistent translation management across large applications
- Complex pluralization rules for different languages
- Date and time formatting for various locales
- Dynamic translation key generation with type safety
- Client/server translation context separation

It's primarily intended for PayloadCMS developers building multilingual applications, content managers working with international content, and contributors adding new language support to the PayloadCMS ecosystem.

<Banner type="info">
The package is open-source. [View source code](https://github.com/payloadcms/payload/tree/main/packages/translations). Need help? [Community Help](https://payloadcms.com/community-help).
</Banner>

## System Requirements

- **PayloadCMS**: 3.x or higher
- **Node.js**: 18.x or higher
- **TypeScript**: 5.0 or higher (recommended for full type safety)
- **Dependencies**: `date-fns` 4.1.0

## Installation

```bash
# npm
npm install @payloadcms/translations

# yarn
yarn add @payloadcms/translations

# pnpm
pnpm add @payloadcms/translations
```

### Peer Dependencies
This package requires the following peer dependencies:
```bash
npm install date-fns@4.1.0
```

## Quick Start

Basic configuration and usage:

```typescript
import { initI18n } from '@payloadcms/translations'
import { translations } from '@payloadcms/translations/all'

// Initialize i18n for server context
const i18n = await initI18n({
  config: {
    fallbackLanguage: 'en',
    supportedLanguages: translations,
  },
  context: 'api',
  language: 'en'
})

// Use translation function
const message = i18n.t('general:welcome') // "Welcome"
const countMessage = i18n.t('general:selectedCount', { count: 3 }) // "3 items selected"
```

## Detailed Configuration

### Main Options

#### `supportedLanguages`

- **Type**: `SupportedLanguages<TDefaultTranslations>`
- **Default value**: All available translations from `/all` export
- **Required**: Yes

Defines which languages your application supports. Each language includes translation strings and date-fns locale configuration.

```typescript
import { translations } from '@payloadcms/translations/all'

const config = {
  supportedLanguages: translations, // All 46+ languages
  // Or specific languages only:
  supportedLanguages: {
    en: translations.en,
    es: translations.es,
    fr: translations.fr,
  }
}
```

#### `fallbackLanguage`

- **Type**: `AcceptedLanguages`
- **Default value**: `'en'`
- **Required**: No

The language to use when a translation is missing in the current language.

```typescript
const config = {
  fallbackLanguage: 'en', // Falls back to English
  supportedLanguages: translations
}
```

#### `translations`

- **Type**: `Partial<{ [key in AcceptedLanguages]?: Language<TTranslations>['translations'] }>`
- **Default value**: `{}`
- **Required**: No

Custom translations to merge with or override default translations.

```typescript
const config = {
  supportedLanguages: translations,
  translations: {
    en: {
      general: {
        welcome: "Custom Welcome Message",
        customKey: "My Custom Translation"
      }
    }
  }
}
```

### Configuration Schema

```typescript
interface I18nOptions<TTranslations = DefaultTranslationsObject> {
  // Language to fall back to when translations are missing
  fallbackLanguage?: AcceptedLanguages
  
  // Available languages with their translation objects
  supportedLanguages?: SupportedLanguages<TTranslations>
  
  // Custom translations to merge with defaults
  translations?: Partial<{
    [key in AcceptedLanguages]?: Language<TTranslations>['translations']
  }>
}
```

## Usage Guides

### Basic Translation Usage

```typescript
import { initI18n, t } from '@payloadcms/translations'
import { translations } from '@payloadcms/translations/all'

// Initialize i18n instance
const i18n = await initI18n({
  config: {
    supportedLanguages: translations,
    fallbackLanguage: 'en'
  },
  context: 'api',
  language: 'fr'
})

// Simple translation
const greeting = i18n.t('general:welcome') // "Bienvenue"

// Translation with variables
const message = i18n.t('general:selectedCount', { count: 5 })
// "5 éléments sélectionnés"

// Direct translation function (without i18n instance)
const directTranslation = t({
  key: 'general:save',
  translations: translations.es.translations
}) // "Guardar"
```

### Working with Pluralization

PayloadCMS translations support complex pluralization rules:

```typescript
// English pluralization (_one, _other)
i18n.t('error:followingFieldsInvalid', { count: 1 }) 
// "The following field is invalid:"

i18n.t('error:followingFieldsInvalid', { count: 3 })
// "The following fields are invalid:"

// More complex pluralization (_zero, _one, _two, _few, _many, _other)
i18n.t('version:versionCount', { count: 0 }) // "No versions found"
i18n.t('version:versionCount', { count: 1 }) // "1 version found"
i18n.t('version:versionCount', { count: 5 }) // "5 versions found"
```

### Language Detection from Headers

Extract preferred language from HTTP Accept-Language headers:

```typescript
import { extractHeaderLanguage } from '@payloadcms/translations'

const acceptLanguage = "en-US,en;q=0.9,fr;q=0.8,es;q=0.7"
const preferredLanguage = extractHeaderLanguage(acceptLanguage)
// Returns: 'en' (first supported language from header)

const i18n = await initI18n({
  config: { supportedLanguages: translations },
  context: 'api',
  language: preferredLanguage || 'en'
})
```

### Client-Side Usage

For client-side applications with reduced translation sets:

```typescript
import { initI18n } from '@payloadcms/translations'
import { translations } from '@payloadcms/translations/all'

// Client context uses only essential translations
const clientI18n = await initI18n({
  config: {
    supportedLanguages: translations,
    fallbackLanguage: 'en'
  },
  context: 'client',
  language: 'de'
})

// Client translations are automatically filtered
// to include only UI-relevant strings
```

### Advanced Patterns

#### Custom Translation Objects

Create custom translation structures for specific needs:

```typescript
interface CustomTranslations {
  myApp: {
    dashboard: {
      title: string
      subtitle: string
    }
    errors: {
      networkError: string
      validationFailed: string
    }
  }
}

const customTranslations: CustomTranslations = {
  myApp: {
    dashboard: {
      title: "My Dashboard",
      subtitle: "Welcome back"
    },
    errors: {
      networkError: "Network connection failed",
      validationFailed: "Please check your input"
    }
  }
}

// Merge with Payload translations
const i18n = await initI18n({
  config: {
    supportedLanguages: translations,
    translations: {
      en: {
        ...translations.en.translations,
        ...customTranslations
      }
    }
  },
  context: 'api',
  language: 'en'
})
```

#### Dynamic Translation Loading

Load translations dynamically for better performance:

```typescript
// Load specific language on demand
async function loadLanguage(lang: AcceptedLanguages) {
  const { [lang]: translation } = await import('@payloadcms/translations/all')
  
  return initI18n({
    config: {
      supportedLanguages: { [lang]: translation },
      fallbackLanguage: 'en'
    },
    context: 'api',
    language: lang
  })
}

const germanI18n = await loadLanguage('de')
```

## API Reference

### Functions

#### `initI18n(args)`

Initializes and returns a complete i18n instance with translation function and date formatting.

**Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| config | `I18nOptions` | Configuration object with supported languages and settings |
| context | `'api' \| 'client'` | Context determines which translation keys are included |
| language | `AcceptedLanguages` | Target language code |

**Returns:** `Promise<I18n>`

**Example:**
```typescript
const i18n = await initI18n({
  config: {
    supportedLanguages: translations,
    fallbackLanguage: 'en'
  },
  context: 'api',
  language: 'fr'
})
```

#### `t(args)`

Standalone translation function for direct translation without i18n instance.

**Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| key | `TTranslationKeys` | Translation key in format "namespace:key" |
| translations | `Language['translations']` | Translation object |
| vars | `Record<string, any>` | Variables to interpolate |

**Returns:** `string`

**Example:**
```typescript
const message = t({
  key: 'general:welcome',
  translations: translations.en.translations,
  vars: { name: 'John' }
})
```

#### `getTranslation(label, i18n)`

Flexible translation function supporting multiple label types including React components and function-based labels.

**Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| label | `string \| Record<string, string> \| Function \| JSX.Element` | Label to translate |
| i18n | `I18n` | i18n instance |

**Returns:** `string | JSX.Element`

**Example:**
```typescript
// String translation
const simple = getTranslation('Hello', i18n)

// Multi-language object
const multilang = getTranslation({
  en: 'Hello',
  fr: 'Bonjour',
  es: 'Hola'
}, i18n)

// Function-based translation
const dynamic = getTranslation(({ t }) => t('general:welcome'), i18n)
```

#### `extractHeaderLanguage(acceptLanguageHeader)`

Parses HTTP Accept-Language header and returns the highest priority supported language.

**Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| acceptLanguageHeader | `string` | HTTP Accept-Language header value |

**Returns:** `AcceptedLanguages \| undefined`

**Example:**
```typescript
const language = extractHeaderLanguage("fr;q=0.9,en;q=0.8")
// Returns: 'fr'
```

#### `importDateFNSLocale(dateFNSKey)`

Dynamically imports date-fns locale for date formatting.

**Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| dateFNSKey | `DateFNSKeys` | date-fns locale key |

**Returns:** `Promise<Locale>`

### Utility Functions

#### `deepMergeSimple(obj1, obj2)`

Performs simple deep merge of translation objects.

**Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| obj1 | `object` | Base object |
| obj2 | `object` | Object to merge into base |

**Returns:** `T`

**Example:**
```typescript
const merged = deepMergeSimple(defaultTranslations, customTranslations)
```

### TypeScript Types

```typescript
// Main i18n instance type
interface I18n<TTranslations = DefaultTranslationsObject, TTranslationKeys = DefaultTranslationKeys> {
  dateFNS: Locale               // date-fns locale object
  dateFNSKey: DateFNSKeys       // date-fns locale key
  fallbackLanguage: string     // configured fallback language
  language: string             // current language
  t: TFunction<TTranslationKeys> // translation function
  translations: TTranslations   // loaded translations
}

// Translation function type
type TFunction<TTranslationKeys = DefaultTranslationKeys> = (
  key: TTranslationKeys,
  options?: Record<string, any>,
) => string

// Supported language codes
type AcceptedLanguages = 'en' | 'fr' | 'es' | 'de' | 'it' | 'pt' | 'ru' | 'ja' | 'ko' | 'zh' | 'ar' | /* ... and 35+ more */

// Language object structure
interface Language<TDefaultTranslations = DefaultTranslationsObject> {
  dateFNSKey: DateFNSKeys       // corresponding date-fns locale
  translations: TDefaultTranslations // translation strings
}

// Configuration options
interface I18nOptions<TTranslations = DefaultTranslationsObject> {
  fallbackLanguage?: AcceptedLanguages
  supportedLanguages?: SupportedLanguages<TTranslations>
  translations?: Partial<{
    [key in AcceptedLanguages]?: Language<TTranslations>['translations']
  }>
}

// Translation keys type (auto-generated from English translations)
type DefaultTranslationKeys = 
  | 'authentication:account'
  | 'authentication:login'
  | 'general:save'
  | 'general:cancel'
  | 'error:required'
  // ... 500+ more keys
```

## Supported Languages

The package supports 46+ languages with full translations:

### Available Languages

| Code | Language | RTL | Date-fns Support |
|------|----------|-----|------------------|
| `ar` | Arabic | ✓ | ✓ |
| `az` | Azerbaijani | | ✓ |
| `bg` | Bulgarian | | ✓ |
| `bn-BD` | Bengali (Bangladesh) | | ✓ |
| `bn-IN` | Bengali (India) | | ✓ |
| `ca` | Catalan | | ✓ |
| `cs` | Czech | | ✓ |
| `da` | Danish | | ✓ |
| `de` | German | | ✓ |
| `en` | English | | ✓ |
| `es` | Spanish | | ✓ |
| `et` | Estonian | | ✓ |
| `fa` | Persian | ✓ | ✓ |
| `fr` | French | | ✓ |
| `he` | Hebrew | ✓ | ✓ |
| `hr` | Croatian | | ✓ |
| `hu` | Hungarian | | ✓ |
| `hy` | Armenian | | ✓ |
| `id` | Indonesian | | ✓ |
| `is` | Icelandic | | ✓ |
| `it` | Italian | | ✓ |
| `ja` | Japanese | | ✓ |
| `ko` | Korean | | ✓ |
| `lt` | Lithuanian | | ✓ |
| `lv` | Latvian | | ✓ |
| `my` | Burmese | | |
| `nb` | Norwegian | | ✓ |
| `nl` | Dutch | | ✓ |
| `pl` | Polish | | ✓ |
| `pt` | Portuguese | | ✓ |
| `ro` | Romanian | | ✓ |
| `rs` | Serbian (Cyrillic) | | ✓ |
| `rs-latin` | Serbian (Latin) | | ✓ |
| `ru` | Russian | | ✓ |
| `sk` | Slovak | | ✓ |
| `sl` | Slovenian | | ✓ |
| `sv` | Swedish | | ✓ |
| `th` | Thai | | ✓ |
| `tr` | Turkish | | ✓ |
| `uk` | Ukrainian | | ✓ |
| `vi` | Vietnamese | | ✓ |
| `zh` | Chinese (Simplified) | | ✓ |
| `zh-TW` | Chinese (Traditional) | | ✓ |

### RTL Language Support

Right-to-left languages are automatically detected:

```typescript
import { rtlLanguages } from '@payloadcms/translations'

// Check if language is RTL
const isRTL = rtlLanguages.includes(currentLanguage)
// RTL languages: ['ar', 'fa', 'he']
```

## Package Exports

The package provides multiple export paths for different use cases:

### Main Export (`@payloadcms/translations`)
```typescript
import { 
  initI18n, 
  t, 
  getTranslation,
  importDateFNSLocale 
} from '@payloadcms/translations'
```

### All Languages (`@payloadcms/translations/all`)
```typescript
import { translations } from '@payloadcms/translations/all'
// Contains all 46+ supported languages
```

### Individual Languages (`@payloadcms/translations/languages/*`)
```typescript
import { en } from '@payloadcms/translations/languages/en'
import { fr } from '@payloadcms/translations/languages/fr'
import { de } from '@payloadcms/translations/languages/de'
```

### Utilities (`@payloadcms/translations/utilities`)
```typescript
import { deepMergeSimple } from '@payloadcms/translations/utilities'
```

### Helper Functions
```typescript
import { 
  acceptedLanguages, 
  extractHeaderLanguage, 
  rtlLanguages 
} from '@payloadcms/translations'
```

## Troubleshooting

### Common Issues

#### Missing Translation Keys

**Problem:** Translation key returns the key itself instead of translated text

**Solution:**
1. Verify the key exists in the translation files
2. Check key format uses colon separator (e.g., `'general:save'`)
3. Ensure language is properly loaded

**Example:**
```typescript
// ❌ Wrong - returns key as fallback
i18n.t('missing:key') // returns "missing:key"

// ✓ Correct - check if key exists first
const translation = i18n.t('general:save') // returns "Save"
```

#### Language Not Loading

**Problem:** Translations show in English despite setting different language

**Solution:**
1. Ensure language is included in `supportedLanguages`
2. Check language code matches available languages
3. Verify async initialization completes

**Example:**
```typescript
// ❌ Wrong - language not in supported languages
const i18n = await initI18n({
  config: {
    supportedLanguages: { en: translations.en }, // Only English
  },
  context: 'api',
  language: 'fr' // French not supported
})

// ✓ Correct - include target language
const i18n = await initI18n({
  config: {
    supportedLanguages: { 
      en: translations.en,
      fr: translations.fr 
    },
  },
  context: 'api',
  language: 'fr'
})
```

#### Pluralization Not Working

**Problem:** Plural forms not displaying correctly

**Solution:**
1. Pass `count` parameter in variables object
2. Check if target language has plural variants
3. Verify pluralization rules for specific language

**Example:**
```typescript
// ❌ Wrong - no count provided
i18n.t('general:selectedCount') // "{{count}} items selected"

// ✓ Correct - count triggers pluralization
i18n.t('general:selectedCount', { count: 1 }) // "1 item selected"
i18n.t('general:selectedCount', { count: 3 }) // "3 items selected"
```

#### Date Formatting Issues

**Problem:** Dates display in wrong format or English

**Solution:**
1. Ensure date-fns locale loads correctly
2. Use i18n.dateFNS for date formatting
3. Check dateFNSKey mapping

**Example:**
```typescript
import { format } from 'date-fns'

// Use i18n.dateFNS for locale-aware formatting
const formattedDate = format(new Date(), 'PPP', {
  locale: i18n.dateFNS
})
```

### Debugging

Enable debug logging to troubleshoot translation issues:

```typescript
// Translation function logs missing keys to console
const translation = i18n.t('missing:key')
// Console: "key not found: missing:key"

// Check loaded translations
console.log('Available translations:', Object.keys(i18n.translations))

// Verify language setup
console.log('Current language:', i18n.language)
console.log('Fallback language:', i18n.fallbackLanguage)
console.log('Date locale:', i18n.dateFNS.code)
```

## Contributing New Languages

### Steps to Add a New Language

1. **Create Language File**
   Create `/src/languages/[language-code].ts`:

```typescript
import type { Language } from '../types.js'

export const myTranslations = {
  authentication: {
    account: 'Mon Compte',
    login: 'Se connecter',
    // ... all required translation keys
  },
  general: {
    save: 'Sauvegarder',
    cancel: 'Annuler',
    // ... complete translation set
  },
  // ... all namespace sections
}

export const myLanguage: Language = {
  dateFNSKey: 'fr', // corresponding date-fns locale
  translations: myTranslations,
}
```

2. **Add to Exports**
   Update `/src/exports/all.ts`:

```typescript
import { myLanguage } from '../languages/myLanguage.js'

export const translations = {
  // ... existing languages
  'my-lang': myLanguage,
}
```

3. **Update Types**
   Add language code to `/src/utilities/languages.ts`:

```typescript
export const acceptedLanguages = [
  // ... existing languages
  'my-lang',
] as const
```

4. **Test Completeness**
   Ensure all 500+ translation keys are included by using English as template.

### Translation Guidelines

- **Consistency**: Use consistent terminology across all translation keys
- **Context**: Consider UI context when translating (button vs. menu item)
- **Length**: Keep translations reasonably similar in length to English
- **Pluralization**: Include all required plural forms for your language
- **Cultural**: Adapt for cultural context, not just literal translation

## Performance

### Performance Optimization

1. **Lazy Loading**: Load only required languages

```typescript
// Instead of loading all languages
import { translations } from '@payloadcms/translations/all'

// Load specific languages
import { en } from '@payloadcms/translations/languages/en'
import { fr } from '@payloadcms/translations/languages/fr'

const supportedLanguages = { en, fr }
```

2. **Client Context**: Use client context for reduced bundle size

```typescript
// Client context automatically filters to essential translations
const clientI18n = await initI18n({
  config: { supportedLanguages },
  context: 'client', // Smaller translation set
  language: 'en'
})
```

3. **Memoization**: The `initI18n` function is automatically memoized based on language and context

4. **Tree Shaking**: Individual language imports enable better tree shaking

```typescript
// ✓ Good - only loads needed languages
import { en, fr, de } from '@payloadcms/translations/languages/en'

// ❌ Less optimal - loads all languages
import { translations } from '@payloadcms/translations/all'
```

## Security

- **No User Input**: Translation keys are static strings, not user input
- **XSS Protection**: HTML escaping handled at framework level
- **No Secret Data**: Translation files contain only display text
- **Safe Interpolation**: Variable interpolation uses safe string replacement

## Contributing

Found a bug or have a suggestion? [Open an issue](https://github.com/payloadcms/payload/issues) or submit a Pull Request.

### Translation Contributions Welcome

We especially welcome contributions for:
- New language support
- Translation accuracy improvements  
- Missing translation keys
- Cultural adaptations

## License

MIT License - see the [LICENSE](LICENSE.md) file for details.