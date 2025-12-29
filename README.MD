# Mega Man Robots API

![Mega Man Robots API](./_docs/assets/mega-man-pixel-art.png)

A Gamer API to return Mega Man games metadata.

![Latest Release](https://img.shields.io/github/v/release/fhcmartins/MegaApiDotnetCore)
![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)
![.NET Core](https://img.shields.io/badge/.NET-Core-512BD4?style=flat&logo=.net)

---

## 📋 Índice

- [Visão Geral](#visão-geral)
- [Características](#características)
- [Tecnologias](#tecnologias)
- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
- [Uso](#uso)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Endpoints da API](#endpoints-da-api)
- [Desenvolvimento](#desenvolvimento)
- [Testes](#testes)
- [Contribuição](#contribuição)
- [Licença](#licença)

---

## 🎮 Visão Geral

**MegaApiDotnetCore** é uma API RESTful desenvolvida em **.NET Core** que fornece metadados de jogos da série Mega Man. Este projeto demonstra como a **IA pode facilitar e aprimorar a criação de documentações técnicas** claras, organizadas e profissionais para projetos de software.

### Objetivo

Mostrar na prática como ferramentas de IA podem ser utilizadas para:
- 📝 Gerar documentação técnica de qualidade
- 🎯 Estruturar projetos de forma padronizada
- 🚀 Otimizar o processo de onboarding de novos desenvolvedores
- 💡 Manter consistência em documentações de múltiplos projetos

---

## ✨ Características

- ✅ **API RESTful completa** com endpoints para consulta de dados de Mega Man
- ✅ **Modelo de dados estruturado** com suporte a filtros e paginação
- ✅ **Documentação Swagger/OpenAPI** integrada
- ✅ **Tratamento robusto de erros** com mensagens padronizadas
- ✅ **CORS habilitado** para acesso de múltiplas origens
- ✅ **Logging estruturado** para rastreamento de requisições
- ✅ **Validação de entrada** com FluentValidation
- ✅ **Testes unitários** com xUnit
- ✅ **Integração com CI/CD** via GitHub Actions
- ✅ **Containerização** com Docker

---

## 🛠 Tecnologias

| Tecnologia | Versão | Propósito |
|-----------|--------|----------|
| **.NET Core** | 6.0+ | Framework principal |
| **ASP.NET Core** | 6.0+ | Construção de APIs web |
| **Entity Framework Core** | 6.0+ | ORM para acesso a dados |
| **Swagger/OpenAPI** | 3.0+ | Documentação da API |
| **FluentValidation** | 11.0+ | Validação de modelos |
| **xUnit** | 2.4+ | Framework de testes |
| **Serilog** | 2.10+ | Logging estruturado |
| **Docker** | Latest | Containerização |
| **PostgreSQL** | 14+ | Banco de dados (opcional) |

---

## 📦 Pré-requisitos

Antes de começar, certifique-se de ter instalado:

- **.NET SDK 6.0 ou superior** - [Download](https://dotnet.microsoft.com/en-us/download)
- **Visual Studio 2022** ou **Visual Studio Code** com extensão C#
- **Git** para clonar o repositório
- **Docker** (opcional, para containerização)
- **PostgreSQL** (opcional, se usar banco de dados externo)

### Verificar versão do .NET

```bash
dotnet --version
```

---

## 🚀 Instalação

### 1. Clonar o Repositório

```bash
git clone https://github.com/fhcmartins/MegaApiDotnetCore.git
cd MegaApiDotnetCore
```

### 2. Restaurar Dependências

```bash
dotnet restore
```

### 3. Configurar Banco de Dados (se necessário)

Atualize a string de conexão em `appsettings.json`:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Database=megaapi;Username=postgres;Password=your_password"
  }
}
```

### 4. Aplicar Migrations

```bash
dotnet ef database update
```

---

## 💻 Uso

### Executar a Aplicação

#### Via CLI

```bash
dotnet run --project ./src/MegaApiDotnetCore.Api
```

#### Via Visual Studio

1. Abra o projeto em Visual Studio
2. Defina `MegaApiDotnetCore.Api` como projeto de inicialização
3. Pressione `F5` ou clique em "Start Debugging"

#### Via Docker

```bash
docker build -t megaapi:latest .
docker run -p 5000:5000 megaapi:latest
```

### Acessar a API

A API estará disponível em:

- **Local**: `http://localhost:5000`
- **Swagger UI**: `http://localhost:5000/swagger`
- **API JSON**: `http://localhost:5000/swagger/v1/swagger.json`

---

## 📁 Estrutura do Projeto

```
MegaApiDotnetCore/
├── src/
│   ├── MegaApiDotnetCore.Api/              # Projeto principal da API
│   │   ├── Controllers/                    # Controladores da API
│   │   ├── Models/                         # Modelos de dados
│   │   ├── Services/                       # Serviços de negócio
│   │   ├── appsettings.json               # Configurações da aplicação
│   │   ├── Program.cs                      # Ponto de entrada
│   │   └── Startup.cs                      # Configuração de inicialização
│   │
│   ├── MegaApiDotnetCore.Domain/           # Camada de domínio
│   │   ├── Entities/                       # Entidades de domínio
│   │   ├── Interfaces/                     # Contratos
│   │   └── ValueObjects/                   # Objetos de valor
│   │
│   ├── MegaApiDotnetCore.Infra/            # Camada de infraestrutura
│   │   ├── Data/                           # Contexto do banco de dados
│   │   ├── Migrations/                     # Migrações do EF Core
│   │   └── Repositories/                   # Repositórios
│   │
│   └── MegaApiDotnetCore.Application/      # Camada de aplicação
│       ├── DTOs/                           # Data Transfer Objects
│       ├── MappingProfiles/                # Configurações de mapeamento
│       └── Services/                       # Serviços de aplicação
│
├── tests/
│   ├── MegaApiDotnetCore.Tests.Unit/       # Testes unitários
│   ├── MegaApiDotnetCore.Tests.Integration/# Testes de integração
│   └── MegaApiDotnetCore.Tests.E2E/        # Testes end-to-end
│
├── _docs/
│   ├── assets/                             # Imagens e recursos
│   ├── api.md                              # Documentação da API
│   └── architecture.md                     # Documentação da arquitetura
│
├── Dockerfile                              # Configuração Docker
├── docker-compose.yml                      # Orquestração de containers
├── MegaApiDotnetCore.sln                   # Solução Visual Studio
└── README.md                               # Este arquivo

```

---

## 🔌 Endpoints da API

### Listar Todos os Robôs

```http
GET /api/robots
```

**Resposta (200 OK)**:
```json
{
  "data": [
    {
      "id": 1,
      "name": "Fire Man",
      "game": "Mega Man 1",
      "weakTo": "Ice Slasher",
      "description": "Robot Master do Mega Man 1"
    }
  ],
  "pageNumber": 1,
  "pageSize": 10,
  "totalCount": 25
}
```

### Obter Robô por ID

```http
GET /api/robots/{id}
```

**Resposta (200 OK)**:
```json
{
  "id": 1,
  "name": "Fire Man",
  "game": "Mega Man 1",
  "weakTo": "Ice Slasher",
  "description": "Robot Master do Mega Man 1"
}
```

### Filtrar Robôs por Jogo

```http
GET /api/robots?game=Mega%20Man%202
```

**Resposta (200 OK)**:
```json
{
  "data": [
    {
      "id": 8,
      "name": "Air Man",
      "game": "Mega Man 2",
      "weakTo": "Leaf Shield",
      "description": "Robot Master do Mega Man 2"
    }
  ]
}
```

### Criar Novo Robô

```http
POST /api/robots
Content-Type: application/json

{
  "name": "Gravity Man",
  "game": "Mega Man 5",
  "weakTo": "Charge Kick",
  "description": "Robot Master do Mega Man 5"
}
```

**Resposta (201 Created)**:
```json
{
  "id": 50,
  "name": "Gravity Man",
  "game": "Mega Man 5",
  "weakTo": "Charge Kick",
  "description": "Robot Master do Mega Man 5"
}
```

### Atualizar Robô

```http
PUT /api/robots/{id}
Content-Type: application/json

{
  "name": "Gravity Man",
  "game": "Mega Man 5",
  "weakTo": "Charge Kick",
  "description": "Descrição atualizada"
}
```

**Resposta (200 OK)**:
```json
{
  "id": 50,
  "name": "Gravity Man",
  "game": "Mega Man 5",
  "weakTo": "Charge Kick",
  "description": "Descrição atualizada"
}
```

### Deletar Robô

```http
DELETE /api/robots/{id}
```

**Resposta (204 No Content)**

---

## 🔧 Desenvolvimento

### Executar em Modo Debug

```bash
dotnet run --configuration Debug --project ./src/MegaApiDotnetCore.Api
```

### Compilar o Projeto

```bash
dotnet build
```

### Verificar Problemas de Estilo de Código

```bash
dotnet format --verify-no-changes
```

### Formatar Código

```bash
dotnet format
```

---

## ✅ Testes

### Executar Todos os Testes

```bash
dotnet test
```

### Executar Testes de um Projeto Específico

```bash
dotnet test ./tests/MegaApiDotnetCore.Tests.Unit
```

### Gerar Relatório de Cobertura de Testes

```bash
dotnet test /p:CollectCoverage=true /p:CoverageFormat=lcov
```

### Exemplos de Testes

#### Teste Unitário

```csharp
[Fact]
public async Task GetRobotById_WithValidId_ReturnsRobot()
{
    // Arrange
    var robotId = 1;
    var expectedRobot = new Robot { Id = robotId, Name = "Fire Man" };
    
    // Act
    var result = await _robotService.GetRobotByIdAsync(robotId);
    
    // Assert
    Assert.NotNull(result);
    Assert.Equal(expectedRobot.Name, result.Name);
}
```

#### Teste de Integração

```csharp
[Fact]
public async Task GetRobots_ReturnsOkResult()
{
    // Arrange
    var client = _factory.CreateClient();
    
    // Act
    var response = await client.GetAsync("/api/robots");
    
    // Assert
    response.EnsureSuccessStatusCode();
    var content = await response.Content.ReadAsAsync<List<RobotDto>>();
    Assert.NotEmpty(content);
}
```

---

## 📚 Documentação Adicional

- **[Arquitetura do Projeto](./_docs/architecture.md)** - Detalhes sobre a arquitetura utilizada
- **[Guia de API](./_docs/api.md)** - Documentação completa de endpoints
- **[Variáveis de Ambiente](./_docs/environment.md)** - Configurações necessárias

---

## 🤝 Contribuição

Contribuições são bem-vindas! Para contribuir com este projeto:

1. **Faça um Fork** do repositório
2. **Crie uma branch** para sua feature (`git checkout -b feature/AmazingFeature`)
3. **Commit suas mudanças** (`git commit -m 'Add some AmazingFeature'`)
4. **Push para a branch** (`git push origin feature/AmazingFeature`)
5. **Abra um Pull Request**

### Padrões de Código

- Siga as convenções de nomenclatura do C#
- Mantenha cobertura de testes acima de 80%
- Atualize a documentação conforme necessário
- Use commits semânticos (feat:, fix:, docs:, etc.)

---

## 🐛 Relatório de Bugs

Se encontrou um bug, por favor abra uma [Issue](https://github.com/fhcmartins/MegaApiDotnetCore/issues) descrevendo:

- Comportamento observado
- Comportamento esperado
- Passos para reproduzir
- Ambiente (SO, versão do .NET, etc.)

---

## 📝 Changelog

Veja o arquivo [CHANGELOG.md](./CHANGELOG.md) para ver um histórico detalhado de mudanças.

---

## 📄 Licença

Este projeto é licenciado sob a Licença MIT - veja o arquivo [LICENSE](./LICENSE) para detalhes.

---

## 👤 Autor

**Flávio H. C. Martins**

- GitHub: [@fhcmartins](https://github.com/fhcmartins)
- LinkedIn: [Flávio Martins](https://linkedin.com/in/flavio-martins)

---

## 🙏 Agradecimentos

- Comunidade .NET Core
- Capcom pela franquia Mega Man
- Todos os contribuidores que ajudaram neste projeto

---

## 📞 Suporte

Para dúvidas ou sugestões:

- 📧 **Email**: seu-email@example.com
- 💬 **Discussions**: [GitHub Discussions](https://github.com/fhcmartins/MegaApiDotnetCore/discussions)
- 📱 **Twitter**: [@seu_usuario](https://twitter.com)

---

## 🎯 Roadmap

- [ ] Integração com GraphQL
- [ ] Suporte a múltiplas versões da API
- [ ] Autenticação e autorização JWT
- [ ] Cache distribuído com Redis
- [ ] Publicação em NuGet Package
- [ ] Integração com Azure DevOps
- [ ] Aplicativo mobile consumindo a API

---

## 📊 Estatísticas

![GitHub Repo stars](https://img.shields.io/github/stars/fhcmartins/MegaApiDotnetCore?style=social)
![GitHub forks](https://img.shields.io/github/forks/fhcmartins/MegaApiDotnetCore?style=social)
![GitHub watchers](https://img.shields.io/github/watchers/fhcmartins/MegaApiDotnetCore?style=social)

---

<div align="center">

**[⬆ Voltar ao Topo](#mega-man-robots-api)**

Feito com ❤️ para demonstrar o potencial da IA na documentação técnica

</div>
