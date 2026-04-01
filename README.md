# 🚀 API MySQL - ASP.NET Core 3.1 + Dapper + Swagger

![.NET Core](https://img.shields.io/badge/.NET%20Core-3.1-512BD4?style=flat-square&logo=dotnet)
![MySQL](https://img.shields.io/badge/MySQL-8.0+-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Dapper](https://img.shields.io/badge/Dapper-2.0-orange?style=flat-square)
![Swagger](https://img.shields.io/badge/Swagger-5.0-85EA2D?style=flat-square&logo=swagger&logoColor=black)
![VS Code](https://img.shields.io/badge/VS%20Code-Ready-007ACC?style=flat-square&logo=visualstudiocode)

## 📋 Visão Geral

**API REST** completa desenvolvida com **ASP.NET Core 3.1**, utilizando **Dapper** como micro ORM para acesso ao banco de dados **MySQL** e **Swagger** para documentação interativa da API. O projeto demonstra a implementação de uma arquitetura limpa com separação de responsabilidades através dos padrões Repository e Dependency Injection.

> **🎓 Projeto Educacional**: Demonstra as melhores práticas de desenvolvimento de APIs RESTful com .NET Core, incluindo documentação automática, acesso a dados com Dapper e integração com MySQL.

---

## 🎯 Objetivo do Projeto

Este projeto tem como objetivos:
- ✅ **Criar API RESTful** com ASP.NET Core 3.1
- ✅ **Integrar com MySQL** usando Dapper (micro ORM)
- ✅ **Documentar API** automaticamente com Swagger/OpenAPI
- ✅ **Implementar Repository Pattern** para acesso a dados
- ✅ **Aplicar Dependency Injection** nativa do .NET Core
- ✅ **Configurar VS Code** para desenvolvimento .NET
- ✅ **Seguir princípios SOLID** e Clean Architecture

---

## 🏗️ Arquitetura da Aplicação

### 📊 Estrutura em Camadas

```
┌────────────────────────────────────────────────────────────────┐
│                    ASP.NET CORE WEB API                        │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │              CAMADA DE APRESENTAÇÃO                      │  │
│  ├──────────────────────────────────────────────────────────┤  │
│  │                                                          │  │
│  │  ┌────────────────────────────────────────────────────┐  │  │
│  │  │  Controllers (API Endpoints)                       │  │  │
│  │  ├────────────────────────────────────────────────────┤  │  │
│  │  │  • PessoaController                                │  │  │
│  │  │    └─ GET /api/pessoa (Lista todas as pessoas)     │  │  │
│  │  │                                                    │  │  │
│  │  │  • WeatherForecastController                       │  │  │
│  │  │    └─ GET /weatherforecast (Exemplo)               │  │  │
│  │  └────────────────────────────────────────────────────┘  │  │
│  │                        │                                 │  │
│  │                        ▼                                 │  │
│  │  ┌────────────────────────────────────────────────────┐  │  │
│  │  │  Startup.cs (Configuração)                         │  │  │
│  │  ├────────────────────────────────────────────────────┤  │  │
│  │  │  • ConfigureServices()                             │  │  │
│  │  │    - Dependency Injection                          │  │  │
│  │  │    - Swagger Configuration                         │  │  │
│  │  │    - Controllers Registration                      │  │  │
│  │  │                                                    │  │  │
│  │  │  • Configure()                                     │  │  │
│  │  │    - Middleware Pipeline                           │  │  │
│  │  │    - Swagger UI                                    │  │  │
│  │  │    - Routing                                       │  │  │
│  │  └────────────────────────────────────────────────────┘  │  │
│  └──────────────────────────────────────────────────────────┘  │
│                               │                                │
│                               ▼                                │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │              CAMADA DE NEGÓCIO (Repository)              │  │
│  ├──────────────────────────────────────────────────────────┤  │
│  │                                                          │  │
│  │  ┌────────────────────────────────────────────────────┐  │  │
│  │  │  IPessoaRepository (Interface)                     │  │  │
│  │  ├────────────────────────────────────────────────────┤  │  │
│  │  │  IEnumerable<Pessoa> GetAll()                      │  │  │
│  │  └────────────────────────────────────────────────────┘  │  │
│  │                        │                                 │  │
│  │                        ▼                                 │  │
│  │  ┌────────────────────────────────────────────────────┐  │  │
│  │  │  PessoaRepository (Implementação)                  │  │  │
│  │  ├────────────────────────────────────────────────────┤  │  │
│  │  │  • Constructor Injection (connectionString)        │  │  │
│  │  │  • GetAll() - Dapper Query                         │  │  │
│  │  │    SELECT Codigo, Nome, Endereco                   │  │  │
│  │  │    FROM Pessoa ORDER BY Nome ASC                   │  │  │
│  │  └────────────────────────────────────────────────────┘  │  │
│  └──────────────────────────────────────────────────────────┘  │ 
│                               │                                │
│                               ▼                                │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │              CAMADA DE DADOS (Dapper + MySQL)            │  │
│  ├──────────────────────────────────────────────────────────┤  │
│  │                                                          │  │
│  │  ┌────────────────────────────────────────────────────┐  │  │
│  │  │  Dapper (Micro ORM)                                │  │  │
│  │  ├────────────────────────────────────────────────────┤  │  │
│  │  │  • Query<T>() - Mapeia SQL para objetos            │  │  │
│  │  │  • MySqlConnection - ADO.NET Provider              │  │  │
│  │  │  • IEnumerable<Pessoa> - Result Set                │  │  │
│  │  └────────────────────────────────────────────────────┘  │  │
│  │                        │                                 │  │
│  │                        ▼                                 │  │
│  │  ┌────────────────────────────────────────────────────┐  │  │
│  │  │  MySQL Database                                    │  │  │
│  │  ├────────────────────────────────────────────────────┤  │  │
│  │  │  Database: myapi                                   │  │  │
│  │  │  Table: Pessoa                                     │  │  │
│  │  │    - Codigo (INT) PK                               │  │  │
│  │  │    - Nome (VARCHAR)                                │  │  │
│  │  │    - Endereco (VARCHAR)                            │  │  │
│  │  └────────────────────────────────────────────────────┘  │  │
│  └──────────────────────────────────────────────────────────┘  │
│                                                                │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │              CAMADA DE MODELO (Domain)                   │  │
│  ├──────────────────────────────────────────────────────────┤  │
│  │  • Pessoa.cs                                             │  │
│  │    - Codigo (int)                                        │  │
│  │    - Nome (string)                                       │  │
│  │    - Endereco (string)                                   │  │
│  └──────────────────────────────────────────────────────────┘  │
│                                                                │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │              SWAGGER UI (Documentação)                   │  │
│  ├──────────────────────────────────────────────────────────┤  │
│  │  • OpenAPI Specification (v3)                            │  │
│  │  • Interactive API Documentation                         │  │
│  │  • Try It Out Feature                                    │  │
│  │  • Schema Definitions                                    │  │
│  │  • Response Examples                                     │  │
│  └──────────────────────────────────────────────────────────┘  │
└────────────────────────────────────────────────────────────────┘

         ACESSO EXTERNO
              ▲
              │
    ┌─────────┴──────────────────┐
    │   HTTP Requests            │
    │   GET /api/pessoa          │  → Lista pessoas
    │   GET /weatherforecast     │  → Previsão do tempo (exemplo)
    │   GET /swagger             │  → Documentação Swagger UI
    └────────────────────────────┘
```

### 🔧 Fluxo de Requisição

```
1. Cliente HTTP → Request GET /api/pessoa
       ↓
2. ASP.NET Core Pipeline → Routing
       ↓
3. PessoaController → Recebe requisição
       ↓
4. IPessoaRepository (DI) → Injeta implementação
       ↓
5. PessoaRepository.GetAll() → Executa query
       ↓
6. Dapper → Mapeia SQL para objetos
       ↓
7. MySqlConnection → Conecta ao banco
       ↓
8. MySQL Database → Executa SELECT
       ↓
9. Result Set → IEnumerable<Pessoa>
       ↓
10. Controller → Ok(pessoas) ou NoContent()
       ↓
11. ASP.NET Core → Serializa para JSON
       ↓
12. Cliente HTTP ← Response 200 OK + JSON
```

---

## 🛠️ Tecnologias e Recursos

### 🎯 Stack Principal

| Tecnologia | Versão | Propósito |
|------------|--------|-----------|
| **.NET Core** | 3.1 | Runtime e framework |
| **ASP.NET Core** | 3.1 | Framework web/API |
| **C#** | 8.0 | Linguagem de programação |
| **MySQL** | 8.0+ | Banco de dados relacional |
| **Dapper** | 2.0.35 | Micro ORM (Object-Relational Mapper) |
| **MySqlConnector** | 0.69.3 | ADO.NET provider para MySQL |
| **Swashbuckle** | 5.0.0 | Geração de documentação Swagger |

### 📦 Pacotes NuGet

```xml
<PackageReference Include="Dapper" Version="2.0.35" />
<PackageReference Include="MySqlConnector" Version="0.69.3" />
<PackageReference Include="Swashbuckle.AspNetCore" Version="5.0.0" />
```

### 🏛️ Padrões de Projeto

| Padrão | Implementação | Benefício |
|--------|---------------|-----------|
| **Repository Pattern** | IPessoaRepository + PessoaRepository | Abstração de acesso a dados |
| **Dependency Injection** | Constructor Injection | Desacoplamento e testabilidade |
| **RESTful API** | HTTP verbs + Resources | Padrão web amplamente adotado |
| **Separation of Concerns** | Controllers, Models, Repositories | Manutenibilidade |

---

## 📁 Estrutura do Projeto

```
web-api-mysql-master/
│
├── 📄 ApiMySql.sln                     # Solution file
├── 📄 ApiMySql.csproj                  # Projeto .NET Core 3.1
├── 📄 README.md                        # Documentação original
├── 📄 README_TECNICO.md                # Este arquivo
├── 📄 .gitignore                       # Arquivos ignorados pelo Git
│
├── 📄 Program.cs                       # Entry point da aplicação
├── 📄 Startup.cs                       # Configuração da aplicação
├── 📄 appsettings.json                 # Configurações (ConnectionString)
├── 📄 appsettings.Development.json     # Configurações de desenvolvimento
├── 📄 WeatherForecast.cs               # Modelo de exemplo
│
├── 📂 Controllers/                     # Controladores da API
│   ├── PessoaController.cs             # Endpoint /api/pessoa
│   └── WeatherForecastController.cs    # Endpoint de exemplo
│
├── 📂 Model/                           # Modelos de domínio
│   └── Pessoa.cs                       # Entidade Pessoa
│
├── 📂 Repository/                      # Camada de acesso a dados
│   ├── IPessoaRepository.cs            # Interface do repositório
│   └── PessoaRepository.cs             # Implementação com Dapper
│
├── 📂 Properties/                      # Propriedades do projeto
│   └── launchSettings.json             # Configurações de execução
│
├── 📂 .vscode/                         # Configurações VS Code
│   ├── launch.json                     # Debug configuration
│   └── tasks.json                      # Build tasks
│
└── 📂 images/                          # Imagens da documentação
    ├── Introduction.png
    └── Swagger.png
```

### 📊 Métricas do Projeto

- **Linhas de código C#**: ~211
- **Total de arquivos .cs**: 8
- **Controllers**: 2
- **Repositories**: 1 interface + 1 implementação
- **Models**: 2 (Pessoa, WeatherForecast)
- **Endpoints**: 2 (/api/pessoa, /weatherforecast)
- **Tamanho**: ~465 KB

---

## 🚀 Configuração e Execução

### 📋 Pré-requisitos

#### Obrigatórios
- ✅ **.NET Core SDK 3.1+**
  ```bash
  dotnet --version
  ```
- ✅ **MySQL Server 8.0+**
  ```bash
  mysql --version
  ```

#### Opcionais
- 🖥️ **Visual Studio Code** com extensões:
  - C# for Visual Studio Code
  - .NET Core Test Explorer
  - REST Client
- 🐬 **MySQL Workbench** ou **DBeaver** (GUI para MySQL)
- 📮 **Postman** ou **Insomnia** (testar API)

---

## 🔧 Instalação Passo a Passo

### 1️⃣ Configurar Banco de Dados MySQL

#### Criar Database e Tabela
```sql
-- Criar banco de dados
CREATE DATABASE myapi;

-- Usar o banco
USE myapi;

-- Criar tabela Pessoa
CREATE TABLE Pessoa (
    Codigo INT AUTO_INCREMENT PRIMARY KEY,
    Nome VARCHAR(100) NOT NULL,
    Endereco VARCHAR(200)
);

-- Inserir dados de exemplo
INSERT INTO Pessoa (Nome, Endereco) VALUES
('João Silva', 'Rua A, 123'),
('Maria Santos', 'Av. B, 456'),
('Pedro Oliveira', 'Rua C, 789');

-- Verificar dados
SELECT * FROM Pessoa ORDER BY Nome ASC;
```

**Saída esperada**:
```
+--------+-----------------+---------------+
| Codigo | Nome            | Endereco      |
+--------+-----------------+---------------+
|      1 | João Silva      | Rua A, 123    |
|      2 | Maria Santos    | Av. B, 456    |
|      3 | Pedro Oliveira  | Rua C, 789    |
+--------+-----------------+---------------+
```

---

### 2️⃣ Configurar Connection String

#### Editar appsettings.json
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "server=localhost;user id=root;password=SUA_SENHA;port=3306;database=myapi;"
  }
}
```

**Parâmetros**:
- `server`: Endereço do MySQL (localhost para local)
- `user id`: Usuário do MySQL (padrão: root)
- `password`: Senha do usuário
- `port`: Porta do MySQL (padrão: 3306)
- `database`: Nome do banco (myapi)

---

### 3️⃣ Restaurar Pacotes NuGet

```bash
cd web-api-mysql-master

# Restaurar dependências
dotnet restore
```

**Saída esperada**:
```
Restore succeeded.
```

---

### 4️⃣ Compilar o Projeto

```bash
# Build
dotnet build

# Ou build em modo Release
dotnet build -c Release
```

**Saída esperada**:
```
Build succeeded.
    0 Warning(s)
    0 Error(s)
```

---

### 5️⃣ Executar a Aplicação

```bash
# Executar
dotnet run

# Ou executar com watch (auto-reload)
dotnet watch run
```

**Saída esperada**:
```
info: Microsoft.Hosting.Lifetime[0]
      Now listening on: https://localhost:5001
info: Microsoft.Hosting.Lifetime[0]
      Now listening on: http://localhost:5000
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
```

---

### 6️⃣ Acessar a API

#### Swagger UI (Documentação Interativa)
```
http://localhost:5000/swagger
```

#### Endpoints Disponíveis

**1. Listar Pessoas**
```bash
curl http://localhost:5000/api/pessoa
```

**Response 200 OK**:
```json
[
  {
    "codigo": 1,
    "nome": "João Silva",
    "endereco": "Rua A, 123"
  },
  {
    "codigo": 2,
    "nome": "Maria Santos",
    "endereco": "Av. B, 456"
  },
  {
    "codigo": 3,
    "nome": "Pedro Oliveira",
    "endereco": "Rua C, 789"
  }
]
```

**Response 204 No Content**:
(Quando não há registros no banco)

---

**2. Weather Forecast (Exemplo)**
```bash
curl http://localhost:5000/weatherforecast
```

**Response 200 OK**:
```json
[
  {
    "date": "2024-04-02",
    "temperatureC": 15,
    "temperatureF": 58,
    "summary": "Cool"
  },
  ...
]
```

---

## 🔍 Análise Detalhada do Código

### 📦 Model - Pessoa.cs

```csharp
namespace ApiMySql.Model
{
    public class Pessoa
    {
        public int Codigo { get; set; }
        public string Nome { get; set; }
        public string Endereco { get; set; }
    }
}
```

**Características**:
- ✅ **POCO** (Plain Old CLR Object)
- ✅ **Propriedades automáticas** (auto-properties)
- ✅ **Mapeia tabela Pessoa** do MySQL
- ✅ **Usado por Dapper** para mapeamento objeto-relacional

---

### 🔌 Repository - IPessoaRepository.cs

```csharp
using System.Collections.Generic;
using ApiMySql.Model;

namespace ApiMySql.Repository
{
    public interface IPessoaRepository
    {
        IEnumerable<Pessoa> GetAll();
    }
}
```

**Características**:
- ✅ **Abstração** do acesso a dados
- ✅ **Contrato** para implementações
- ✅ **Dependency Inversion Principle** (SOLID)
- ✅ **Facilita testes** (mockable)

---

### 💾 Repository - PessoaRepository.cs

```csharp
using System.Collections.Generic;
using ApiMySql.Model;
using MySql.Data.MySqlClient;
using Dapper;

namespace ApiMySql.Repository
{
    public class PessoaRepository : IPessoaRepository
    {
        private readonly string _connectionString;
        
        public PessoaRepository(string connectionString)
        {
            _connectionString = connectionString;
        }
        
        public IEnumerable<Pessoa> GetAll()
        {
            using(MySqlConnection connection = new MySqlConnection(_connectionString))
            {
                return connection.Query<Pessoa>(
                    "SELECT Codigo, Nome, Endereco FROM Pessoa ORDER BY Nome ASC"
                );
            }
        }
    }
}
```

**Características**:
- ✅ **Constructor Injection**: Recebe connection string
- ✅ **Dapper Query<T>**: Mapeia SQL para objetos
- ✅ **using statement**: Garante dispose da conexão
- ✅ **MySqlConnection**: Provider do MySQL
- ✅ **IEnumerable<Pessoa>**: Retorno lazy (performance)

**Fluxo de Execução**:
1. Cria conexão MySQL
2. Executa query SQL
3. Dapper mapeia colunas para propriedades
4. Retorna IEnumerable<Pessoa>
5. Conexão é fechada automaticamente (using)

---

### 🎮 Controller - PessoaController.cs

```csharp
using ApiMySql.Model;
using ApiMySql.Repository;
using Microsoft.AspNetCore.Mvc;
using System.Linq;

namespace ApiMySql.Controller
{
    [ApiController]
    [Route("/api/[controller]")]
    public class PessoaController : ControllerBase
    {
        private readonly IPessoaRepository _pessoaRepository;
        
        public PessoaController(IPessoaRepository pessoaRepository)
        {
            _pessoaRepository = pessoaRepository;
        }
        
        [HttpGet]
        [Produces(typeof(Pessoa))]
        public IActionResult Get()
        {
            var pessoas = _pessoaRepository.GetAll();
            
            if (pessoas.Count() == 0)
                return NoContent();
                
            return Ok(pessoas);
        }
    }
}
```

**Atributos e Anotações**:
- `[ApiController]`: Habilita recursos de API (model validation, etc)
- `[Route("/api/[controller]")]`: Define rota /api/pessoa
- `[HttpGet]`: Endpoint responde a GET
- `[Produces(typeof(Pessoa))]`: Documenta tipo de retorno

**Lógica**:
1. Injeta `IPessoaRepository` via DI
2. Chama `GetAll()` no repositório
3. Se vazio → retorna **204 No Content**
4. Se tem dados → retorna **200 OK** + JSON

---

### ⚙️ Startup.cs - Configuração

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddControllers();

    // Swagger
    services.AddSwaggerGen(c =>
    {
        c.SwaggerDoc("v1", new OpenApiInfo { 
            Title = "My API", 
            Version = "v1" 
        });
    });
}

public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseHsts();
    }

    // Swagger
    app.UseSwagger();
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1");
    });

    app.UseRouting();
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllers();
    });
}
```

**ConfigureServices**:
- Registra controllers
- Configura Swagger (geração de docs)

**Configure**:
- Pipeline de middleware
- Ativa Swagger UI
- Configura roteamento
- Mapeia controllers

---

### 🔗 Dependency Injection

**⚠️ Nota**: O projeto atual **não registra** o repositório no container DI.

**Implementação Necessária**:

```csharp
// Startup.cs - ConfigureServices
public void ConfigureServices(IServiceCollection services)
{
    services.AddControllers();
    
    // Registrar repositório
    string connectionString = Configuration.GetConnectionString("DefaultConnection");
    services.AddScoped<IPessoaRepository>(provider => 
        new PessoaRepository(connectionString)
    );
    
    // Swagger
    services.AddSwaggerGen(c =>
    {
        c.SwaggerDoc("v1", new OpenApiInfo { Title = "My API", Version = "v1" });
    });
}
```

**Ciclos de Vida**:
- `AddScoped`: Uma instância por requisição HTTP
- `AddTransient`: Nova instância sempre
- `AddSingleton`: Uma única instância (singleton)

---

## 📊 Swagger - Documentação Interativa

### 🎨 Interface Swagger UI

**URL**: `http://localhost:5000/swagger`

**Recursos**:
- ✅ **Lista de Endpoints**: Todos os endpoints da API
- ✅ **Try it out**: Testar endpoints diretamente
- ✅ **Schemas**: Definições de modelos
- ✅ **Response examples**: Exemplos de respostas
- ✅ **Download OpenAPI Spec**: JSON/YAML

**Exemplo de Endpoint no Swagger**:
```
GET /api/pessoa
  Responses:
    200 - Success
      Content-Type: application/json
      Schema: Array of Pessoa
      
    204 - No Content
```

---

## 🐛 Troubleshooting

### ❌ Problema: Erro de conexão com MySQL

**Sintomas**:
```
MySql.Data.MySqlClient.MySqlException: Unable to connect to any of the specified MySQL hosts.
```

**Diagnóstico**:
```bash
# Verificar se MySQL está rodando
sudo systemctl status mysql  # Linux
# ou
net start MySQL  # Windows

# Testar conexão
mysql -u root -p -h localhost
```

**Solução**:
```json
// Verificar appsettings.json
{
  "ConnectionStrings": {
    "DefaultConnection": "server=localhost;user id=root;password=SUA_SENHA_CORRETA;port=3306;database=myapi;"
  }
}
```

---

### ❌ Problema: Tabela 'Pessoa' não existe

**Sintomas**:
```
MySql.Data.MySqlClient.MySqlException: Table 'myapi.Pessoa' doesn't exist
```

**Solução**:
```sql
-- Verificar se database existe
SHOW DATABASES;

-- Criar database se não existir
CREATE DATABASE myapi;

-- Usar database
USE myapi;

-- Criar tabela
CREATE TABLE Pessoa (
    Codigo INT AUTO_INCREMENT PRIMARY KEY,
    Nome VARCHAR(100) NOT NULL,
    Endereco VARCHAR(200)
);
```

---

### ❌ Problema: Swagger não aparece

**Sintomas**:
404 Not Found ao acessar /swagger

**Solução**:
```csharp
// Verificar Startup.cs - Configure
app.UseSwagger();
app.UseSwaggerUI(c =>
{
    c.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1");
    c.RoutePrefix = string.Empty;  // Swagger na raiz (/)
});
```

---

### ❌ Problema: Dependência não injetada

**Sintomas**:
```
System.InvalidOperationException: Unable to resolve service for type 'ApiMySql.Repository.IPessoaRepository'
```

**Solução**:
```csharp
// Adicionar em Startup.cs - ConfigureServices
services.AddScoped<IPessoaRepository>(provider => 
    new PessoaRepository(
        Configuration.GetConnectionString("DefaultConnection")
    )
);
```

---

## 🎓 Conceitos .NET Core Abordados

### ✅ 1. ASP.NET Core Web API

**Definição**: Framework para criar APIs HTTP RESTful.

**Características**:
- 🔸 Cross-platform (Windows, Linux, macOS)
- 🔸 Alto desempenho
- 🔸 Middleware pipeline
- 🔸 Dependency Injection nativa
- 🔸 Model binding e validation
- 🔸 Content negotiation (JSON, XML)

---

### ✅ 2. Dapper (Micro ORM)

**Definição**: ORM leve e de alta performance.

**Vantagens**:
- ✅ **Performance**: ~2x mais rápido que Entity Framework
- ✅ **Simplicidade**: Escreve SQL puro
- ✅ **Leve**: Apenas mapeamento objeto-relacional
- ✅ **Controle**: SQL explícito (sem magic)

**Comparação com EF Core**:

| Feature | Dapper | Entity Framework Core |
|---------|--------|----------------------|
| **Performance** | Muito alto | Moderado |
| **Controle SQL** | Total | Abstrato (LINQ) |
| **Curva de aprendizado** | Baixa | Alta |
| **Migrations** | Manual | Automático |
| **Change Tracking** | Não | Sim |
| **Tamanho** | ~100 KB | ~10 MB |

---

### ✅ 3. Dependency Injection

**Definição**: Padrão de injeção de dependências.

**Container Nativo**:
```csharp
// Registro
services.AddScoped<IRepository, Repository>();

// Injeção via construtor
public class Controller
{
    private readonly IRepository _repo;
    
    public Controller(IRepository repo)
    {
        _repo = repo;
    }
}
```

**Benefícios**:
- 🔸 Desacoplamento
- 🔸 Testabilidade
- 🔸 Manutenibilidade
- 🔸 Inversão de controle

---

### ✅ 4. Repository Pattern

**Definição**: Abstração da camada de acesso a dados.

**Estrutura**:
```csharp
// Interface (Abstração)
public interface IRepository
{
    IEnumerable<Entity> GetAll();
    Entity GetById(int id);
    void Add(Entity entity);
    void Update(Entity entity);
    void Delete(int id);
}

// Implementação
public class Repository : IRepository
{
    // Implementação com Dapper
}
```

---

### ✅ 5. RESTful API

**Princípios**:
- **Stateless**: Sem estado no servidor
- **Resources**: URLs representam recursos
- **HTTP Verbs**: GET, POST, PUT, DELETE
- **JSON**: Formato padrão de dados

**Convenções**:
```
GET    /api/pessoa     → Lista todos
GET    /api/pessoa/1   → Busca por ID
POST   /api/pessoa     → Cria novo
PUT    /api/pessoa/1   → Atualiza
DELETE /api/pessoa/1   → Remove
```

---

### ✅ 6. Swagger/OpenAPI

**Definição**: Especificação para documentar APIs.

**Swashbuckle**: Implementação .NET do Swagger

**Recursos**:
- 📄 Geração automática de docs
- 🧪 Testes interativos (Try It Out)
- 📋 Schemas e exemplos
- 📥 Download da especificação OpenAPI

---

## 🗺️ Roadmap de Melhorias

### 🎯 Curto Prazo
- [x] GET /api/pessoa (listar)
- [ ] Registrar IPessoaRepository no DI container
- [ ] GET /api/pessoa/{id} (buscar por ID)
- [ ] POST /api/pessoa (criar)
- [ ] PUT /api/pessoa/{id} (atualizar)
- [ ] DELETE /api/pessoa/{id} (remover)

### 🎯 Médio Prazo
- [ ] Validação de modelos (FluentValidation)
- [ ] Tratamento global de erros
- [ ] Logging (Serilog)
- [ ] Paginação de resultados
- [ ] CORS configuration
- [ ] Authentication/Authorization (JWT)

### 🎯 Longo Prazo
- [ ] Migração para .NET 8
- [ ] Unit Tests (xUnit + Moq)
- [ ] Integration Tests
- [ ] Docker containerization
- [ ] CI/CD pipeline
- [ ] Health checks
- [ ] Rate limiting
- [ ] Caching (Redis)

---

## 📝 Notas Importantes

### ⚠️ Avisos
- 🔴 **.NET Core 3.1**: Versão com suporte até 2022 (migrar para .NET 8)
- 🟡 **DI não configurado**: Repositório precisa ser registrado
- 🟠 **Apenas GET**: Outros métodos HTTP não implementados
- 🔵 **Sem autenticação**: API aberta (não usar em produção)

### ✅ Pontos Fortes
- ✔️ Arquitetura limpa (Controllers, Models, Repositories)
- ✔️ Dapper para alta performance
- ✔️ Swagger para documentação
- ✔️ Separation of Concerns
- ✔️ Pronto para VS Code

### 📦 Informações Técnicas
- **.NET Core**: 3.1
- **C#**: 8.0
- **Target Framework**: netcoreapp3.1
- **Linhas de código**: ~211
- **Arquivos C#**: 8

---

## 🔐 Melhorias de Segurança para Produção

### 1. Connection String Segura

```csharp
// Usar User Secrets em desenvolvimento
dotnet user-secrets set "ConnectionStrings:DefaultConnection" "server=..."

// Usar variáveis de ambiente em produção
services.AddDbContext<AppDbContext>(options =>
    options.UseMySql(
        Environment.GetEnvironmentVariable("DB_CONNECTION_STRING")
    )
);
```

### 2. Validação de Entrada

```csharp
public class PessoaDto
{
    [Required(ErrorMessage = "Nome é obrigatório")]
    [StringLength(100, MinimumLength = 3)]
    public string Nome { get; set; }
    
    [StringLength(200)]
    public string Endereco { get; set; }
}
```

### 3. CORS Configurado

```csharp
services.AddCors(options =>
{
    options.AddPolicy("AllowSpecificOrigin",
        builder => builder
            .WithOrigins("https://meusite.com")
            .AllowAnyMethod()
            .AllowAnyHeader()
    );
});

app.UseCors("AllowSpecificOrigin");
```

### 4. HTTPS Obrigatório

```csharp
services.AddHttpsRedirection(options =>
{
    options.RedirectStatusCode = StatusCodes.Status307TemporaryRedirect;
    options.HttpsPort = 5001;
});

app.UseHttpsRedirection();
```

---

## 📚 Recursos de Aprendizado

### 📖 Documentação Oficial
- [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core)
- [Dapper Documentation](https://dapperlib.github.io/Dapper/)
- [MySQL Connector/NET](https://dev.mysql.com/doc/connector-net/en/)
- [Swagger/OpenAPI](https://swagger.io/docs/)

### 🎓 Tutoriais Recomendados
- **Microsoft Learn** - ASP.NET Core Web API
- **Pluralsight** - Building Web APIs with ASP.NET Core
- **YouTube** - Tutoriais em português sobre .NET Core

### 📺 Comunidade
- [Stack Overflow](https://stackoverflow.com/questions/tagged/asp.net-core) (tag: asp.net-core)
- [.NET Foundation](https://dotnetfoundation.org/)
- [Reddit r/dotnet](https://www.reddit.com/r/dotnet/)

---

## 🔄 Comandos .NET CLI Essenciais

### Projeto
```bash
# Criar novo projeto Web API
dotnet new webapi -n NomeDoProjeto

# Restaurar pacotes
dotnet restore

# Build
dotnet build

# Executar
dotnet run

# Watch (auto-reload)
dotnet watch run

# Publicar
dotnet publish -c Release
```

### Pacotes NuGet
```bash
# Adicionar pacote
dotnet add package Dapper
dotnet add package MySqlConnector
dotnet add package Swashbuckle.AspNetCore

# Listar pacotes
dotnet list package

# Remover pacote
dotnet remove package NomeDoPacote
```

### Entity Framework (Alternativa)
```bash
# Adicionar EF Core
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Pomelo.EntityFrameworkCore.MySql

# Criar migration
dotnet ef migrations add InitialCreate

# Aplicar migration
dotnet ef database update
```

---

## 📄 Licença

Projeto educacional para fins de aprendizado de ASP.NET Core Web API.

---

## 🤝 Suporte e Contato

Para dúvidas sobre .NET Core:
- 📧 [ASP.NET Core Docs](https://docs.microsoft.com/aspnet/core)
- 💬 Stack Overflow (tag: asp.net-core)
- 🎓 Cursos da Alura sobre .NET Core

---

**Desenvolvido com ASP.NET Core** 🚀 | **Web API + Dapper + MySQL + Swagger**  
**Stack**: .NET Core 3.1 + C# 8.0 + MySQL 8.0 + Dapper 2.0 + Swagger 5.0  
*Última atualização: Abril 2024*

---

## 🎯 Quick Start

```bash
# 1. Clonar/Baixar projeto
cd web-api-mysql-master

# 2. Criar banco MySQL
mysql -u root -p < script_database.sql

# 3. Configurar appsettings.json
# Editar ConnectionString com sua senha

# 4. Restaurar pacotes
dotnet restore

# 5. Executar
dotnet run

# 6. Acessar Swagger
# http://localhost:5000/swagger
```

**Pronto! API rodando com documentação interativa.** 🎉
