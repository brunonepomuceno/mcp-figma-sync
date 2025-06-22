# MCP Figma Sync

Este projeto é uma ponte bidirecional entre o Design System e o Figma, permitindo a sincronização automática de componentes entre o código e o design.

## Estrutura do Projeto

A estrutura principal do projeto foi organizada para separar as responsabilidades:

```
.
├── docs/                  # Documentação do projeto
├── figma-plugin/          # Código-fonte do Plugin do Figma
├── scripts/               # Scripts de automação e o servidor da API
└── src/                   # Código-fonte do Design System (React)
    └── design-system/
        └── components/
            ├── button/
            │   └── button.json  # Definição do componente
            └── search/
                └── search.json  # Definição do componente
```

## Pré-requisitos

- Node.js (versão 18 ou superior)
- npm
- Figma Desktop App

## Instalação

1.  Clone o repositório:
    ```bash
    git clone [URL_DO_REPOSITÓRIO]
    cd mcp-figma-sync
    ```
2.  Instale as dependências:
    ```bash
    npm install
    ```

## Configuração do Plugin no Figma

1.  Abra o Figma Desktop App.
2.  Vá em `Plugins > Development > Import plugin from manifest...`.
3.  Selecione o arquivo `figma-plugin/manifest.json` na raiz do projeto.
4.  O plugin, agora chamado "MCP Figma Sync", estará disponível em `Plugins > Development`.

## Ambiente de Desenvolvimento (Modo Simples)

Para uma experiência de desenvolvimento completa com sincronização bidirecional, rode o seguinte comando em seu terminal:

```bash
npm run dev:sync
```

Este único comando irá:

1.  **Iniciar o servidor da API** (porta 3002).
2.  **Observar as mudanças nos arquivos `.json`** (sincronização Código -> Figma).
3.  **Compilar o plugin do Figma** em tempo real.

Tudo acontecerá em um único terminal.

### Ambiente de Desenvolvimento (Modo Manual)

Se preferir rodar cada processo em um terminal separado (útil para depuração), siga os passos abaixo. Você precisará de **3 terminais**.

1.  **Terminal 1: Servidor da API**

    ```bash
    npm run start:server
    ```

2.  **Terminal 2: Observador de Código (Código -> Figma)**

    ```bash
    npm run watch:components
    ```

3.  **Terminal 3: Compilador do Plugin (TypeScript -> JavaScript)**
    ```bash
    npm run watch:plugin
    ```

## Uso

1.  **Criar Componentes (Código -> Figma):**

    - Com o ambiente de desenvolvimento rodando (`npm run dev:sync`), abra o plugin no Figma (`Plugins > Development > MCP Figma Sync`).
    - Use o menu dropdown para selecionar um componente (ex: `button`, `search`).
    - Clique em "Create Component". O plugin buscará o `.json` correspondente via API e renderizará o componente no canvas.

2.  **Sincronização (Figma -> Código):**

    - Modifique qualquer propriedade de um componente que foi criado pelo plugin (mude a cor, o texto, o padding, etc.).
    - Após um breve momento, o arquivo `.json` correspondente no seu editor de código será atualizado automaticamente para refletir a mudança.

3.  **Sincronização (Código -> Figma):**
    - Modifique qualquer propriedade em um arquivo `.json` (ex: altere o `backgroundColor` em `button.json`).
    - Salve o arquivo. Dentro de alguns segundos, o componente correspondente no canvas do Figma será atualizado automaticamente.

## Estrutura do `component.json`

Os componentes são definidos por arquivos `.json` que seguem uma estrutura hierárquica. Esta estrutura permite a descrição de componentes complexos com múltiplos nós aninhados.

Exemplo (`search.json`):

```json
{
  "name": "search",
  "node": {
    "type": "FRAME",
    "name": "search",
    "width": 239,
    "layoutMode": "HORIZONTAL",
    "primaryAxisSizingMode": "FIXED",
    "counterAxisSizingMode": "AUTO",
    "primaryAxisAlignItems": "SPACE_BETWEEN",
    "counterAxisAlignItems": "MIN",
    "children": [
      {
        "type": "TEXT",
        "name": "Placeholder",
        "characters": "Placeholder",
        "primaryAxisSizingMode": "AUTO"
      },
      {
        "type": "FRAME",
        "name": "IconContainer",
        "width": 16,
        "height": 16,
        "children": [
          {
            "type": "TEXT",
            "name": "Icon",
            "characters": "🔍"
          }
        ]
      }
    ]
  }
}
```

## Contribuição

1.  Faça um fork do projeto.
2.  Crie uma branch para sua feature (`git checkout -b feature/nova-feature`).
3.  Commit suas mudanças (`git commit -m 'Adiciona nova feature'`).
4.  Push para a branch (`git push origin feature/nova-feature`).
5.  Abra um Pull Request.

## Licença

Este projeto está sob a licença MIT.
