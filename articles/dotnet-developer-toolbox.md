# .NET Developer Toolbox: O Guia Definitivo da Stack Moderna

O ecossistema .NET passou por uma transformação estrutural profunda nos últimos dois anos. Mudanças de licenciamento em bibliotecas historicamente dominantes, a maturidade das ferramentas nativas da Microsoft (ciclo .NET 8, 9 e 10) e a consolidação da inteligência artificial no fluxo de desenvolvimento redefiniram o que é considerado "boa prática".

Para desenvolvedores seniores, arquitetos e Tech Leads, manter a caixa de ferramentas atualizada não é apenas uma questão de acompanhar tendências, mas de mitigar riscos de licenciamento, reduzir o *boilerplate* e otimizar a performance e a manutenção dos sistemas.

Abaixo está o panorama técnico das ferramentas, bibliotecas e padrões arquiteturais recomendados para projetos .NET em 2026/2027.

## 1. IDEs, Editores e Fluxo de Trabalho com IA

A codificação assistida por inteligência artificial deixou de ser um diferencial e tornou-se a linha de base de produtividade. O ferramental atual divide-se pela necessidade da tarefa:

* **VS Code (com C# Dev Kit + GitHub Copilot) / Cursor:** Tornaram-se as ferramentas padrão para o dia a dia. O amadurecimento do *C# Dev Kit* trouxe um Language Server rápido e confiável, permitindo um fluxo de trabalho leve e multiplataforma. O **Cursor** destacou-se em fluxos de trabalho *AI-first*, permitindo refatorações em múltiplos arquivos com contexto profundo do repositório.
* **JetBrains Rider:** Permanece insubstituível para refatorações arquiteturais pesadas, análise estática avançada, inspeção de memória e gerenciamento de soluções legadas massivas. A mudança para o modelo gratuito para uso não-comercial expandiu ainda mais sua base.
* **Visual Studio:** Exclusivo para ambientes Windows, ainda é forte em empresas tradicionais, mas perdeu a hegemonia.

## 2. Testes Automatizados

Esta foi a categoria que mais sofreu alterações devido à comercialização de pacotes open-source tradicionais (como o caso do *SponsorLink* no Moq e a mudança de licenciamento do FluentAssertions v8+).

* **Frameworks de Teste:** O **xUnit** continua sendo o padrão de mercado pela sua estabilidade. Entretanto, o **TUnit** surgiu como a principal alternativa moderna para .NET 8+, utilizando *Source Generators* para execução livre de reflexão (compatível com Native AOT) e paralelismo extremo por padrão.
* **Mocking:** O **NSubstitute** assumiu a liderança absoluta em novos projetos, oferecendo uma sintaxe mais limpa e sem as controvérsias de segurança e telemetria que afetaram o Moq.
* **Asserções:** O **Shouldly** consolidou-se como o substituto natural e gratuito para asserções fluentes e mensagens de erro legíveis, evitando os custos de licenciamento comercial exigidos pelo FluentAssertions.
* **Testes de Integração e E2E:** O uso de bancos de dados em memória (`EF Core InMemory`) está obsoleto. O padrão absoluto é o **Testcontainers**, que sobe instâncias reais do banco de dados, mensageria e cache em containers Docker descartáveis durante a execução da suíte de testes. Para testes ponta a ponta (E2E) na web, o **Playwright** superou o Selenium e o Cypress em velocidade e confiabilidade no ecossistema .NET.

## 3. Desenvolvimento de APIs

A evolução do ASP.NET Core focou na redução de cerimônia e no aumento de throughput.

* **Minimal APIs & FastEndpoints:** As *Minimal APIs* substituíram os tradicionais `Controllers` como padrão para novos serviços, entregando menor alocação de memória e inicialização mais rápida. Para evitar arquivos `Program.cs` desorganizados, bibliotecas como **FastEndpoints** (que aplica o padrão REPR - *Request-Endpoint-Response*) ou **Carter** são amplamente utilizadas para estruturar os endpoints de forma coesa.
* **Documentação OpenAPI (Scalar):** A partir do .NET 9, o pacote `Swashbuckle` (Swagger UI) deixou de vir nos templates padrão devido à falta de manutenção ativa, dando lugar à geração nativa via `Microsoft.AspNetCore.OpenApi`. Para a interface visual de testes e documentação, o **Scalar** substituiu o Swagger UI, oferecendo uma UI moderna, rápida e com geração de clientes para diversas linguagens.
* **Comunicação HTTP:** O **Refit** continua sendo a escolha ideal para transformar interfaces C# em clientes HTTP fortemente tipados, integrado diretamente ao `IHttpClientFactory` e às políticas de resiliência nativas (`Microsoft.Extensions.Http.Resilience`, baseado no Polly v8).

## 4. Persistência de Dados e Caching

* **Banco de Dados Relacional:** O **PostgreSQL** (via driver `Npgsql`) ultrapassou o SQL Server como a primeira escolha para novos projetos em .NET. A ausência de custos proibitivos de licenciamento, a excelente performance em containers Linux e o suporte nativo avançado a JSON (`jsonb`) impulsionaram essa virada. O SQL Server permanece forte onde há contratos corporativos pré-existentes.
* **ORMs:** O **Entity Framework Core** nas versões recentes reduziu drasticamente a distância de performance para micro-ORMs, especialmente com suporte a *Bulk Updates/Deletes* (`ExecuteUpdateAsync` / `ExecuteDeleteAsync`) e *Compiled Queries*. O **Dapper** segue relevante, mas seu uso hoje é cirúrgico: restrito a *hot paths* de leitura extrema ou queries analíticas complexas.
* **Caching (HybridCache):** A interação manual com `IDistributedCache` e `IMemoryCache` deu lugar ao **HybridCache** (nativo da Microsoft) e ao **FusionCache**. Essas ferramentas gerenciam automaticamente um cache de dois níveis (L1 em memória local + L2 distribuído no Redis), incluem serialização otimizada e protegem a aplicação nativamente contra o problema de *Cache Stampede* (quando múltiplas requisições simultâneas tentam reconstruir um cache expirado ao mesmo tempo).

## 5. Logging, Observabilidade e Orquestração Local

* **OpenTelemetry & Serilog:** O **Serilog** mantém seu posto para geração de logs estruturados em texto/JSON. Contudo, a coleta de métricas, logs e *distributed tracing* convergiu inteiramente para o padrão **OpenTelemetry (OTel)**, eliminando o acoplamento do código com agentes proprietários de APM (como SDKs específicos do Datadog, New Relic ou Application Insights).
* **.NET Aspire:** É uma das maiores adições ao ecossistema recente. O Aspire resolve a dor de configurar ambientes locais complexos. Através de um projeto C# (`AppHost`), ele orquestra microsserviços, bancos de dados, Redis e mensageria sem exigir arquivos `docker-compose.yml` gigantescos. Além disso, o **Aspire Dashboard** fornece uma interface local instantânea para visualizar logs, traces e métricas via OpenTelemetry em tempo real durante o desenvolvimento (podendo inclusive ser executado via Docker de forma independente em projetos que não usam o restante do Aspire).

## 6. Mensageria e Processamento Assíncrono

* **Brokers:** **RabbitMQ** para cenários independentes de nuvem ou *on-premises*, e **Azure Service Bus** (ou AWS SQS/SNS) para ambientes gerenciados.
* **Abstração e Command Bus (Wolverine vs. MassTransit + MediatR):** Embora a dupla **MassTransit** (para mensageria) e **MediatR** (para desacoplamento in-process) ainda tenha a maior base instalada no mercado, o **Wolverine** despontou como a ferramenta de maior crescimento. O Wolverine unifica um *Command Bus* local (substituindo o MediatR) e um framework de mensageria assíncrona com suporte nativo ao padrão *Transactional Outbox*. Ele utiliza geração de código em tempo de compilação em vez de reflexão pesada, resultando em menor consumo de memória e maior velocidade de execução.

## 7. Autenticação e Segurança

* **Keycloak & Entra ID:** Com a consolidação do modelo comercial pago do *Duende IdentityServer*, o mercado dividiu-se em duas frentes claras: **Microsoft Entra ID** (antigo Azure AD) para projetos fortemente acoplados à nuvem da Microsoft, e **Keycloak** (rodando em container) como a solução open-source definitiva para gerenciamento de identidade e acesso (IAM) auto-hospedado.
* **Protocolos:** Implementação estrita de **OAuth 2.0** e **OpenID Connect (OIDC)**, utilizando validação nativa de tokens **JWT Bearer** nas APIs.

## 8. Arquitetura de Software

A mudança mais madura do ecossistema nos últimos dois anos não foi uma ferramenta, mas uma correção de rota arquitetural.

* **Vertical Slice Architecture (VSA):** Houve um forte recuo contra a complexidade artificial da *Clean Architecture* / *Onion Architecture* tradicional em projetos de pequeno e médio porte (onde alterar um campo no banco exigia modificar 5 projetos e 8 arquivos diferentes). Na **Vertical Slice Architecture**, o código é organizado por funcionalidade de negócio (*Features*), mantendo o Endpoint, o Request, o Validador (FluentValidation) e o Handler de acesso a dados juntos. A coesão aumenta e o acoplamento entre funcionalidades distintas cai drasticamente.
* **Monolito Modular antes de Microsserviços:** A adoção prematura de microsserviços provou-se custosa para equipes enxutas. A recomendação padrão em 2026/2027 é iniciar com um **Monolito Modular** bem delimitado (usando *Vertical Slices* internamente e comunicação assíncrona entre módulos quando necessário) e extrair para microsserviços apenas os módulos que exigirem escala independente comprovada.

## Resumo da Stack Recomendada

| Categoria | Escolha Padrão (Default) | Alternativa Sólida / Caso Específico |
| :--- | :--- | :--- |
| **IDE / Editor** | VS Code + C# Dev Kit / Cursor | JetBrains Rider (Refatoração pesada) |
| **Testes (Unidade)** | xUnit + NSubstitute + Shouldly | TUnit (Foco em AOT e performance) |
| **Testes (Integração/E2E)** | Testcontainers + Playwright | - |
| **APIs** | Minimal APIs + Scalar (OpenAPI) | FastEndpoints / Carter |
| **Acesso a Dados** | EF Core + PostgreSQL | Dapper (Hot paths) + SQL Server (Enterprise) |
| **Cache** | HybridCache + Redis | FusionCache |
| **Observabilidade** | OpenTelemetry + Serilog + Aspire Dashboard | - |
| **Mensageria / Mediator** | Wolverine (Unificado) | MassTransit + MediatR |
| **Identidade (Auth)** | Keycloak (Self-hosted) | Microsoft Entra ID (Cloud) |
| **Orquestração Local** | .NET Aspire + Docker | Docker Compose tradicional |
| **CI/CD & IaC** | GitHub Actions + Bicep (Azure) | Azure DevOps + Terraform / OpenTofu |
| **Frontend** | React + TypeScript + Tailwind CSS | Blazor (Sistemas internos / Backoffice) |
| **Arquitetura** | Monolito Modular + Vertical Slices | Microsserviços + Event-Driven (Alta escala) |

## Fontes e Referências
O ponto de partida deste artigo foi o [Post de Julio Casal, no Linkedin](https://www.linkedin.com/posts/juliocasal_ive-been-building-with-net-for-over-20-share-7512857476397150208-s4EJ/).

### 1. IDEs, Editores e Fluxo de Trabalho com IA
* **Visual Studio Code:** https://code.visualstudio.com/
* **C# Dev Kit (VS Code Marketplace):** https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit
* **GitHub Copilot:** https://github.com/features/copilot
* **Cursor:** https://www.cursor.com/
* **JetBrains Rider:** https://www.jetbrains.com/rider/
* *Referência - Anúncio da gratuidade do Rider para uso não-comercial:* https://blog.jetbrains.com/blog/2024/10/24/webstorm-and-rider-are-now-free-for-non-commercial-use/

### 2. Testes Automatizados
* **xUnit.net:** https://xunit.net/
* **TUnit:** https://github.com/thomhurst/TUnit
* **NSubstitute:** https://nsubstitute.github.io/
* **Shouldly:** https://docs.shouldly.org/
* **Testcontainers for .NET:** https://dotnet.testcontainers.org/
* **Playwright for .NET:** https://playwright.dev/dotnet/
* *Referência - Incidente SponsorLink no Moq (GitHub Issue #1372):* https://github.com/devlooped/moq/issues/1372
* *Referência - Mudança de licenciamento do FluentAssertions v8 (Xceed):* https://fluentassertions.com/releases/

### 3. Desenvolvimento de APIs
* **ASP.NET Core Minimal APIs:** https://learn.microsoft.com/en-us/aspnet/core/fundamentals/minimal-apis/overview
* **FastEndpoints:** https://fast-endpoints.com/
* **Carter:** https://github.com/CarterCommunity/Carter
* **Scalar:** https://scalar.com/ (Repositório: https://github.com/scalar/scalar)
* **Refit:** https://github.com/reactiveui/refit
* **Resiliência HTTP Nativa (.NET Resilience / Polly v8):** https://learn.microsoft.com/en-us/dotnet/core/resilience/http-resilience
* *Referência - Remoção do Swashbuckle e suporte nativo a OpenAPI no .NET 9:* https://learn.microsoft.com/en-us/aspnet/core/fundamentals/openapi/overview

### 4. Persistência de Dados e Caching
* **Entity Framework Core:** https://learn.microsoft.com/en-us/ef/core/
* **Dapper:** https://github.com/DapperLib/Dapper
* **PostgreSQL:** https://www.postgresql.org/
* **Npgsql (Provedor .NET para PostgreSQL):** https://www.npgsql.org/
* **Redis:** https://redis.io/
* **HybridCache (Documentação Oficial Microsoft):** https://learn.microsoft.com/en-us/aspnet/core/performance/caching/hybrid
* **FusionCache:** https://github.com/ZiggyCreatures/FusionCache

### 5. Logging, Observabilidade e Orquestração Local
* **Serilog:** https://serilog.net/
* **OpenTelemetry .NET:** https://opentelemetry.io/docs/languages/net/
* **.NET Aspire (Documentação Oficial):** https://learn.microsoft.com/en-us/dotnet/aspire/
* **.NET Aspire Dashboard (Execução Standalone via Docker):** https://learn.microsoft.com/en-us/dotnet/aspire/fundamentals/dashboard/standalone

### 6. Mensageria e Processamento Assíncrono
* **Wolverine:** https://wolverinefx.net/
* **MassTransit:** https://masstransit.io/
* **MediatR:** https://github.com/jbogard/MediatR
* **RabbitMQ:** https://www.rabbitmq.com/
* **Azure Service Bus:** https://learn.microsoft.com/en-us/azure/service-bus-messaging/

### 7. Autenticação e Segurança
* **Keycloak:** https://www.keycloak.org/
* **Microsoft Entra ID (para Desenvolvedores):** https://learn.microsoft.com/en-us/entra/identity-platform/
* **Duende IdentityServer:** https://duendesoftware.com/products/identityserver

### 8. Containers, CI/CD e Cloud
* **Docker:** https://www.docker.com/
* **Kubernetes:** https://kubernetes.io/
* **GitHub Actions:** https://github.com/features/actions
* **Azure DevOps Pipelines:** https://azure.microsoft.com/en-us/products/devops/pipelines
* **Azure Bicep:** https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/
* **Terraform:** https://www.terraform.io/
* **OpenTofu (Fork Open-Source do Terraform):** https://opentofu.org/
* **Pulumi:** https://www.pulumi.com/

### 9. Frontend
* **Blazor:** https://dotnet.microsoft.com/en-us/apps/aspnet/web-apps/blazor
* **React:** https://react.dev/
* **TypeScript:** https://www.typescriptlang.org/
* **Tailwind CSS:** https://tailwindcss.com/

### 10. Arquitetura de Software (Artigos e Conceitos Fundamentais)
* **Vertical Slice Architecture (Artigo original por Jimmy Bogard):** https://www.jimmybogard.com/vertical-slice-architecture/
* **Monolith First (Artigo de referência por Martin Fowler):** https://martinfowler.com/bliki/MonolithFirst.html