
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
