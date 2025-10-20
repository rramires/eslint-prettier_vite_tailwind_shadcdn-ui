
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
