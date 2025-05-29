 📋 Sistema de Controle de Tarefas

> Sistema completo para gerenciamento de tarefas em equipes de desenvolvimento de software

## 📖 Descrição do Projeto

O **Sistema de Controle de Tarefas** é uma aplicação web full-stack desenvolvida para atender às necessidades de uma fábrica de software na organização e controle das tarefas dos times de desenvolvimento. O sistema oferece funcionalidades diferenciadas para gerentes e colaboradores, permitindo um fluxo de trabalho eficiente e organizado.

## 🎯 Funcionalidades Implementadas

### 👨‍💼 **Funcionalidades do Gerente:**
- ✅ **Gerenciamento de Tarefas**: Criar, editar e excluir tarefas
- ✅ **Gerenciamento de Colaboradores**: Cadastrar e remover colaboradores
- ✅ **Gerenciamento de Categorias**: Criar, editar e excluir categorias com cores personalizadas
- ✅ **Atribuição de Tarefas**: Associar tarefas específicas a colaboradores
- ✅ **Visualização Completa**: Acesso a todas as tarefas, colaboradores e categorias
- ✅ **Dashboard Executivo**: Estatísticas e métricas em tempo real

### 👩‍💻 **Funcionalidades do Colaborador:**
- ✅ **Consulta de Tarefas**: Visualizar tarefas atribuídas
- ✅ **Atualização de Status**: Alterar status das próprias tarefas
- ✅ **Filtros Personalizados**: Filtrar tarefas por categoria e status

### 🔍 **Funcionalidades Compartilhadas:**
- ✅ **Sistema de Filtros**: Filtrar tarefas por colaborador, categoria e status
- ✅ **Interface Responsiva**: Design adaptável a diferentes dispositivos
- ✅ **Notificações**: Feedback visual para todas as operações
- ✅ **Autenticação Segura**: Sistema de login com controle de acesso baseado em papéis

## 🏗️ Arquitetura do Sistema

```
📁 Projeto
├── 🔗 shared/          # Schemas e tipos compartilhados
├── ⚙️ server/          # Backend - API REST
│   ├── index.ts        # Servidor Express
│   ├── routes.ts       # Rotas da API
│   ├── storage.ts      # Sistema de armazenamento
│   └── vite.ts         # Configuração Vite
├── 🎨 client/          # Frontend - React SPA
│   └── src/
│       ├── components/ # Componentes reutilizáveis
│       ├── pages/      # Páginas da aplicação
│       ├── hooks/      # Hooks customizados
│       └── lib/        # Utilitários
└── 📋 package.json     # Dependências do projeto
```

## 🛠️ Tecnologias Utilizadas

### **Backend:**
- **Node.js** + **Express.js** - Servidor web
- **TypeScript** - Linguagem de programação
- **Zod** - Validação de dados
- **Drizzle ORM** - Modelagem de dados

### **Frontend:**
- **React 18** - Biblioteca de interface
- **TypeScript** - Linguagem de programação
- **Wouter** - Roteamento
- **TanStack Query** - Gerenciamento de estado servidor
- **React Hook Form** - Gerenciamento de formulários
- **Tailwind CSS** - Estilização
- **shadcn/ui** - Componentes de interface

### **Ferramentas de Desenvolvimento:**
- **Vite** - Build tool e dev server
- **ESBuild** - Transpilação rápida

## 📊 Modelo de Dados

### **Entidades Principais:**

```typescript
// 👤 Usuários
interface User {
  id: number;
  username: string;
  password: string;
  name: string;
  role: 'manager' | 'collaborator';
}

// 🏷️ Categorias
interface Category {
  id: number;
  name: string;
  color: string;
}

// ✅ Tarefas
interface Task {
  id: number;
  title: string;
  description?: string;
  status: 'pending' | 'in-progress' | 'completed';
  assigneeId?: number;
  categoryId?: number;
  dueDate?: string;
  createdBy: number;
}
```

## 🚀 Instruções para Execução

### **Pré-requisitos:**
- Node.js 18+ instalado
- NPM ou Yarn como gerenciador de pacotes

### **1. Instalação das Dependências:**
```bash
npm install
```

### **2. Executar o Projeto:**
```bash
npm run dev
```

### **3. Acessar a Aplicação:**
- Abra o navegador e acesse: `http://localhost:5000`

## 🔐 Credenciais de Acesso

### **Gerente (Acesso Completo):**
- **Usuário:** `admin`
- **Senha:** `admin123`

