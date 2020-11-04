# Tailwind Setup
## Setup

1. Install Stylelint
`npm install --save-dev stylelint stylelint-config-recommended`

2. Create a file named `stylelint.config.js` with the following
```javascript
module.exports = {
  extends: ["stylelint-config-recommended"],
  rules: {
    "at-rule-no-unknown": [
      true,
      {
        ignoreAtRules: [
          "tailwind",
          "apply",
          "variants",
          "responsive",
          "screen",
        ],
      },
    ],
    "declaration-block-trailing-semicolon": null,
    "no-descending-specificity": null,
  },
};
```
3. Install _Stylelint_ and _Tailwind CSS Intellisense_ VSCode extensions
4. Tweak VSCode Settings (`settings.json`)
```javascript
"css.validate": false,
"less.validate": false,
"scss.validate": false
```
5. Install TailwindCSS `npm install tailwindcss`
6. Add build script to `package.json`
```javascript
"build-css": "tailwindcss build src/styles.css -o public/styles.css"
```
7. (Optional) Scaffold default Tailwind configuration
`npx tailwindcss init tailwindfull-config.js --full`

8. Minimal configuration file to store custom configurations
`npx tailwindcss init`

9. Sample configuration extension
```javascript
module.exports = {
  future: {
    // removeDeprecatedGapUtilities: true,
    // purgeLayersByDefault: true,
    // defaultLineHeights: true,
    // standardFontWeights: true
  },
  purge: [],
  theme: {
    extend: {
      colors: {
        primary:'#ff6363',
        secondary:{
          100: '#E2E2D5',
          200: '#88883'
        }
      },
      fontFamily:{
        standard: ['Nunito']
      }
    }
  },
  variants: {},
  plugins: []
}
```
## Usage

1. Common Utility Patterns extracted as classes
```html
<button class="btn-blue">
  Button
</button>

<style>
.btn-blue {
  @apply bg-blue-500 text-white font-bold py-2 px-4 rounded;
}
.btn-blue:hover {
  @apply bg-blue-700;
}
</style>
```
2. Multiple `@apply` calls can be used
```css
.btn {
  @apply font-bold;
  @apply py-2;
  @apply px-4;
  @apply rounded;
}
```
3. Use the `@layer` directive to tell Tailwind which "bucket" a set of custom styles belong in. Valid layers are a `base`, `components`, and `utilities`
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  h1 {
    @apply text-2xl;
  }
  h2 {
    @apply text-xl;
  }
}

@layer components {
  .btn-blue {
    @apply bg-blue-500 text-white font-bold py-2 px-4 rounded;
  }
  .btn-blue:hover {
    @apply bg-blue-700;
  }
}

@layer utilities {
  @variants hover, focus {
    .filter-none {
      filter: none;
    }
    .filter-grayscale {
      filter: grayscale(100%);
    }
  }
}
```
4. 
