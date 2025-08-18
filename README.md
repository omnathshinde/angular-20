# Angular 20 Base Template 🚀

> **Note:** Install Angular CLI globally first:
>
> ```bash
> npm install -g @angular/cli
> ```

A clean, production-ready Angular 20 starter configured with modern dev tools:

- ✅ Angular 20 + Node.js 22 support
- ✅ TypeScript 5
- ✅ ESLint (`@angular-eslint`)
- ✅ Prettier for formatting
- ✅ Husky + lint-staged for pre-commit checks
- ✅ Environment configuration
- ✅ Recommended VS Code setup

---

## ⚙️ Prerequisites

- **Node.js**: v22.x (LTS)
- **npm**: v10.x
- **Angular CLI**: latest (20.x)

Check versions:

```bash
node -v
npm -v
ng version
```

> **ESM note:** this project uses ESM for tooling. In `package.json`,
> set:

```json
{ "type": "module" }
```

---

## 🎨 Prettier Setup

### 1) Install Prettier

```bash
npm install -D prettier
```

### 2) Add Configuration

Create a **`.prettierrc`** file in the project root:

```json
{
	"printWidth": 120,
	"useTabs": true,
	"singleQuote": false,
	"overrides": [
		{
			"files": "*.html",
			"options": {
				"parser": "angular"
			}
		}
	]
}
```

Create a **`.prettierignore`** file:

```
# Node modules
node_modules/

# Build output
dist/
build/

# Environment variables
.env

# Logs
*.log

# Static assets
public/
assets/


node_modules
dist
coverage
*.svg
*.png
```

### 3) Add NPM Scripts

In **package.json** → `"scripts"` section, add:

```json
{
	"scripts": {
		"format": "prettier --write .",
		"format:check": "prettier --check ."
	}
}
```

### 4) Usage

Format all code:

```bash
npm run format
```

Check formatting (CI-friendly, no changes applied):

```bash
npm run format:check
```

---

## 🧹 ESLint Setup (Angular 20, Flat Config)

### 1) Add Angular ESLint schematics

```bash
ng add @angular-eslint/schematics
```

### 2) Install additional ESLint deps

```bash
npm install -D eslint-plugin-simple-import-sort eslint-plugin-import eslint-config-prettier
```

**What they do (one-liners):**

- `eslint-plugin-simple-import-sort` – stable, opinionated import sorting
- `eslint-plugin-import` – import order/quality checks (duplicates, first, newline)
- `eslint-config-prettier` – disables rules that conflict with Prettier formatting

### 3) `eslint.config.js` (flat config)

Create **`eslint.config.js`** in the project root:

```json
import eslint from "@eslint/js";
import * as tseslint from "typescript-eslint";
import * as angular from "angular-eslint";
import simpleImportSort from "eslint-plugin-simple-import-sort";
import eslintPluginImport from "eslint-plugin-import";

export default tseslint.config(
	{
		files: ["**/*.ts"],
		plugins: {
			"simple-import-sort": simpleImportSort,
			import: eslintPluginImport,
		},
		extends: [
			eslint.configs.recommended,
			...tseslint.configs.recommended,
			...tseslint.configs.stylistic,
			...angular.configs.tsRecommended,
		],
		processor: angular.processInlineTemplates,
		rules: {
			"simple-import-sort/imports": [
				"error",
				{
					groups: [
						["^node:"],
						["^@?\\w"],
						["^src/", "^@app", "^@core", "^@shared"],
						["^\\."],
						["^\\u0000"],
					],
				},
			],
			"simple-import-sort/exports": "error",
			"import/first": "error",
			"import/newline-after-import": "error",
			"import/no-duplicates": "error",
			"@angular-eslint/directive-selector": [
				"error",
				{
					type: "attribute",
					prefix: "app",
					style: "camelCase",
				},
			],
			"@angular-eslint/component-selector": [
				"error",
				{
					type: "element",
					prefix: "app",
					style: "kebab-case",
				},
			],
		},
	},
	{
		files: ["**/*.html"],
		extends: [
			...angular.configs.templateRecommended,
			...angular.configs.templateAccessibility,
		],
		rules: {},
	},
);
```

### 4) Usage

Now you can lint your project with Angular CLI:

```bash
ng lint
```

This will run ESLint using the configuration above.If fixes are available, ESLint will suggest running with --fix:

```bash
ng lint --fix
```
