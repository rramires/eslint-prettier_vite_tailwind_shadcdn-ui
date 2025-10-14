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



