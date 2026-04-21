# EcoMonitor 🌱

Prova de conceito (PoC) de um painel de gamificação sustentável desenvolvido com **Blazor Interactive Server (.NET)**.  
Projeto da Lista 12 — Componentização e Estado com Blazor.

---

## Identificação

- **Nome:** Jonathan Eduardo Martins Julião
- **Curso:** Análise e Desenvolvimento de Sistemas — Centro Universitário UNA Contagem
- **Disciplina:** Interação Humano-Computador e UX
- **Professor:** Daniel Henrique Matos de Paiva

---

## Sobre o Projeto

O **EcoMonitor** é um sistema de gamificação para a ONG ReCiclo, onde o usuário registra ações sustentáveis e acompanha seu impacto em tempo real. A aplicação demonstra o uso de componentes reutilizáveis no Blazor por meio do componente `EcoStatus.razor`.

---

## Heurísticas de Nielsen Aplicadas

### 1. Visibilidade do Status do Sistema
O contador de pontos é atualizado imediatamente a cada clique, sem atraso ou necessidade de recarregar a página. O usuário sempre sabe exatamente quanto já acumulou, tornando o feedback instantâneo e claro.

### 2. Reconhecimento em vez de Memorização
Cada instância do componente exibe o nome da ação (ex: "Reciclagem de Plástico") e o peso associado diretamente na interface. O usuário não precisa lembrar o que cada botão faz — a informação está sempre visível.

---

## Funcionalidades

- Três instâncias do componente `EcoStatus` com pesos diferentes
- Contador individual por ação
- Estilização condicional: o texto muda de cor ao ultrapassar 50 pontos
- Barra de progresso visual que avança conforme o contador cresce *(desafio extra)*
- Mensagem de conquista ao atingir 100 pontos *(desafio extra)*

---

## Como Executar o Projeto

### Pré-requisitos

- [.NET 8 SDK](https://dotnet.microsoft.com/download) instalado
- Terminal (PowerShell, bash ou similar)

### Passos

```bash
# 1. Clone o repositório
git clone https://github.com/[seu-usuario]/una-blazor-lista12.git

# 2. Acesse a pasta do projeto
cd una-blazor-lista12/EcoMonitor

# 3. Execute com o perfil HTTPS
dotnet run --launch-profile https
```

Acesse no navegador: `https://localhost:5001`

> Se o navegador alertar sobre certificado, clique em "Avançado" e depois "Continuar".  
> Para confiar no certificado de desenvolvimento: `dotnet dev-certs https --trust`

---

## Explicação Técnica — Como o `[Parameter]` foi utilizado

O parâmetro é o que torna o componente **reutilizável**. Em vez de criar três componentes diferentes para cada ação, um único `EcoStatus.razor` aceita valores externos via `[Parameter]`:

```razor
@* EcoStatus.razor *@

@* Parâmetros que o componente recebe de quem o usa *@
[Parameter] public string NomeAcao { get; set; } = "Ação";
[Parameter] public int PesoAcao { get; set; } = 1;
[Parameter] public int Meta { get; set; } = 50;
```

Na `Home.razor`, o mesmo componente é chamado três vezes com valores diferentes:

```razor
<EcoStatus NomeAcao="Reciclagem de Plástico" PesoAcao="1" />
<EcoStatus NomeAcao="Plantio de Árvores"     PesoAcao="10" />
<EcoStatus NomeAcao="Descarte de Eletrônicos" PesoAcao="5" />
```

Cada instância mantém seu próprio **estado interno** (`total`), completamente independente das outras. Isso é o princípio de componentização: escreve-se uma vez, usa-se quantas vezes quiser com comportamentos diferentes.

---

## Estrutura do Projeto

```
EcoMonitor/
├── Components/
│   ├── Pages/
... (23 linhas)
