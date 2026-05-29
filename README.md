<<<<<<< HEAD
# SIGA FATEC - Sistema Integrado de Gestão Acadêmica

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Arquitetura](#arquitetura)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Pré-requisitos](#pré-requisitos)
- [Instalação e Configuração](#instalação-e-configuração)
- [Como Executar](#como-executar)
- [Como Testar](#como-testar)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Funcionalidades Implementadas](#funcionalidades-implementadas)
- [Integração Backend-Frontend](#integração-backend-frontend)
- [Documentação Adicional](#documentação-adicional)

---

## 🎯 Sobre o Projeto

O **SIGA FATEC** é um sistema completo de gestão acadêmica composto por:

- **Aplicativo Mobile** (`frontend`): Aplicativo React Native com Expo para estudantes acessarem suas informações acadêmicas
- **Backend API** (`backend`): API RESTful Node.js/Express com MongoDB para gerenciar dados acadêmicos

### Objetivo

Fornecer aos estudantes da FATEC uma experiência mobile moderna e intuitiva para:

- Consultar notas e médias
- Acompanhar frequência e faltas
- Visualizar disciplinas e professores
- Gerenciar atividades acadêmicas (provas, trabalhos)
- Acessar informações do perfil e progresso do curso

### Problema Resolvido

O sistema SIGA tradicional não é otimizado para dispositivos móveis, resultando em:

- Navegação complexa e lenta
- Falta de notificações em tempo real
- Interface desatualizada
- Dificuldade para consultas rápidas

O SIGA FATEC Mobile resolve esses problemas com uma interface nativa, rápida e intuitiva.

---

## 🏗️ Arquitetura

### Visão Geral

```
┌─────────────────────────────────────┐
│   fatec-react-native (Mobile App)   │
│   - React Native + Expo             │
│   - TypeScript                      │
│   - NativeWind (Tailwind CSS)       │
└─────────────┬───────────────────────┘
              │ HTTPS/REST
              │ JWT Authentication
┌─────────────▼───────────────────────┐
│   backend (Node.js API)             │
│   - Express.js                      │
│   - JWT Authentication              │
│   - MongoDB (Mongoose)              │
└─────────────┬───────────────────────┘
              │
┌─────────────▼───────────────────────┐
│   MongoDB Database                  │
│   - Users (Students)                │
│   - Courses                         │
│   - Subjects                        │
│   - Activities                      │
└─────────────────────────────────────┘
```

### Arquitetura em Camadas

**Frontend (Mobile)**:

- **Camada de Apresentação**: Screens e Components (React Native)
- **Camada de Serviços**: API Service, Auth Service
- **Camada de Estado**: Custom Hooks (useStudent, useActivities)

**Backend (API)**:

- **Camada de Rotas**: Express Routes
- **Camada de Middleware**: Auth, Error Handling
- **Camada de Controllers**: Business Logic
- **Camada de Modelos**: Mongoose Models

---

## 🚀 Tecnologias Utilizadas

### Frontend (fatec-react-native)

| Tecnologia              | Versão | Propósito                        |
| ----------------------- | ------ | -------------------------------- |
| React Native            | 0.81.4 | Framework mobile multiplataforma |
| Expo                    | 54.0.0 | Plataforma de desenvolvimento    |
| TypeScript              | 5.9.2  | Tipagem estática                 |
| NativeWind              | 4.2.1  | Tailwind CSS para React Native   |
| Expo Router             | 6.0.12 | Navegação baseada em arquivos    |
| Axios                   | 1.13.2 | Cliente HTTP para API            |
| React Native Reanimated | 4.1.1  | Animações de alta performance    |
| AsyncStorage            | 2.2.0  | Armazenamento local              |

### Backend (siga-backend)

| Tecnologia | Propósito               |
| ---------- | ----------------------- |
| Node.js    | Runtime JavaScript      |
| Express.js | Framework web           |
| MongoDB    | Banco de dados NoSQL    |
| Mongoose   | ODM para MongoDB        |
| JWT        | Autenticação via tokens |
| Bcrypt     | Hash de senhas          |
| Docker     | Containerização         |

---

## 📦 Pré-requisitos

### Para o Frontend (Mobile)

- **Node.js** 18+ ([Download](https://nodejs.org/))
- **npm** ou **yarn**
- **Expo Go** app no seu smartphone ([iOS](https://apps.apple.com/app/expo-go/id982107779) | [Android](https://play.google.com/store/apps/details?id=host.exp.exponent))

### Para o Backend

- **Docker** e **Docker Compose** ([Download](https://www.docker.com/products/docker-desktop/))
- **Git** ([Download](https://git-scm.com/))

---

## ⚙️ Instalação e Configuração

### 1. Clone o Repositório

```bash
git clone <url-do-repositorio>
cd <nome-do-repositorio>
```

### 2. Configuração do Backend

#### 2.1. Navegue até a pasta do backend

```bash
cd siga-backend
```

#### 2.2. Configure as variáveis de ambiente

O arquivo `.env` já existe em `backend/api/.env` com as seguintes configurações:

```env
MONGODB_URI=mongodb+srv://dbSigaUser:fatec%401234@siga-cluster.3gwcvxy.mongodb.net/siga?retryWrites=true&w=majority&appName=siga-cluster
JWT_SECRET=fatec1234
```

> **Nota**: Para produção, altere o `JWT_SECRET` para um valor mais seguro.

#### 2.3. Inicie os containers Docker

```bash
docker-compose up --build
```

Aguarde até ver as mensagens:

```
backend_app | Servidor rodando na porta 3000
backend_app | MongoDB conectado com sucesso
frontend_server | Serving "/app" at http://0.0.0.0:5500
```

**Serviços disponíveis**:

- Backend API: `http://localhost:3000`
- Frontend de testes: `http://localhost:5500`
- MongoDB: `localhost:27017`

### 3. Configuração do Frontend (Mobile)

#### 3.1. Abra um novo terminal e navegue até a pasta do frontend

```bash
cd fatec-react-native
```

#### 3.2. Instale as dependências

```bash
npm install
```

#### 3.3. Configure as variáveis de ambiente

Crie um arquivo `.env` baseado no `.env.example`:

```bash
cp .env.example .env
```

Edite o arquivo `.env`:

```env
# Para desenvolvimento local (backend rodando no Docker)
EXPO_PUBLIC_API_URL=http://localhost:3000

# Para testar em dispositivo físico, use o IP da sua máquina
# EXPO_PUBLIC_API_URL=http://192.168.1.100:3000
```

> **Importante**: Se você for testar no Expo Go em um dispositivo físico, substitua `localhost` pelo IP local da sua máquina (ex: `192.168.1.100`).

---

## 🎮 Como Executar

### Backend

Se ainda não estiver rodando:

```bash
cd siga-backend
docker-compose up
```

Para parar os containers:

```bash
docker-compose down
```

Para reconstruir após mudanças:

```bash
docker-compose up --build
```

### Frontend (Mobile)

#### Opção 1: Expo Go (Recomendado para desenvolvimento)

```bash
cd fatec-react-native
npm run dev
```

Isso abrirá o Expo DevTools. Você pode:

- Escanear o QR code com o app **Expo Go** no seu smartphone
- Pressionar `a` para abrir no emulador Android
- Pressionar `i` para abrir no simulador iOS (apenas Mac)
- Pressionar `w` para abrir no navegador web

#### Opção 2: Emuladores

**Android**:

```bash
npm run android
```

**iOS** (apenas Mac):

```bash
npm run ios
```

**Web**:

```bash
npm run web
```

---

## 🧪 Como Testar

### Testes do Backend

```bash
cd backend/api
npm test
```

Os testes incluem:

- Testes de integração dos endpoints
- Validação de autenticação JWT
- Cálculos de dados agregados (média, frequência)
- Mapeamento de campos

### Testes do Frontend

```bash
cd fatec-react-native
npm test
```

Para executar em modo watch:

```bash
npm run test:watch
```

Para gerar relatório de cobertura:

```bash
npm run test:coverage
```

Os testes incluem:

- Testes unitários dos serviços de API
- Testes dos custom hooks (useStudent, useActivities)
- Testes de componentes React Native
- Tratamento de erros e estados de carregamento

### Teste Manual End-to-End

1. **Inicie o backend**:

   ```bash
   cd backend
   docker-compose up
   ```

2. **Inicie o frontend**:

   ```bash
   cd frontend
   npm run dev
   ```

3. **Teste o fluxo completo**:
   - Abra o app no Expo Go
   - Faça login com credenciais de teste
   - Navegue pelas telas: Dashboard, Disciplinas, Notas, Presença
   - Verifique se os dados são carregados corretamente
   - Teste estados de erro (desconecte o backend)

---

## 📁 Estrutura do Projeto

### Frontend (fatec-react-native)

```
frontend/
├── app/                      # Rotas do Expo Router
│   ├── (app)/               # Grupo de rotas autenticadas
│   │   ├── _layout.tsx      # Drawer Navigator
│   │   ├── dashboard.tsx    # Tela principal
│   │   └── disciplinas.tsx  # Lista de disciplinas
│   ├── _layout.tsx          # Layout raiz
│   └── index.tsx            # Tela de login
├── components/              # Componentes reutilizáveis
│   └── ui/                  # Componentes UI (Card, Button, etc.)
├── hooks/                   # Custom Hooks
│   ├── useStudent.ts        # Hook para dados do estudante
│   └── useActivities.ts     # Hook para atividades
├── lib/                     # Bibliotecas e utilitários
│   ├── api.ts              # Serviço de API
│   └── auth.ts             # Serviço de autenticação
├── types/                   # Definições TypeScript
│   └── student.ts          # Tipos de dados do estudante
├── data/                    # Dados mockados (desenvolvimento)
│   ├── mockStudent.ts
│   └── mockActivities.ts
├── .env                     # Variáveis de ambiente
├── .env.example            # Exemplo de configuração
├── package.json            # Dependências
└── tsconfig.json           # Configuração TypeScript
```

### Backend (siga-backend)

```
backend/
├── api/
│   ├── config/             # Configurações (DB, etc.)
│   ├── controllers/        # Lógica de negócios
│   │   ├── studentController.js
│   │   └── activityController.js
│   ├── middlewares/        # Middlewares (auth, error)
│   │   └── auth.js
│   ├── models/             # Modelos Mongoose
│   │   ├── User.js
│   │   ├── Course.js
│   │   ├── Subject.js
│   │   └── Activity.js
│   ├── routes/             # Rotas da API
│   │   ├── authRoutes.js
│   │   ├── studentRoutes.js
│   │   └── activityRoutes.js
│   ├── .env                # Variáveis de ambiente
│   ├── Dockerfile          # Dockerfile do backend
│   ├── package.json        # Dependências
│   └── server.js           # Ponto de entrada
├── api-tester/               # Interface de testes
│   ├── index.html
│   ├── css/
│   ├── js/
│   └── Dockerfile
└── docker-compose.yml      # Orquestração dos serviços
```

---

## ✨ Funcionalidades Implementadas

### Frontend (Mobile)

✅ **Autenticação**

- Login com CPF e senha
- Armazenamento seguro de token JWT
- Validação de campos

✅ **Dashboard**

- Visão geral do desempenho acadêmico
- Média geral e taxa de frequência
- Próximas atividades
- Estatísticas do curso

✅ **Disciplinas**

- Lista de todas as disciplinas matriculadas
- Detalhes: professor, código, notas, frequência
- Cards expansíveis com animações

✅ **Notas**

- Visualização de notas por disciplina
- Notas de P1, P2, Trabalhos e P3
- Cálculo de média por disciplina

✅ **Presença**

- Taxa de frequência por disciplina
- Total de aulas e faltas
- Indicadores visuais de status

✅ **Perfil**

- Informações do estudante
- Foto de perfil
- Progresso do curso
- Dados acadêmicos

### Backend (API)

✅ **Autenticação**

- `POST /api/auth/login` - Login de usuário
- JWT com expiração configurável
- Middleware de autenticação

✅ **Estudantes**

- `GET /api/student` - Dados completos do estudante autenticado
- Cálculo automático de médias e frequência
- Mapeamento de campos para formato do frontend

✅ **Atividades**

- `GET /api/activities` - Lista de atividades do estudante
- `POST /api/activities` - Criar nova atividade
- `PUT /api/activities/:id` - Atualizar atividade
- `DELETE /api/activities/:id` - Deletar atividade

✅ **Cursos e Disciplinas**

- `GET /api/courses` - Listar cursos
- `POST /api/courses` - Criar curso (admin)
- `GET /api/subjects` - Listar disciplinas
- `POST /api/subjects` - Criar disciplina (admin)

---

## 🔗 Integração Backend-Frontend

### Fluxo de Autenticação

1. Usuário insere CPF e senha no app
2. App envia `POST /api/auth/login`
3. Backend valida credenciais e retorna JWT token
4. App armazena token no AsyncStorage
5. Todas as requisições subsequentes incluem token no header `Authorization: Bearer <token>`

### Fluxo de Dados do Estudante

1. App envia `GET /api/student` com token JWT
2. Backend valida token e extrai user ID
3. Backend busca dados do usuário no MongoDB
4. Backend calcula dados agregados:
   - Média geral de todas as disciplinas
   - Taxa de frequência geral
   - Total de faltas
5. Backend mapeia campos do banco para formato do frontend
6. App recebe JSON e atualiza UI

### Formato de Resposta da API

**GET /api/student**:

```json
{
  "name": "João Silva Santos",
  "ra": "0050482311001",
  "email": "joao.santos@fatec.sp.gov.br",
  "profilePhoto": "url",
  "courseProgress": 68,
  "courseName": "Análise e Desenvolvimento de Sistemas",
  "averageGrade": 8.2,
  "attendanceRate": 95.5,
  "totalAbsences": 11,
  "totalSubjects": 5,
  "subjects": [...]
}
```

**GET /api/activities**:

```json
[
  {
    "id": "507f1f77bcf86cd799439011",
    "title": "Prova P3 - Programação Web",
    "subject": "Programação Web",
    "date": "2025-10-13",
    "type": "exam"
  }
]
```

---

## 📚 Documentação Adicional

### Documentos de Especificação

O projeto possui documentação detalhada na pasta `.kiro/specs/backend-frontend-integration/`:

- **`requirements.md`**: Requisitos funcionais e critérios de aceitação
- **`design.md`**: Arquitetura técnica detalhada, componentes e interfaces
- **`tasks.md`**: Plano de implementação com tarefas concluídas

### Contexto do Projeto

- **`GEMINI.md`**: Visão geral completa do projeto para IA
- **`integration_plan.md`**: Plano de integração entre frontend e backend

### READMEs Específicos

- **`frontend/README.md`**: Documentação completa do aplicativo mobile
- **`backend/README.md`**: Documentação completa da API

---

## 🔐 Segurança

### Práticas Implementadas

- ✅ Senhas hasheadas com bcrypt
- ✅ Autenticação JWT com expiração
- ✅ Middleware de autorização por role (aluno/admin)
- ✅ Validação de entrada de dados
- ✅ CORS configurado
- ✅ Variáveis de ambiente para segredos

### Recomendações para Produção

- [ ] Usar HTTPS obrigatório
- [ ] Implementar rate limiting
- [ ] Adicionar refresh tokens
- [ ] Configurar helmet.js para headers de segurança
- [ ] Implementar logging de auditoria
- [ ] Usar secrets manager para credenciais

---

## 🚧 Próximas Funcionalidades

- [ ] Notificações push para novas notas e atividades
- [ ] Sincronização offline com AsyncStorage
- [ ] Gráficos de desempenho acadêmico
- [ ] Calendário integrado de atividades
- [ ] Chat entre alunos e professores
- [ ] Download de documentos acadêmicos
- [ ] Autenticação biométrica (Face ID, Touch ID)

---

## 👥 Contribuindo

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/NovaFuncionalidade`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova funcionalidade'`)
4. Push para a branch (`git push origin feature/NovaFuncionalidade`)
5. Abra um Pull Request

---

## 📄 Licença

Este projeto é desenvolvido para fins acadêmicos da FATEC.

---

## 📞 Suporte

Para dúvidas ou problemas:

- Abra uma issue no repositório
- Consulte a documentação em `.kiro/specs/`
- Verifique os READMEs específicos de cada módulo

---

**Desenvolvido com ❤️ para os estudantes da FATEC**
=======
# app-fatec-cloud
>>>>>>> f052cb07a0c8c3b40350f042f0ab0d5f1a619d79
