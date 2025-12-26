_to_write = """# AI Agent Guide: Internationalization (i18n) Implementation

**Objective**: To implement a robust internationalization framework in the Refine frontend application, supporting English and Spanish initially, with a clear process for adding new languages.

---

## 1. Setup and Configuration

### 1.1. Install Dependencies

In the `bi-reset-frontend` directory, install the necessary `i18next` packages:

```bash
pnpm install i18next react-i18next i18next-browser-languagedetector
```

### 1.2. Create Locale Files

Create the following directory structure and files inside the `public/` directory:

```
/public
└── locales/
    ├── en/
    │   └── common.json
    └── es/
        └── common.json
```

**`public/locales/en/common.json`**:

```json
{
  "dashboard": {
    "title": "Dashboard"
  },
  "reports": {
    "title": "Reports"
  },
  "buttons": {
    "save": "Save",
    "cancel": "Cancel"
  }
}
```

**`public/locales/es/common.json`**:

```json
{
  "dashboard": {
    "title": "Tablero"
  },
  "reports": {
    "title": "Reportes"
  },
  "buttons": {
    "save": "Guardar",
    "cancel": "Cancelar"
  }
}
```

### 1.3. Configure i18next

Create a new file `src/i18n.ts` to configure the `i18next` instance.

```typescript
import i18n from 'i18next';
import { initReactI18next } from 'react-i18next';
import LanguageDetector from 'i18next-browser-languagedetector';

i18n
  // Detect user language
  .use(LanguageDetector)
  // Pass the i18n instance to react-i18next
  .use(initReactI18next)
  // Initialize i18next
  .init({
    debug: true, // Set to false in production
    fallbackLng: 'en',
    interpolation: {
      escapeValue: false, // React already safes from xss
    },
    resources: {
      en: {
        common: require('../public/locales/en/common.json')
      },
      es: {
        common: require('../public/locales/es/common.json')
      }
    },
    ns: ['common'],
    defaultNS: 'common'
  });

export default i18n;
```

Finally, import this configuration in your main application entry point (e.g., `src/index.tsx` or `src/App.tsx`):

```typescript
import './i18n';
```

## 2. Usage in Components

To use the translations in your React components, use the `useTranslation` hook from `react-i18next`.

**Example Component**:

```tsx
import React from 'react';
import { useTranslation } from 'react-i18next';

export const MyDashboard: React.FC = () => {
  const { t } = useTranslation('common');

  return (
    <div>
      <h1>{t('dashboard.title')}</h1>
      <button>{t('buttons.save')}</button>
    </div>
  );
};
```

## 3. Language Switching UI

Implement a language switcher component that allows the user to manually change the language.

**Example LanguageSwitcher.tsx**:

```tsx
import React from 'react';
import { useTranslation } from 'react-i18next';

const languages = [
  { code: 'en', name: 'English' },
  { code: 'es', name: 'Español' },
];

export const LanguageSwitcher: React.FC = () => {
  const { i18n } = useTranslation();

  const changeLanguage = (lng: string) => {
    i18n.changeLanguage(lng);
  };

  return (
    <div>
      {languages.map((lang) => (
        <button
          key={lang.code}
          onClick={() => changeLanguage(lang.code)}
          disabled={i18n.language === lang.code}
        >
          {lang.name}
        </button>
      ))}
    </div>
  );
};
```

## 4. AI-Assisted Translation Workflow (Future Scope)

As specified in the architecture, a CI/CD pipeline will be created to automate the translation of new strings. The high-level steps for this workflow are:

1.  **Trigger**: The pipeline runs on any push to the `main` branch where `public/locales/en/common.json` has changed.
2.  **Diff**: The script identifies new keys present in the English file but missing in other language files (e.g., `es/common.json`).
3.  **Translate**: For each new key, the English text is sent to an AI translation API (e.g., Google Translate).
4.  **Update Files**: The script updates the corresponding language files with the translated text.
5.  **Create PR**: The pipeline creates a new pull request titled `feat(i18n): Add new translations for [language_code]` for a human to review and merge.

This ensures that the application's translations stay up-to-date with minimal manual intervention.
"""