### **Colaboradores:**
- **Usuário:** `maria` | **Senha:** `maria123`
- **Usuário:** `pedro` | **Senha:** `pedro123`
- **Usuário:** `ana` | **Senha:** `ana123`

## 🎮 Como Usar o Sistema

### **Para Gerentes:**
1. **Login** como administrador
2. **Dashboard** - Visualize estatísticas gerais
3. **Criar Tarefa** - Use o botão "Nova Tarefa" ou menu lateral
4. **Gerenciar Colaboradores** - Acesse "Colaboradores" no menu
5. **Gerenciar Categorias** - Acesse "Categorias" no menu
6. **Filtrar Tarefas** - Use os filtros no dashboard

### **Para Colaboradores:**
1. **Login** com credenciais de colaborador
2. **Visualizar Tarefas** - Veja apenas tarefas atribuídas a você
3. **Atualizar Status** - Clique no dropdown de status na tabela
4. **Filtrar** - Use filtros por categoria e status

## 📋 Operações CRUD Implementadas

### **Usuários/Colaboradores:**
- ✅ **Create**: Cadastro de novos colaboradores
- ✅ **Read**: Listagem de todos os colaboradores
- ✅ **Update**: Edição de dados (implementado na estrutura)
- ✅ **Delete**: Exclusão de colaboradores

### **Categorias:**
- ✅ **Create**: Criação de novas categorias
- ✅ **Read**: Listagem de todas as categorias
- ✅ **Update**: Edição de categorias existentes
- ✅ **Delete**: Exclusão de categorias

### **Tarefas:**
- ✅ **Create**: Criação de novas tarefas
- ✅ **Read**: Listagem e consulta de tarefas
- ✅ **Update**: Edição completa e atualização de status
- ✅ **Delete**: Exclusão de tarefas

## 🔄 APIs Disponíveis

### **Autenticação:**
- `POST /api/auth/login` - Login do usuário

### **Colaboradores:**
- `GET /api/collaborators` - Listar colaboradores
- `POST /api/collaborators` - Criar colaborador
- `DELETE /api/collaborators/:id` - Excluir colaborador

### **Categorias:**
- `GET /api/categories` - Listar categorias
- `POST /api/categories` - Criar categoria
- `PUT /api/categories/:id` - Atualizar categoria
- `DELETE /api/categories/:id` - Excluir categoria

### **Tarefas:**
- `GET /api/tasks` - Listar todas as tarefas
- `GET /api/tasks/assignee/:id` - Tarefas por colaborador
- `POST /api/tasks` - Criar tarefa
- `PUT /api/tasks/:id` - Atualizar tarefa
- `PATCH /api/tasks/:id/status` - Atualizar status
- `DELETE /api/tasks/:id` - Excluir tarefa

### **Estatísticas:**
- `GET /api/stats` - Estatísticas do dashboard

## 🎨 Recursos de Interface

- **Design Responsivo** - Funciona em desktop, tablet e mobile
- **Modo Escuro** - Suporte a tema escuro (preparado)
- **Componentes Modernos** - Interface profissional com shadcn/ui
- **Feedback Visual** - Notificações toast para todas as ações
- **Loading States** - Indicadores de carregamento
- **Validação de Formulários** - Validação em tempo real
- **Filtros Dinâmicos** - Filtros com atualização automática

## 🔒 Segurança e Validação

- **Validação de Dados** - Schemas Zod em frontend e backend
- **Controle de Acesso** - Permissões baseadas em papéis
- **Sanitização** - Dados limpos antes do armazenamento
- **Tratamento de Erros** - Mensagens amigáveis ao usuário

## 🚀 Próximos Passos (Melhorias Futuras)

- 🗄️ **Banco de Dados Persistente** - Migração para PostgreSQL
- 🔐 **Autenticação JWT** - Tokens seguros
- 📧 **Notificações** - Email/SMS para deadlines
- 📊 **Relatórios** - Dashboards avançados
- 🔍 **Busca Avançada** - Filtros mais complexos
- 📱 **App Mobile** - Versão para dispositivos móveis

## 👥 Equipe de Desenvolvimento

Este projeto foi desenvolvido seguindo as melhores práticas de desenvolvimento web moderno, com foco em:
- **Código limpo e organizadado**
- **Arquitetura escalável**
- **Experiência do usuário intuitiva**
- **Performance otimizada**

---

## 📞 Suporte

Para dúvidas ou problemas:
1. Verifique se todas as dependências foram instaladas
2. Confirme que o Node.js 18+ está instalado
3. Execute `npm run dev` e acesse `http://localhost:5000`
