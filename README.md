# Minha Loja - E-commerce SPA & PWA

Este é um projeto de frontend para um aplicativo de e-commerce básico. O aplicativo foi construído para funcionar em uma única página (SPA) e possui capacidades de Progressive Web App (PWA), permitindo sua instalação nos dispositivos dos usuários e funcionamento offline básico.

## 🚀 Tecnologias Utilizadas

* **HTML5, CSS3 e JavaScript (Vanilla)**: A base estrutural, visual e lógica da aplicação[cite: 1].
* **Bootstrap 5.3.3**: Framework CSS importado via CDN, utilizado para a criação de um layout responsivo, barra de navegação (navbar), sistema de grids e cards de produtos[cite: 1].
* **Axios**: Biblioteca JavaScript (importada via CDN) baseada em Promises, utilizada para realizar requisições HTTP[cite: 1].
* **Fake Store API**: Uma API REST pública e gratuita (`https://fakestoreapi.com`) usada para popular a loja com dados fictícios de produtos, categorias e avaliações[cite: 1].

## 🧠 Conceitos Envolvidos

### 1. Single Page Application (SPA)
A aplicação não recarrega a página ao navegar entre as seções. O documento `index.html` contém todas as "telas" da aplicação divididas em blocos `<div>` com as classes `.tela` e `.collapse`[cite: 1]. 
* O arquivo `script.js` gerencia a navegação através da função `navegar(destino)`, que remove a classe `.show` da tela atual e a adiciona na tela de destino, criando a ilusão de troca de páginas[cite: 1].
* Existe um histórico simples de navegação gerenciado pelas variáveis `telaAtual` e `telaAnterior`, permitindo o funcionamento do botão "Voltar"[cite: 1].

### 2. Progressive Web App (PWA)
A aplicação adota práticas de PWA para oferecer uma experiência semelhante a um aplicativo nativo:
* **Manifesto (`manifest.json`)**: Arquivo de configuração que define o nome do app ("Minha Loja PWA"), cores de tema, ícones (em tamanhos 192x192 e 512x512) e define o modo de exibição como `standalone` (sem a barra de endereços do navegador)[cite: 1].
* **Service Worker (`service-worker.js`)**: Um script executado em segundo plano que gerencia o cache da aplicação[cite: 1]. 
  * Durante a instalação (`install`), ele salva os arquivos estáticos essenciais (`./`, `index.html`, `script.js`) no cache do navegador[cite: 1].
  * Durante as requisições (`fetch`), ele intercepta chamadas de rede. Se o usuário estiver offline e o recurso estiver em cache, o Service Worker serve a versão armazenada localmente, garantindo que o app continue acessível[cite: 1].
* **Instalação**: O script intercepta o evento `beforeinstallprompt` do navegador e exibe um botão "Instalar APP" na interface para que o usuário adicione a loja à tela inicial do seu dispositivo[cite: 1].

### 3. Consumo de API Assíncrono
O carregamento dinâmico do catálogo é feito inteiramente por JavaScript:
* Funções assíncronas (`async/await`) disparam requisições via Axios para buscar a lista de produtos (por categoria ou geral) ou os detalhes de um produto específico usando seu `id`[cite: 1].
* Os dados em formato JSON retornados pela API são iterados e injetados dinamicamente no DOM através da manipulação de `innerHTML`[cite: 1].

## 📂 Estrutura de Arquivos

* `index.html`: Estrutura principal, carregamento de CDNs (Bootstrap e Axios) e contentor das telas da SPA[cite: 1].
* `script.js`: Lógica de roteamento da SPA, chamadas de API, renderização de produtos no DOM e registro do Service Worker[cite: 1].
* `service-worker.js`: Script responsável pelas estratégias de cache offline[cite: 1].
* `manifest.json`: Arquivo de metadados para a instalação do PWA[cite: 1].
* `/imagens`: Diretório contendo os ícones (`icone192.png` e `icone512.png`) referenciados pelo manifesto[cite: 1].

## 🛠️ Como Executar

Para que o Service Worker e as funcionalidades do PWA funcionem corretamente, os arquivos não devem ser abertos diretamente pelo sistema de arquivos (protocolo `file://`). É necessário rodar a aplicação através de um servidor local (como o *Live Server* do VS Code, Servidor HTTP do Python ou Node.js).