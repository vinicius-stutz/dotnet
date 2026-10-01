# Os 10 Melhores Pacotes NuGet para .NET
Lista dos pacotes NuGet essenciais e mais recomendados para projetos corporativos e APIs em .NET.

Proposta: **apresentar 10 pacotes NuGet que talvez você não conheça, mas deveria**. Não é só uma lista. É um convite pra turbinar seu repertório técnico com ferramentas maduras, poderosas e que podem transformar completamente sua forma de escrever software.

## FastEndpoints
- **GitHub**: [https://github.com/dj-nitehawk/FastEndpoints](https://github.com/dj-nitehawk/FastEndpoints)
### O problema
As Minimal APIs do ASP.NET são práticas, mas logo começam a crescer de forma desorganizada. Fica difícil aplicar validação, autenticação, versionamento e testabilidade sem fazer malabarismo com middleware, atributos e filtros.
### A solução
O FastEndpoints é uma alternativa moderna, enxuta e altamente estruturada às Minimal APIs. Ele oferece uma arquitetura baseada em "endpoints" isolados, fortemente tipados, com suporte nativo para validação, filtros, Swagger, versionamento, testes e injeção de dependência, tudo pronto para produção.

```csharp
public class HelloEndpoint : EndpointWithoutRequest<string>
{
    public override void Configure()
    {
        Get("/hello");
    }

    public override Task HandleAsync(CancellationToken ct)
    {
        return SendAsync("Hello, world!");
    }
}
```

**Quando usar**: Em APIs modernas REST/RESTful, especialmente quando você busca produtividade sem abrir mão de boas práticas e organização.

## Spectre.Console
- **GitHub**: [https://github.com/spectreconsole/spectre.console](https://github.com/spectreconsole/spectre.console)
### O problema
Criar aplicações de linha de comando geralmente resulta em interfaces pobres e pouco amigáveis. Um CLI moderno precisa mais do que `Console.WriteLine()` para brilhar.
### A solução
O Spectre.Console é o que todo terminal merece. Ele permite renderizar **tabelas, árvores, barras de progresso, prompts, textos coloridos**, com uma API fluente e intuitiva.

```csharp
AnsiConsole.Markup("[green]Deploy finalizado com sucesso![/]");
```

**Quando usar**: Em ferramentas internas, geradores de código, DevOps, scripts de build ou qualquer aplicação CLI que merece um toque profissional.

## FluentValidation
- **GitHub**: [https://github.com/FluentValidation/FluentValidation](https://github.com/FluentValidation/FluentValidation)
### O problema
Validar dados em controladores ou em entidades manualmente gera código poluído, difícil de testar e pouco reutilizável.
### A solução
Com FluentValidation, você encapsula regras de validação em classes específicas, de forma **declarativa, coesa e testável**.

```csharp
public class PessoaValidator : AbstractValidator<Pessoa>
{
    public PessoaValidator()
    {
        RuleFor(p => p.Nome).NotEmpty();
        RuleFor(p => p.Idade).InclusiveBetween(1, 120);
    }
}
```

**Quando usar**: Em qualquer aplicação que receba dados do usuário e precise validar com precisão dados de entrada ou entidades ricas sem poluir o código original.

## Polly
- **GitHub**: [https://github.com/App-vNext/Polly](https://github.com/App-vNext/Polly)
### O problema
Chamadas para serviços externos podem falhar. É inevitável. Mas fazer retry, fallback ou circuit breaker manualmente é complexo, propenso a bugs e difícil de manter.
### A solução
O Polly traz resiliência para sua aplicação de forma elegante. Ele fornece políticas reutilizáveis para **retry, timeout, bulkhead isolation, fallback e circuit breaker**.

```csharp
var policy = Policy.Handle<HttpRequestException>()
    .WaitAndRetry(3, retryAttempt => TimeSpan.FromSeconds(Math.Pow(2, retryAttempt)));

await policy.ExecuteAsync(() => httpClient.GetAsync("https://api.pagamento.com"));
```

**Quando usar**: Toda vez que sua aplicação depende de APIs externas, bancos de dados ou recursos instáveis.

## Scrutor
- **GitHub**: [https://github.com/khellang/Scrutor](https://github.com/khellang/Scrutor)
### O problema
Registrar serviços manualmente no DI é repetitivo, cansativo e gera acoplamento com a infraestrutura.
### A solução
Scrutor permite escanear assemblies e registrar dependências automaticamente com base em convenções. Reduz boilerplate e aumenta a escalabilidade do seu DI.

```csharp
services.Scan(scan => scan
    .FromAssemblyOf<IMeuServico>()
    .AddClasses()
    .AsImplementedInterfaces()
    .WithScopedLifetime());
```

**Quando usar**: Em aplicações com muitos serviços, CQRS, Handlers, Repositórios, etc. Ideal para manter a Program.cs limpa.

## Humanizer
- **GitHub**: [https://github.com/Humanizr/Humanizer](https://github.com/Humanizr/Humanizer)
### O problema
Transformar datas, números e enums em formatos legíveis por humanos costuma ser tedioso e cheio de if-else.
### A solução
Humanizer converte valores em formatos descritivos com uma API simples. Perfeito para UX.

```csharp
Console.WriteLine(DateTime.UtcNow.AddHours(-3).Humanize()); // "há 3 horas"
```

**Quando usar**: Sempre que for apresentar dados ao usuário. Melhora imensamente a experiência em dashboards, logs e relatórios.

## Refit
- **GitHub**: [https://github.com/reactiveui/refit](https://github.com/reactiveui/refit)
### O problema
Criar clientes HTTP exige muito código repetido: `HttpClient`, serialização, tratamento de erros, headers...
### A solução
Refit cria clientes REST a partir de interfaces. Você define a API e deixa que o pacote gere todo o código repetitivo.

```csharp
public interface IMyApi
{
    [Get("users/{id}")]
    Task<Usuario> GetUsuarioAsync(int id);

    [Post("users")]
    Task<Usuario> CriarUsuarioAsync([Body] Usuario novo);
}

// Registro com HttpClientFactory
services.AddRefitClient<IMyApi>()
        .ConfigureHttpClient(c => c.BaseAddress = new Uri("https://api.meusistema.com"));

// Uso no controller ou serviço
public class UsuarioService
{
    private readonly IMyApi _api;

    public UsuarioService(IMyApi api)
    {
        _api = api;
    }

    public async Task<Usuario> BuscarUsuario(int id)
    {
        return await _api.GetUsuarioAsync(id);
    }
}
```

**Quando usar**: Sempre que precisar integrar com APIs REST de forma tipada, testável e limpa.

## Mapster
- **GitHub**: [https://github.com/MapsterMapper/Mapster](https://github.com/MapsterMapper/Mapster)
### O problema
Fazer mapeamento entre DTOs e entidades pode gerar toneladas de código repetido. O AutoMapper resolve isso, mas se tornou pago e muitas vezes gera sobrecarga demais.
### A solução
Mapster é uma alternativa leve ao AutoMapper. Suporta mapeamento inline, projeta direto para DTOs e é rápido.

```csharp
UsuarioDTO dto = usuario.Adapt<UsuarioDTO>();
```

**Quando usar**: Sempre que precisar transformar objetos entre camadas, especialmente em APIs.

## DocumentFormat.OpenXml
- **GitHub**: [https://github.com/OfficeDev/Open-XML-SDK](https://github.com/OfficeDev/Open-XML-SDK)
### O problema
Gerar ou editar arquivos do Word/Excel programaticamente pode ser um pesadelo com COM+ ou automação do Office.
### A solução
Este SDK permite gerar documentos do Office manipulando diretamente a estrutura OpenXML. Sem necessidade de Office instalado.

```csharp
using (var document = WordprocessingDocument.Create("relatorio.docx", WordprocessingDocumentType.Document))
{
    var mainPart = document.AddMainDocumentPart();
    mainPart.Document = new Document(new Body(new Paragraph(new Run(new Text("Relatório Final")))));
}
```

**Quando usar**: Relatórios corporativos, integração com sistemas legados ou automação de documentos.

## QuestPDF
- **GitHub**: [https://github.com/QuestPDF/QuestPDF](https://github.com/QuestPDF/QuestPDF)
### O problema
Gerar PDFs com layout decente em .NET é historicamente difícil. Muitos pacotes são verbosos ou baseados em coordenadas absolutas.
### A solução
QuestPDF traz uma API fluente inspirada em layouts reativos. Criar um relatório visualmente bonito e responsivo se torna simples e natural.

```csharp
Document.Create(container =>
{
    container.Page(page =>
    {
        page.Content().Element(e => e.Text("Relatório de vendas").FontSize(20));
    });
})
.GeneratePdf("relatorio.pdf");
```

**Quando usar**: Geração de faturas, contratos, relatórios, recibos ou qualquer saída impressa.

## NetDevPack
Um ecossistema de Componentes Corporativos prontos para produção
- **GitHub**: [https://github.com/netdevpack](https://github.com/netdevpack)
### As soluções
Se você trabalha com DDD, arquitetura em camadas, validações ricas e um modelo de aplicação orientado a domínio, precisa conhecer o **NetDevPack**. Trata-se de uma coleção de pacotes voltados para acelerar o desenvolvimento de aplicações .NET corporativas, com foco em padrões e boas práticas.

**O NetDevPack é criado e mantido pela [desenvolvedo.io](https://desenvolvedo.io/)**
### O que o NetDevPack oferece
- `NetDevPack`: Implementações úteis para trabalhar com DDD, CQRS entre outros como por exemplo o uso do padrão Specification Pattern.
- `NetDevPack.Mediator`: Abstração baseada no MediatR, já preparada para uso com CommandHandlers, Events e Notifications. (E vai continuar free 🙂)
- `NetDevPack.Identity`: Integrações e extensões para ASP.NET Identity com foco em APIs.
- `NetDevPack.Brasil`: Validações de documentos e dados brasileiros como CPF, CNPJ, CEP, etc.
- `Security.Jwt`: Melhorias de segurança na autenticação com JWT, como JWT com chave rotativa, publico e privada e outras funcionalidades de segurança.
### Exemplo: Specification Pattern

```csharp
public class ClienteAtivoSpec : Specification<Cliente>
{
    public override Expression<Func<Cliente, bool>> ToExpression() =>
        cliente => cliente.Ativo;
}

var clientesAtivos = context.Clientes.Where(new ClienteAtivoSpec().ToExpression());
```

**Quando usar**: Projetos com arquitetura em DDD, separação entre Application/Domain, regras de negócio complexas ou necessidade de reaproveitamento de validações e filtros.

## Conclusão
Esses 10 pacotes NuGet não são apenas "atalhos", eles representam **anos de experiência condensados em código reutilizável**. Conhecê-los é um passo fundamental para quem quer ser mais produtivo, entregar software mais confiável e focar no que realmente importa: resolver problemas de negócio.

Então fica a pergunta: **quantas horas da sua semana são gastas escrevendo código que já está pronto, testado e mantido por uma comunidade?** Se a resposta for "muitas", talvez seja hora de abrir a toolbox do .NET e aproveitar o melhor que o ecossistema NuGet tem a oferecer.

## Referências
- Fonte: https://desenvolvedor.io/blog/10-pacotes-nuget-que-todo-desenvolvedor-dotnet-deveria-conhecer
- Autor: [Eduardo Pires](https://desenvolvedor.io/instrutor/eduardo-pires) *(com adaptações)*
