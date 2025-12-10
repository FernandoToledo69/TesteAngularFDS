# Choose - Plataforma de Anúncios de Veículos

Plataforma web desenvolvida em Angular 21 para anúncios de veículos com comparação de preços com a tabela FIPE. A aplicação permite cadastrar, buscar e comparar preços de carros anunciados.

## 📋 Índice

- [Tecnologias](#tecnologias)
- [Estrutura de Pastas](#estrutura-de-pastas)
- [Componentes](#componentes)
- [Serviços](#serviços)
- [Modelos](#modelos)
- [Rotas e Operações](#rotas-e-operações)
- [Como Executar](#como-executar)
- [FAQ](#faq)

## 🛠 Tecnologias

- **Angular 21.0** - Framework principal
- **TypeScript 5.9** - Linguagem de programação
- **RxJS 7.8** - Programação reativa
- **Angular Signals** - Gerenciamento de estado reativo
- **Angular SSR** - Server-Side Rendering
- **Spring Boot** - Backend (servidor separado na porta 8080)

## 📁 Estrutura de Pastas

```
src/
├── app/
│   ├── components/          # Componentes reutilizáveis
│   │   ├── header/         # Cabeçalho da aplicação
│   │   └── footer/         # Rodapé da aplicação
│   │
│   ├── pages/              # Páginas/Componentes de rota
│   │   ├── home/           # Página inicial (listagem de carros)
│   │   ├── login/          # Página de login/cadastro
│   │   ├── busca/          # Página de busca de veículos
│   │   ├── carro/          # Página de detalhes do carro
│   │   └── anuncio/        # Formulário multi-passo de anúncio
│   │       ├── anuncio-passo1.ts  # Passo 1: Dados básicos
│   │       ├── anuncio-passo2.ts  # Passo 2: Fotos e placa
│   │       ├── anuncio-passo3.ts  # Passo 3: Detalhes adicionais
│   │       └── anuncio-passo4.ts  # Passo 4: Preço e finalização
│   │
│   ├── services/           # Serviços Angular (lógica de negócio)
│   │   ├── carro.service.ts        # Serviço de carros
│   │   ├── usuario.service.ts     # Serviço de usuários
│   │   └── anuncio.service.ts      # Serviço de gerenciamento de anúncio
│   │
│   ├── models/             # Interfaces TypeScript (modelos de dados)
│   │   ├── carro.model.ts         # Interface do modelo Carro
│   │   └── usuario.model.ts      # Interface do modelo Usuario
│   │
│   ├── app.config.ts       # Configuração da aplicação
│   ├── app.routes.ts       # Definição de rotas
│   └── app.ts              # Componente raiz
│
├── assets/                 # Arquivos estáticos (imagens, etc.)
└── public/                 # Arquivos públicos
```

## 🧩 Componentes

### Componentes de Página (Pages)

#### 1. **Home** (`pages/home/`)

- **Rota**: `/`
- **Descrição**: Página inicial que exibe a listagem de todos os carros cadastrados
- **Funcionalidades**:
  - Lista carros do servidor via `CarroService`
  - Exibe cards com informações básicas (imagem, nome, preço, tags)
  - Navegação para detalhes do carro
  - Estados de loading e erro

#### 2. **Login** (`pages/login/`)

- **Rota**: `/login`
- **Descrição**: Página de autenticação e cadastro de usuários
- **Funcionalidades**:
  - Formulário reativo com validação
  - Cadastro de novos usuários via `UsuarioService`
  - Validação de email e senha

#### 3. **Busca** (`pages/busca/`)

- **Rota**: `/busca?categoria=...&termo=...`
- **Descrição**: Página de busca de veículos por categoria ou termo
- **Funcionalidades**:
  - Busca por termo (modelo do carro)
  - Busca por categoria
  - Filtragem de resultados
  - Estados de loading e erro

#### 4. **Carro** (`pages/carro/`)

- **Rota**: `/carro/:id`
- **Descrição**: Página de detalhes completos de um carro específico
- **Funcionalidades**:
  - Exibe informações detalhadas do carro
  - Galeria de imagens
  - Comparação com preço FIPE
  - Tags e descrição completa
  - Informações de contato

#### 5. **Anúncio - Passo 1** (`pages/anuncio/anuncio-passo1/`)

- **Rota**: `/anuncio/passo-1`
- **Descrição**: Primeiro passo do formulário de anúncio - Dados básicos
- **Campos**: Tipo de veículo, modelo, ano, versão, câmbio, potência, portas

#### 6. **Anúncio - Passo 2** (`pages/anuncio/anuncio-passo2/`)

- **Rota**: `/anuncio/passo-2`
- **Descrição**: Segundo passo - Fotos e placa do veículo
- **Campos**: Upload de fotos, placa do veículo

#### 7. **Anúncio - Passo 3** (`pages/anuncio/anuncio-passo3/`)

- **Rota**: `/anuncio/passo-3`
- **Descrição**: Terceiro passo - Detalhes adicionais
- **Campos**: Quilometragem, cor, informações adicionais, descrição, tags

#### 8. **Anúncio - Passo 4** (`pages/anuncio/anuncio-passo4/`)

- **Rota**: `/anuncio/passo-4`
- **Descrição**: Quarto passo - Preço e finalização
- **Funcionalidades**:
  - Definição do preço
  - Comparação com tabela FIPE
  - Finalização e cadastro do anúncio

### Componentes Reutilizáveis (Components)

#### 1. **Header** (`components/header/`)

- **Descrição**: Cabeçalho da aplicação presente em todas as páginas
- **Funcionalidades**:
  - Logo/nome da aplicação
  - Menu de navegação
  - Links para páginas principais

#### 2. **Footer** (`components/footer/`)

- **Descrição**: Rodapé da aplicação presente em todas as páginas
- **Funcionalidades**:
  - Informações de contato
  - Links úteis
  - Copyright

## 🔧 Serviços

### 1. **CarroService** (`services/carro.service.ts`)

Gerencia todas as operações relacionadas a carros.

**Métodos disponíveis:**

- `cadastrarCarro(carro: Carro): Observable<string>`

  - **Endpoint**: `POST /carros/cadastrar`
  - **Descrição**: Cadastra um novo carro no servidor
  - **Retorno**: Mensagem de sucesso

- `listarCarros(): Observable<Carro[]>`

  - **Endpoint**: `GET /carros/listar`
  - **Descrição**: Lista todos os carros cadastrados
  - **Retorno**: Array de carros

- `buscarCarro(modelo: string): Observable<Carro | null>`

  - **Endpoint**: `GET /carros/buscar/{modelo}`
  - **Descrição**: Busca um carro específico pelo modelo
  - **Retorno**: Carro encontrado ou null

- `compararPreco(modelo: string): Observable<string>`
  - **Endpoint**: `GET /carros/comparar/{modelo}`
  - **Descrição**: Compara o preço do anúncio com a tabela FIPE
  - **Retorno**: String formatada com comparação e recomendação

**Tratamento de erros**: Inclui tratamento completo de erros HTTP, conexão e SSR.

### 2. **UsuarioService** (`services/usuario.service.ts`)

Gerencia todas as operações relacionadas a usuários.

**Métodos disponíveis:**

- `cadastrarUsuario(usuario: Usuario): Observable<string>`

  - **Endpoint**: `POST /usuarios/cadastrar`
  - **Descrição**: Cadastra um novo usuário
  - **Retorno**: Mensagem de sucesso

- `listarUsuarios(): Observable<Usuario[]>`

  - **Endpoint**: `GET /usuarios/listar`
  - **Descrição**: Lista todos os usuários cadastrados
  - **Retorno**: Array de usuários

- `deletarUsuario(nick: string, usuario: Usuario): Observable<string>`

  - **Endpoint**: `DELETE /usuarios/deletar/{nick}`
  - **Descrição**: Deleta um usuário pelo nick
  - **Retorno**: Mensagem de sucesso

- `editarUsuario(nick: string, usuario: Usuario): Observable<string>`
  - **Endpoint**: `PUT /usuarios/editar/{nick}`
  - **Descrição**: Atualiza os dados de um usuário
  - **Retorno**: Mensagem de sucesso

**Tratamento de erros**: Inclui tratamento completo de erros HTTP e conexão.

### 3. **AnuncioService** (`services/anuncio.service.ts`)

Gerencia o estado do formulário de anúncio multi-passo usando Angular Signals.

**Métodos disponíveis:**

- `setDadosPasso1(dados: Partial<Carro>): void`

  - **Descrição**: Armazena dados do passo 1

- `setDadosPasso2(dados: Partial<Carro>): void`

  - **Descrição**: Armazena dados do passo 2

- `setDadosPasso3(dados: Partial<Carro>): void`

  - **Descrição**: Armazena dados do passo 3

- `setDadosPasso4(dados: Partial<Carro>): void`

  - **Descrição**: Armazena dados do passo 4

- `getDadosAnuncio(): Signal<Partial<Carro>>`

  - **Descrição**: Retorna signal read-only com todos os dados coletados

- `limparDados(): void`
  - **Descrição**: Limpa todos os dados do anúncio

**Características**:

- Usa Angular Signals para reatividade
- Mantém dados entre navegações dos passos
- Permite acesso reativo aos dados em qualquer componente

## 📊 Modelos

### 1. **Carro** (`models/carro.model.ts`)

Interface que representa um carro na aplicação.

```typescript
interface Carro {
  modelo: string;
  marca: string;
  versao: string;
  cor: string;
  quilometragem: number;
  ano: number;
  preco: number;
  cambio: string;
  quantidadeDePortas: number;
  potenciaMotor: string | null;
}
```

### 2. **Usuario** (`models/usuario.model.ts`)

Interface que representa um usuário na aplicação.

```typescript
interface Usuario {
  nick: string;
  nome: string;
  email: string;
  senha: string;
}
```

## 🗺 Rotas e Operações

### Rotas Disponíveis

| Rota               | Componente       | Descrição                             |
| ------------------ | ---------------- | ------------------------------------- |
| `/`                | `Home`           | Página inicial com listagem de carros |
| `/login`           | `Login`          | Página de login/cadastro              |
| `/busca`           | `Busca`          | Página de busca de veículos           |
| `/carro/:id`       | `CarroComponent` | Detalhes de um carro específico       |
| `/anuncio/passo-1` | `AnuncioPasso1`  | Formulário passo 1                    |
| `/anuncio/passo-2` | `AnuncioPasso2`  | Formulário passo 2                    |
| `/anuncio/passo-3` | `AnuncioPasso3`  | Formulário passo 3                    |
| `/anuncio/passo-4` | `AnuncioPasso4`  | Formulário passo 4                    |
| `/**`              | -                | Redireciona para home (404)           |

### Lazy Loading

Todas as rotas utilizam **lazy loading** para melhor performance:

```typescript
{
  path: 'carro/:id',
  loadComponent: () => import('./pages/carro/carro').then((m) => m.CarroComponent),
}
```

Isso significa que cada componente só é carregado quando necessário, reduzindo o bundle inicial.

## 🚀 Como Executar

### Pré-requisitos

- Node.js 18+ e npm
- Angular CLI 21+
- Servidor Spring Boot rodando na porta 8080 (backend)

### Instalação

1. Clone o repositório:

```bash
git clone <url-do-repositorio>
cd Choose
```

2. Instale as dependências:

```bash
npm install
```

### Executar em Desenvolvimento

```bash
ng serve
```

A aplicação estará disponível em `http://localhost:4200`

### Build para Produção

```bash
npm run build
# ou
ng build
```

Os arquivos compilados estarão em `dist/Choose/browser/`

### Executar com SSR

```bash
npm run serve:ssr:Choose
```

### Executar Testes

```bash
npm test
# ou
ng test
```

## ❓ FAQ

### 1. O que é Angular Signals?

Angular Signals é uma API moderna do Angular para gerenciamento de estado reativo. No projeto, é usado no `AnuncioService` para manter os dados do formulário multi-passo sincronizados entre componentes.

**Exemplo de uso:**

```typescript
const dados = signal<Partial<Carro>>({});
dados.update((atual) => ({ ...atual, ...novosDados }));
```

### 2. Por que usar lazy loading nas rotas?

Lazy loading melhora a performance inicial da aplicação, carregando componentes apenas quando necessário. Isso reduz o tamanho do bundle inicial e melhora o tempo de carregamento.

### 3. Como funciona o formulário multi-passo?

O formulário de anúncio é dividido em 4 passos. O `AnuncioService` usa Signals para armazenar os dados de cada passo. Quando o usuário navega entre os passos, os dados são preservados. No passo 4, todos os dados são consolidados e enviados ao servidor.

### 4. O que fazer se o servidor não estiver rodando?

A aplicação exibirá mensagens de erro amigáveis quando não conseguir conectar ao servidor. Certifique-se de que o servidor Spring Boot está rodando na porta 8080 antes de usar a aplicação.

### 5. Como adicionar um novo endpoint?

1. Adicione o método no serviço correspondente (`CarroService` ou `UsuarioService`)
2. Use `HttpClient` para fazer a requisição
3. Adicione tratamento de erros com `catchError`
4. Retorne um `Observable` tipado

**Exemplo:**

```typescript
novoMetodo(param: string): Observable<TipoRetorno> {
  return this.http
    .get<TipoRetorno>(`${this.apiUrl}/novo-endpoint/${param}`)
    .pipe(catchError(this.handleError));
}
```

### 6. Como funciona a comparação com FIPE?

O endpoint `/carros/comparar/{modelo}` retorna uma string formatada com:

- Preço do anúncio
- Preço na tabela FIPE
- Diferença de preço
- Recomendação de compra

A aplicação exibe essas informações na página de detalhes do carro.

### 7. Por que usar `ChangeDetectionStrategy.OnPush`?

`OnPush` melhora a performance ao reduzir verificações desnecessárias de mudanças. É usado em todos os componentes que utilizam Signals, pois Signals notificam automaticamente quando há mudanças.

### 8. Como funciona o tratamento de erros?

Todos os serviços implementam um método `handleError` que:

- Detecta erros de conexão (status 0)
- Trata erros HTTP (404, 500, etc.)
- É compatível com SSR (não usa APIs do browser)
- Retorna mensagens de erro amigáveis

### 9. Onde estão os assets (imagens)?

Os assets estão em `src/assets/` e são servidos através da configuração em `angular.json`. As imagens são referenciadas como `/assets/nome-imagem.jpg`.

### 10. Como adicionar uma nova página?

1. Crie a pasta do componente em `src/app/pages/`
2. Crie os arquivos `.ts`, `.html` e `.css`
3. Adicione a rota em `src/app/app.routes.ts`:

```typescript
{
  path: 'nova-pagina',
  loadComponent: () => import('./pages/nova-pagina/nova-pagina').then((m) => m.NovaPagina),
}
```

## 📝 Notas Importantes

- **Backend**: A aplicação requer um servidor Spring Boot rodando em `http://localhost:8080`
- **CORS**: O servidor backend precisa estar configurado para aceitar requisições do Angular (porta 4200)
- **SSR**: A aplicação suporta Server-Side Rendering, mas está temporariamente desabilitado para debug
- **Signals**: Todos os componentes usam Angular Signals para estado reativo
- **TypeScript**: O projeto usa TypeScript strict mode para maior segurança de tipos

## 🤝 Contribuindo

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT.

---

**Desenvolvido com ❤️ usando Angular 21**
