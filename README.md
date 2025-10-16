# eslint-prettier-for-vite+tailwind+shadcdn-ui

Eslint + Prettier + Vite + Tailwind + ShadcdnUI

#### Eslint + Prettier + Vite + Vite + Tailwind + ShadcdnUI setup without headaches and conflicts

### Instalação e configuração do Vite

1 - Instale o Vite:

[Vite Guide](https://vite.dev/guide/)

- Obs: Caso antes já tenha um arquivo README, a instalação vai sobrescrever. Então faça backup antes ou volte a versão dele com usando o git.

```sh
pnpm create vite .
```

Siga o passo a passo, no meu caso, já tem arquivos no projeto então vou mandar ignorar. E vou usar React + TypeScript
(Use as setas para mudar de opção)

1. ✔ Ignore files and continue
2. ✔ React
3. ✔ TypeScript
4. ✗ Use rolldown-vite
5. ✔ Install with pnpm and start now?

2 - Caso tenha optado por não instalar no wizard, instale as dependências e rode o projeto:

```sh
pnpm install
pnpm dev
```

3 - Caso queira trocar a porta, adicione no **vite.config.ts**:

```js
export default defineConfig({
	// adicione
	server: {
		port: 3001,
	},
	//
	plugins: [react()],
})
```

### Limpando o projeto padrão

1 - Exclua todos os arquivos .css e .svg

```sh
// remover
public/vite.svg
assets/react.svg
// remover
App.css
index.css
```

2 - Remova os imports desnecessários de **main.tsx**:

```js
// remover
import './index.css'
```

3 - Remova os imports e códigos desnecessários de **App.tsx**:

```js
// remover
import { useState } from 'react'
import reactLogo from './assets/react.svg'
import viteLogo from '/vite.svg'
import './App.css'
// remover
const [count, setCount] = useState(0)
// remover todo HTML do return (...)
```

4 - Adicione apenas um Hello World no return do **App.tsx**, ficando:

```html
<h1>Hello World !!!</h1>
```

- Vai dar erro de importação no **main.tsx**

5 - Corrija a importação no **main.tsx**, adicionando chaves { }:

```js
// mudar de
import App from './App.tsx'
// para
import { App } from './App.tsx'
```

6 - Comente a linha do Favicon no **index.html**:

```html
<!-- <link rel="icon" type="image/svg+xml" href="logo.svg" /> -->
```

- Com isso, o projeto está limpo, pronto para ser organizado ao seu critério e exibindo apenas um **Hello World !!!** na página inicial.

Rode com:

```sh
pnpm dev
```

---

### Instalação e configuração do Prettier

1 - Instale o Prettier:

[Prettier Install](https://prettier.io/docs/install)

- Obs: O ESLint já vem por padrão instalado qdo instalamos o Vite.

```sh
pnpm add --save-dev --save-exact prettier
```

2 - Crie o arquivo de exclusão **.prettierignore** e adicione:  
[Ignoring Code](https://prettier.io/docs/ignore)

```ini
# Dist Folder
dist
```

3 - Crie o arquivo de configuração do Prettier, **.prettierrc.json** contendo:  
[Prettier Options](https://prettier.io/docs/options)

- Minha configuração:  
  **printWidth=80** - Largura máxima de uma linha (quebra após passar)  
  **endOfLine="lf"** - Quebra de linha, "lf" padrão unix  
  **singleQuote=true** - Aspas simples  
  **jsxSingleQuote=true** - Aspas simples no jsx também  
  **quoteProps="as-needed"** - Usa aspas nas propriedases, só quando necessário  
  **semi=false** - Sem ponto e virgula  
  **useTabs=true** - Usar tabs em vez de espaços para indentação  
  **tabWidth=4** - Tab equvalente a 4 espaços  
  **arrowParens="always"** - Sempre usa parenteses nas Arrow Functions

```json
{
	"printWidth": 80,
	"endOfLine": "lf",
	"singleQuote": true,
	"jsxSingleQuote": true,
	"quoteProps": "as-needed",
	"semi": false,
	"useTabs": true,
	"tabWidth": 4,
	"arrowParens": "always"
}
```

- Atenção! Para funcionar deve estar marcado a opção do Prettier no VSCode requireConfig = true

Para habilitar via interface vá na Engrenagem > Settings e busque por **Prettier: Require Config**  
Marque a caixa de seleção e REINICIE o VSCode.

Para verificar/adicionar no **settings.json**.

```json
"prettier.requireConfig": true,
```

É essa linha que é adicionada ao clicar na caixa de seleção.

4 - Para que funcione ao salvar o arquivo ou no autoSave, adicione também no **settings.json**:

```js
// Verifique se existe:
"editor.formatOnSave": true
// Se não funcionar nos	.tsx, tente adicionar
"[typescriptreact]": {
    "editor.formatOnSave": true
},
```

Reinicie o VSCode.

5 - Caso queira, crie os comandos na sessão de **scripts** do **package.json**:

```json
"scripts": {
  "check": "prettier --check \"src/**/*.ts*\"",
  "format": "prettier --write \"src/**/*.ts*\""
}
```

Testando. Vá no **App.tsx** e **main.tsx** e volte aspas duplas e ponto e vírgula.

Verificar:

```sh
pnpm check
```

Corrigir:

```sh
pnpm format
```

---

### Garantindo que não vai ter conflito entre o Eslint e o Prettier.

- Aqui que vem a grande sacada para que as duas extensões e pacotes não conflitem e fique um anulando alguma coisa que o outro modificou:  
  [Integrating with Linters](https://prettier.io/docs/integrating-with-linters)

1 - Vendo a documentação acima, vamos instalar o pacote **eslint-config-prettier**:  
[Eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)

```sh
pnpm add -D eslint-config-prettier
```

2 - No arquivo de configuração do Eslint, importe e adicione por último o **eslintConfigPrettier**:

```js
// Importe
import eslintConfigPrettier from 'eslint-config-prettier'

// Na parte onde tem
tseslint.configs.recommended,
// Adicione por último
eslintConfigPrettier,
```

3 - Crie uma área para colocar as exceções às regras:

- Coloquei algumas que costumo usar, mudando alguns erros para apenas alerta.
- Normalmente no próprio erro, tem um link para documentação da regra, ex:  
   [no-unused-vars](https://typescript-eslint.io/rules/no-unused-vars/)  
  Caso não seja necessária, basta ver as opções na documentação e adicionar em **rules**.

```js
// Depois de
reactRefresh.configs.vite,
// Adicione
{
	rules: {
		'prefer-const': 'warn',
		'no-unused-vars': 'off',
		'@typescript-eslint/no-unused-vars': 'warn',
	},
},
```

### Organizando as importações.

- Um excelente plugin para organizar os imports e exports é esse:  
  [Simple import sort](https://github.com/lydell/eslint-plugin-simple-import-sort)

1 - Instale

```sh
pnpm add -D eslint-plugin-simple-import-sort
```

2 - No arquivo de configuração do Eslint, importe e adicione por último o **simpleImportSort**:

```js
// Importe
import simpleImportSort from "eslint-plugin-simple-import-sort";

// entre o languageOptions e o extends, adicione
plugins: {
	'simple-import-sort': simpleImportSort,
},
// adicione as regras na sessão já existente
'simple-import-sort/imports': 'error',
/* 'simple-import-sort/exports': 'error', */
// no caso, não quero que formate o exports, então comentei a regra
```

--

O arquivo final **eslint.config.js**, ficou assim:

```js
import js from '@eslint/js'
import globals from 'globals'
import reactHooks from 'eslint-plugin-react-hooks'
import reactRefresh from 'eslint-plugin-react-refresh'
import tseslint from 'typescript-eslint'
import { defineConfig, globalIgnores } from 'eslint/config'
import eslintConfigPrettier from 'eslint-config-prettier'
import simpleImportSort from 'eslint-plugin-simple-import-sort'

export default defineConfig([
	globalIgnores(['dist']),
	{
		files: ['**/*.{ts,tsx}'],
		languageOptions: {
			ecmaVersion: 2020,
			globals: globals.browser,
		},
		plugins: {
			'simple-import-sort': simpleImportSort,
		},
		extends: [
			js.configs.recommended,
			tseslint.configs.recommended,
			reactHooks.configs['recommended-latest'],
			reactRefresh.configs.vite,
			{
				rules: {
					'prefer-const': 'warn',
					'no-unused-vars': 'off',
					'@typescript-eslint/no-unused-vars': 'warn',
					'simple-import-sort/imports': 'error',
					/* 'simple-import-sort/exports': 'error', */
				},
			},
			eslintConfigPrettier,
		],
	},
])
```

---

### Instalação e configuração do Tailwind

1 - Instale o TailwindCSS:

- O guia do Shadcn tem as intruções para os 2. Shadcn-UI e Tailwind:  
  [Shadcn Guide](https://ui.shadcn.com/docs/installation/vite)

```sh
pnpm add tailwindcss @tailwindcss/vite
```

2 - Instale os Types:

```sh
pnpm add -D @types/node
```

3 - Edite o **tsconfig.json** e adicione:

```js
/* depois do colchete do "references"]*/
,
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
```

4 - Atualize o **vite.config.ts**, adicionando:

```js
// adicione
import path from 'node:path'
import tailwindcss from '@tailwindcss/vite'

// em plugins adicione
/* plugins: [react(), */ tailwindcss() /* ] */ ,

// depois de plugins, adicione
resolve: {
	alias: {
		'@': path.resolve(__dirname, './src'),
	},
},
```

5 - Atualize o **tsconfig.app.json** no compilerOptions, adicionando:

```js
// depois de
"skipLibCheck": true,
// adicione
"baseUrl": ".",
"paths": {
	"@/*": ["./src/*"]
},
```

6 - Crie um arquivo **index.css** dentro de **src** e adicione:

```css
@import 'tailwindcss';
```

7 - Importe **index.css** no **main.tsx**:

```js
// adicione
import './index.css'
```

8 - Instale a extensão do Tailwind no VSCode:  
[Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)

9 -Instale o plugin para organizar a ordem das classes no Tailwind

[Automatic Class Sorting](https://tailwindcss.com/blog/automatic-class-sorting-with-prettier)

```sh
pnpm add -D prettier-plugin-tailwindcss
```

10 - Adicione no arquivo de configuração do Prettier, **prettierrc.json**:

```js
// depois de
/* "arrowParens": "always" */,
"plugins": ["prettier-plugin-tailwindcss"]
```

11 - Para testar, adicione alguns estilos no hello world em **App.tsx**

- Veja o autocomplete funcionando dentro do className, graças a extensão.

```js
return (
	<div className='text-center'>
		<h1 className='text-3xl font-bold'>Hello World !!!</h1>
	</div>
)
```

- Veja tamtém a ordem classificação das classes, invertendo
  'font-bold text-3xl' e vendo que voltam para 'text-3xl font-bold' quando salva.

12 - Rode para verificar:

```sh
pnpm dev
```

---

### Instalação e configuração do Shadcn-UI

1 - Instale o Shadcn-UI:

```sh
pnpm dlx shadcn@latest init
```

Selecione o tom de cinza preferido:  
[ui.shadcn/colors](https://ui.shadcn.com/colors)

Gostei do mais puxado pro azul:  
✔ Slate

2 - Vá até o arquivo **index.css** e veja que foi adicionado bastante css do ShadcnUI. Percerba que contém alguns erros, para resolver adicione a extensão de PostCSS no VSCode:

[PostCSS Language Support](https://marketplace.visualstudio.com/items?itemName=csstools.postcss)

- Com isso os erros devem desaparecer.

3 - Para testar, instale um component, por exemplo o button:  
[ui.shadcn/button](https://ui.shadcn.com/docs/components/button)

```sh
pnpm dlx shadcn@latest add button
```

4 - Adicione no **App.tsx**:

```js
// adicione
import { Button } from './components/ui/button'

return (
	<div className='text-center'>
		<h1 className='text-3xl font-bold'>Hello World !!!</h1>
		/* adicione */
		<Button variant='outline'>Shadcn-UI Button</Button>
	</div>
)
```

5 - Rode para verificar:

```sh
pnpm dev
```

// Adicionar
https://tailwindcss.com/blog/automatic-class-sorting-with-prettier
