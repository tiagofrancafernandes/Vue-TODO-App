# Todo App

[🇬🇧 English](./README.md) | 🇧🇷 Português

Uma aplicação moderna e elegante de gerenciamento de tarefas construída com Vue 3, Vite e TailwindCSS v4. Esta aplicação permite criar, gerenciar e rastrear suas tarefas diárias de forma eficiente com persistência automática de dados usando o LocalStorage do navegador.

<a href="https://vercel.com/new/clone?repository-url=https://github.com/tiagofrancafernandes/Vue-TODO-App/tree/master"><img src="https://vercel.com/button"></a>


## Índice
- [Recursos](#recursos)
- [Tecnologias](#tecnologias)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Instalação](#instalação)
- [Como Usar](#como-usar)
- [Persistência de Dados](#persistência-de-dados)
- [Scripts Disponíveis](#scripts-disponíveis)
- [Configuração do TailwindCSS v4](#configuração-do-tailwindcss-v4)
- [Suporte a Navegadores](#suporte-a-navegadores)
- [Desenvolvimento](#desenvolvimento)
- [Licença](#licença)
- [Contribuindo](#contribuindo)
- [Suporte](#suporte)
- [Agradecimentos](#agradecimentos)


## Recursos

✨ **Criar Tarefas** - Adicione novas tarefas com uma interface simples e intuitiva <br>
✅ **Marcar como Completo** - Alterne o status de conclusão da tarefa com um único clique <br>
🗑️ **Deletar Tarefas** - Remova tarefas individuais da sua lista <br>
🔍 **Filtrar Tarefas** - Visualize todas as tarefas, tarefas pendentes ou tarefas completas <br>
📊 **Painel de Estatísticas** - Estatísticas em tempo real mostrando total, completas e tarefas pendentes <br>
💾 **Persistência com LocalStorage** - Todas as suas tarefas são salvas automaticamente no LocalStorage do seu navegador <br>
⌨️ **Suporte a Teclado** - Pressione Enter para adicionar rapidamente uma nova tarefa <br>
🎨 **Design Responsivo** - Interface linda e responsiva que funciona em todos os dispositivos <br>
🌈 **Estilo Moderno** - Construído com TailwindCSS v4 para um visual limpo e moderno <br>
🌓 **Tema Claro e Escuro** - Alterne entre tema claro e escuro com persistência automática <br>
✏️ **Editar Tarefas** - Edite tarefas existentes inline com suporte a teclado <br>

## Tecnologias

- **Vue 3** - Framework JavaScript progressivo com Composition API
- **Vite** - Ferramenta de build frontend de próxima geração
- **TailwindCSS v4** - Framework CSS utility-first com configuração CSS-first
- **LocalStorage API** - Persistência de dados integrada do navegador
- **JavaScript ES6+** - Recursos modernos de JavaScript

## Estrutura do Projeto

```
.
├── src/
│   ├── App.vue           # Componente principal com toda a lógica
│   ├── main.js           # Ponto de entrada da aplicação
│   ├── style.css         # Estilos globais com import do TailwindCSS
│   └── assets/           # Arquivos estáticos (imagens, etc.)
├── vite.config.js        # Configuração do Vite com plugin TailwindCSS
├── index.html            # Ponto de entrada HTML
└── package.json          # Dependências do projeto
```

## Instalação

### Pré-requisitos

- **Node.js** (v16 ou superior)
- **npm** (v7 ou superior) ou **yarn**

### Passos de Instalação

1. **Clone ou navegue até o diretório do projeto:**
   ```bash
   cd app-directory
   ```

2. **Instale as dependências:**
   ```bash
   npm install
   ```

3. **Inicie o servidor de desenvolvimento:**
   ```bash
   npm run dev
   ```

4. **Abra no seu navegador:**
   A aplicação estará disponível em `http://localhost:5174/`

## Como Usar

### Adicionando uma Tarefa
1. Digite sua tarefa no campo de entrada
2. Pressione **Enter** ou clique no botão **Add**
3. Sua tarefa aparecerá na lista e será salva automaticamente

### Concluindo uma Tarefa
- Clique na caixa de seleção ao lado de uma tarefa para marcá-la como concluída
- Tarefas completas serão exibidas com um risco

### Deletando uma Tarefa
- Clique no botão **Delete** em qualquer tarefa para removê-la da sua lista

### Editando uma Tarefa
- Clique no botão **Edit** em uma tarefa para editá-la inline
- Pressione **Enter** para salvar ou **Escape** para cancelar

### Filtrando Tarefas
- Use os botões de filtro para visualizar:
  - **All** - Todas as tarefas (padrão)
  - **Pending** - Apenas tarefas incompletas
  - **Completed** - Apenas tarefas completas

### Limpando Tarefas Completas
- Quando você tem tarefas completas, um botão **Clear Completed Tasks** aparece
- Clique nele para remover todas as tarefas completas de uma vez

### Alternando Tema
- Use o botão com ícone de sol/lua no canto superior direito para alternar entre modo claro e escuro
- Sua preferência de tema é salva automaticamente

## Persistência de Dados

Esta aplicação usa a **LocalStorage API** do navegador para persistir suas tarefas. Seus dados são armazenados localmente em seu dispositivo e estarão disponíveis quando você:
- Atualizar a página
- Fechar e reabrir o navegador
- Retornar à aplicação mais tarde

**Nota:** LocalStorage é específico do navegador. Tarefas salvas no Chrome não aparecerão no Firefox ou Safari.

## Scripts Disponíveis

### Servidor de Desenvolvimento
```bash
npm run dev
```
Inicia o servidor de desenvolvimento do Vite com recarregamento de módulo quente (HMR)

### Build para Produção
```bash
npm run build
```
Cria um build otimizado para produção no diretório `dist/`

### Preview do Build de Produção
```bash
npm run preview
```
Visualiza o build de produção localmente

## Configuração do TailwindCSS v4

Este projeto usa TailwindCSS v4 com Vite, o que significa:
- ✅ **Nenhum arquivo de configuração necessário** - A configuração é CSS-first
- ✅ **Import único** - Apenas `@import "tailwindcss"` no seu CSS
- ✅ **Processamento automático** - O plugin do Vite cuida de toda a geração de CSS
- ✅ **Bundle menor** - Inclui apenas os estilos que você realmente usa

## Suporte a Navegadores

Esta aplicação funciona em todos os navegadores modernos que suportam:
- JavaScript ES6+
- LocalStorage API
- CSS Grid e Flexbox

Navegadores suportados:
- Chrome/Edge (versão recente)
- Firefox (versão recente)
- Safari (versão recente)
- Opera (versão recente)

## Desenvolvimento

### Estilo de Código

Este projeto segue as melhores práticas de Vue 3 e JavaScript:
- **Composition API** para lógica de componentes
- **Referências reativas** usando `ref()` e `computed()`
- **Hooks de ciclo de vida** como `onMounted()`
- **Estilos com escopo de componente** com `<style scoped>`

### Melhorias Futuras

Possíveis melhorias para versões futuras:
- Sincronização em nuvem (Firebase, Supabase)
- Autenticação e contas de usuário
- Categorias ou tags de tarefas
- Datas de vencimento e lembretes
- Funcionalidade de exportação de tarefas
- Reordenação com arrastar e soltar

## Licença

Este projeto é de código aberto e está disponível sob a Licença MIT.

## Contribuindo

Sinta-se livre para fazer um fork deste projeto e enviar pull requests para qualquer melhoria ou correção de bug.

## Suporte

Se você encontrar problemas ou tiver dúvidas sobre a aplicação, crie um issue no repositório do projeto.

---

**Feliz gerenciamento de tarefas!** ✨

### Agradecimentos

- [Vercel](https://vercel.com)
- [Vue 3](https://vuejs.org/)
- [Vite](https://vitejs.dev/)
- [TailwindCSS v4](https://tailwindcss.com/)
