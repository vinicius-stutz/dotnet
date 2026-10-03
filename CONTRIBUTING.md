# Guia de Contribuição
Este documento estabelece as diretrizes para inclusão e aprimoramento de artigos, boas práticas e dicas técnicas.

## Como Contribuir
1. Faça um fork do repositório.
2. Crie uma issue descrevendo a proposta de artigo, melhoria ou correção de conteúdo.
3. Crie uma branch para sua contribuição a partir da branch principal seguindo o padrão GitFlow:
   - Para novos artigos: `feature/novo-artigo-nome`
   - Para correções ou revisões: `fix/ajuste-artigo-nome`
   - Para novas dicas de terminal: `feature/dica-cli-nome`
4. Realize as alterações mantendo os padrões de documentação e formatação.
5. Valide que todos os snippets de código C# ou comandos de terminal são válidos e foram testados localmente.
6. Envie um Pull Request detalhando as alterações propostas e referenciando a issue relacionada.

## Padrões de Conteúdo e Formatação
Para manter a consistência e a qualidade da documentação:
- **Codificação**: Todos os arquivos devem estar codificados em **UTF-8**.
- **Idioma**: Todo o conteúdo deve ser redigido em português brasileiro (PT-BR), com tom técnico, objetivo e impessoal, mas os trechos de código devem estar preferencialmente em **inglês**.
- **Formatação de Código**: Utilize blocos de código com identificação correta de sintaxe (ex.: ````csharp```` para C#, ````bash```` para comandos de shell).
- **Estrutura de Pastas**:
  - `articles/`: Artigos analíticos, comparativos e aprofundados sobre tecnologias e bibliotecas do ecossistema .NET.
  - `guidelines/`: Diretrizes de desenvolvimento, convenções de código, princípios de arquitetura e design de software.
  - `tips/`: Dicas práticas, comandos de terminal e soluções pontuais de consulta rápida.

## Padrão de Commits
Adote a especificação Conventional Commits para mensagens de commit:
- `docs: inclusão do artigo sobre FastEndpoints`
- `fix: correção de exemplo de código em naming-conventions`
- `style: padronização de formatação em solid.md`
- `refactor: reestruturação do sumário do repositório`

## Processo de Revisão
- Todo Pull Request passará por revisão de conteúdo e formatação antes do merge.
- Feedbacks serão focados na precisão técnica dos exemplos e na clareza didática das explicações.
- Uma vez aprovado, o Pull Request será incorporado ao repositório.
