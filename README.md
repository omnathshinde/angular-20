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
