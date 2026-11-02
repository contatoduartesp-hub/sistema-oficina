# AutoGestão Oficina — GitHub Pages

Projeto React + Vite + Tailwind preparado a partir do arquivo TSX original.

## Como publicar

1. Crie um repositório no GitHub (por exemplo, `autogestao-oficina`).
2. Extraia este ZIP e envie **todos os arquivos e pastas**, inclusive `.github/workflows/deploy.yml`, à raiz do repositório na branch `main`.
3. Acesse **Settings > Pages > Build and deployment > Source > GitHub Actions**.
4. Abra **Actions** e acompanhe o workflow **Publicar no GitHub Pages**. Se necessário, execute por `Run workflow`.
5. Acesse o endereço informado após o deploy: `https://SEU-USUARIO.github.io/autogestao-oficina/` (altere usuário/repositório).

`base: './'` em `vite.config.js` permite publicar tanto em subdiretórios de repositório quanto em domínios personalizados.

## Desenvolvimento local

```bash
npm install
npm run dev
npm run build
```

É necessário Node.js 20+ (recomendado Node 22).

## Integração com Google Apps Script

A URL do Google Apps Script do arquivo original foi preservada em `src/App.tsx`. O Pages hospeda **somente o frontend**; a planilha e os processos de gravação continuam no Apps Script. Confira permissões de acesso, respostas a GET/POST e eventuais restrições de CORS. O navegador pode recusar a integração mesmo que a implantação no Pages funcione.

## AVISO CRÍTICO DE SEGURANÇA — não colocar dados reais em produção sem correções

Este pacote mantém o comportamento original, **não converte o sistema em uma aplicação segura**:

- O frontend contém uma senha administrativa inicial em texto puro. Código servido pelo Pages é público, inclusive em repositórios privados com Pages público.
- O login confere credenciais no navegador; não substitui autenticação e autorização **no servidor**.
- O frontend recebe/salva conjuntos de dados que podem incluir usuários/senhas e dados de clientes.
- O fluxo de criação do primeiro administrador, se não houver usuários, é inseguro para um endpoint público.
- O método `POST` envia o banco inteiro e a interface não verifica de forma robusta a resposta do servidor; cliques sucessivos podem gerar sobrescrita de dados.
- A URL do Apps Script publicada na aplicação não é um segredo e não serve como mecanismo de controle de acesso.

**Antes de publicar para terceiros**: implementar autenticação/autorização no backend (Google Apps Script ou outro backend), armazenar senhas como hash seguro ou usar um provedor de identidade, restringir acesso a dados e operações por usuário, validar requisições no servidor e rever o desenho de sincronização. Apenas alterar a senha padrão ou ocultar botões não resolve. Para um ERP com informações sensíveis, considere hospedagem que forneça uma camada backend de autenticação adequada.

## Observação sobre testes

O projeto foi estruturado para compilação via Vite e deploy via Actions, mas o deploy e a comunicação com o backend precisam ser testados em sua conta GitHub/Google. Não existe uma publicação já concluída.
