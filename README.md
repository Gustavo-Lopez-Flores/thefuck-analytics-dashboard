# TheFuck Analytics Dashboard

Painel analítico desenvolvido com **Vue.js** para exibir dados sobre o crescimento de estrelas do repositório `nvbn/thefuck` no GitHub. A aplicação permite aos usuários visualizar a evolução do número de estrelas ao longo do tempo e explorar destaques dos usuários que interagiram com o projeto.

## Descrição dos Componentes

### 1. **StarChart**
   - **Função**: Exibe o gráfico de evolução do número de estrelas ao longo do tempo.
   - **Interfaces**:
     - **Dados Necessários**: JSON com registros contendo `starred_at` e `stars`.
     - **Opções de Filtro**:
       - **Período**: Últimos 30 dias, últimos 6 meses, último ano, e todo o período.
       - **Tipo de Visualização**: Absoluto (número de estrelas em cada data) ou Cumulativo (total acumulado ao longo do tempo).
   - **Serviços Oferecidos**:
     - Permite a visualização do gráfico com diferentes opções de filtro e agrupamento.

### 2. **UserHighlights**
   - **Função**: Lista usuários destacados com base na interação com o repositório.
   - **Interfaces**:
     - **Dados Necessários**: JSON com informações dos usuários (`starred_at`, `followers`, etc.).
     - **Filtros Internos**:
       - **Primeiros Usuários**: Lista dos primeiros usuários a darem estrelas no repositório.
       - **Usuários Recentes**: Lista dos usuários mais recentes a interagir.
       - **Usuários Populares**: Lista os usuários com mais seguidores.
   - **Serviços Oferecidos**:
     - Exibe listas de usuários destacados com base nos critérios acima.

## Estrutura do Projeto

- `src/components/StarChart.vue`: Componente Vue para exibir o gráfico de estrelas com filtros.
- `src/components/UserHighlights.vue`: Componente Vue para exibir destaques dos usuários.
- `src/data/thefuck-sample-100.json`: Dados JSON estáticos com o histórico de estrelas e informações de usuários.

## Instalação e Execução

### Pré-requisitos

- **Node.js** (versão recomendada: 14 ou superior)
- **Vue CLI** instalado globalmente

### Passo a Passo

1. **Clone o repositório**:
   ```bash
   git clone https://github.com/Gustavo-Lopez-Flores/thefuck-analytics-dashboard.git
   cd thefuck-analytics-dashboard
   ```

2. **Instale as dependências**:
   ```bash
   npm install
   ```

3. **Execute o servidor de desenvolvimento**:
   ```bash
   npm run serve
   ```
   Acesse a aplicação em `http://localhost:8080`.

4. **Build para Produção**:
   Para compilar a aplicação para produção:
   ```bash
   npm run build
   ```

5. **Linter**:
   Para verificar e corrigir erros de linting, execute:
   ```bash
   npm run lint
   ```

## Uso da Aplicação

- **Gráfico de Estrelas**: O gráfico de evolução de estrelas permite ao usuário ajustar o período e o tipo de visualização, de modo a compreender o crescimento do projeto.
- **Destaques de Usuários**: A seção de destaques exibe uma lista de usuários que interagiram com o projeto, dividida em categorias (primeiros, recentes e populares).