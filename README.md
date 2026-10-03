```text
                            _   
                _ __   ___ | |_ 
                 '_ \ / _ \| __|
                 | | |  __/| |_ 
             (_)_| |_|\___| \__|
  ==========================================
    Artigos, Diretrizes e Dicas sobre .NET
```

<a id="readme-top"></a>

<h1 align="center">Base de Conhecimento .NET</h1>

<p align="center">
  <img src="https://img.shields.io/badge/ecossistema-.NET-purple" alt="Ecossistema .NET" />
  <a href="LICENSE"><img src="https://img.shields.io/badge/licença-MIT-darkcyan" alt="Licença" /></a>
  <a href="https://github.com/vinicius-stutz" target="_blank"><img src="https://img.shields.io/github/followers/vinicius-stutz?label=follow&style=social" height="20" title="Siga-me!" alt="Siga-me!" /></a>
</p>


## Sobre o Projeto
Este repositório consiste em um acervo técnico de consulta, curadoria e compartilhamento de conhecimentos práticos sobre o ecossistema .NET e a linguagem C#. Diferente de uma aplicação de software compilável com regras de negócio e persistência em banco de dados, este projeto atua como uma base viva de documentação técnica, dicas, artigos especializados, diretrizes de arquitetura e notas de referência rápida.

### Propósito
O propósito central é fornecer aos desenvolvedores alguma ou outra referência técnica e dicas em português brasileiro (PT-BR), auxiliando na tomada de decisões arquiteturais, na escolha criteriosa de dependências e na manutenção de padrões rigorosos de qualidade de código.

### Contexto
O ecossistema .NET evolui continuamente com novos lançamentos de runtime, compiladores e pacotes da comunidade. Engenheiros de software enfrentam recorrentemente problemas como:
- Falta de padronização na nomenclatura de classes, métodos, campos e interfaces;
- Aplicação superficial ou inadequada dos princípios de engenharia orientada a objetos (SOLID);
- Dificuldade em identificar bibliotecas consolidadas e maduras no repositório NuGet para substituir abordagens manuais lentas ou propensas a falhas;
- Necessidade de comandos rápidos para administração do ambiente e troubleshooting de SDKs via terminal.

Este repositório visa auxiliar em parte dessas demandas com materiais objetivos, didáticos e embasados nas melhores práticas de engenharia de software.

### Termos que você pode encontrar aqui
- **SDK (Software Development Kit)**: Conjunto de ferramentas de compilação, bibliotecas e comandos CLI necessários para desenvolver aplicações .NET.
- **Runtime**: Ambiente de execução responsável pelo gerenciamento de memória (Garbage Collector), JIT (Just-In-Time compilation) e execução do código intermediário (IL).
- **NuGet**: Gerenciador oficial de pacotes para o ecossistema .NET.
- **PascalCase / camelCase**: Convenções de escrita tipográfica para nomenclatura de símbolos em linguagens estruturadas.
- **SOLID**: Acrônimo dos cinco princípios fundamentais de design orientado a objetos introduzidos por Robert C. Martin.
- **Minimal APIs**: Abordagem simplificada do ASP.NET Core para criação de endpoints HTTP com menor overhead de configuração.

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

## Organização do Conteúdo
Os materiais estão estruturados em diretórios temáticos para facilitar a consulta conforme o nível de detalhe desejado:

### 1. Artigos (`articles/`)
- [**Os 10 Melhores Pacotes NuGet para .NET**](articles/melhores-pacotes-nuget.md): Curadoria de bibliotecas recomendadas para APIs e microsserviços modernos, incluindo ferramentas como [FastEndpoints](https://github.com/dj-nitehawk/FastEndpoints), [Spectre.Console](https://github.com/spectreconsole/spectre.console), entre outras soluções para produtividade e robustez técnica.

### 2. Diretrizes Técnicas (`guidelines/`)
- [**Padrões de Nomenclatura em C#**](guidelines/naming-conventions.md): Guia de referência detalhado cobrindo convenções de nomenclatura para namespaces, classes, interfaces, métodos, campos privados, propriedades e parâmetros.
- [**Princípios SOLID**](guidelines/solid.md): Resumo conceitual dos 5 pilares do design orientado a objetos (Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion).

### 3. Dicas Rápidas (`tips/`)
- [**Principais Comandos .NET Core no Console**](tips/dotnet-commands.md): Lista de comandos fundamentais para verificação de versão, listagem de runtimes e SDKs instalados, além de restauração e compilação de aplicações via terminal.

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

## Como Utilizar

Por se tratar de um repositório documental, não há necessidade de compilação ou execução de tarefas de build globais. Os tópicos podem ser lidos diretamente na interface web do GitHub ou clonados para leitura em qualquer editor compatível com Markdown.

### Pré-requisitos para Testar Snippets

Caso deseje executar os códigos e comandos exemplificados nos artigos:
- [.NET SDK LTS](https://dotnet.microsoft.com/download) instalado;
- Editores de código recomendados (um entre os abaixo listados):
    - [Visual Studio Community Edition](https://visualstudio.microsoft.com/pt-br/vs/community/) 
    - [Visual Studio Code](https://code.visualstudio.com/)
    - [JetBrains Rider](https://www.jetbrains.com/rider/)
- Terminal compatível com Bash, PowerShell ou Zsh.

### Validação do Ambiente
Para confirmar que seu ambiente .NET está configurado corretamente para reproduzir os exemplos:

```bash
dotnet --version
dotnet --list-sdks
dotnet --list-runtimes
```

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

## Roadmap

A tabela a seguir apresenta a análise crítica dos materiais existentes e o planejamento de evolução técnica da base de conhecimento:
- [ ] Boas Práticas
- [ ] Programação Assíncrona
- [ ] SOLID
- [ ] Resiliência
- [ ] Observabilidade
- [ ] Testabilidade

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

## Contribuindo
Contribuições que ampliem a qualidade e a abrangência desta base de conhecimento são bem-vindas. Para instruções completas sobre abertura de issues, padronização e formatação dos textos, consulte o arquivo [CONTRIBUTING.md](CONTRIBUTING.md).

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

## Licença
Este projeto é distribuído sob os termos da licença MIT. Para mais detalhes sobre permissões e direitos de uso, consulte o arquivo [LICENSE](LICENSE).

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>

## Contato
- **Responsável**: Vinícius Stutz
- **GitHub**: [vinicius-stutz](https://github.com/vinicius-stutz)
- **Repositório**: [dotnet](https://github.com/vinicius-stutz/dotnet)
- **Gestão do Projeto**: [Issues](https://github.com/vinicius-stutz/dotnet/issues) e [Pull Requests](https://github.com/vinicius-stutz/dotnet/pulls)

<p align="right">(<a href="#readme-top">voltar ao topo</a>)</p>