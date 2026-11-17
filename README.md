# NexaTech — Projeto CI/CD

Aplicação web estática demonstrativa de uma empresa fictícia de tecnologia, criada para a atividade de CI/CD.

## Tecnologias
- HTML5
- CSS3
- JavaScript
- Git e GitHub
- GitHub Actions
- Cloudflare Pages

## Executar localmente
Abra o arquivo `index.html` no navegador. Para uma experiência mais próxima de hospedagem, use a extensão Live Server do VS Code.

## Pipeline CI
O workflow `.github/workflows/ci.yml` é acionado em `push` e `pull_request` para a branch `main`. Ele executa:
1. Setup: checkout e listagem dos arquivos.
2. Validação: verifica os arquivos obrigatórios e referências locais.
3. Build: prepara a pasta `dist` e armazena um artefato.
4. Deploy: informa que o deploy de produção é realizado pelo Cloudflare Pages conectado ao GitHub.

## Publicação no Cloudflare Pages
1. Envie este projeto para um repositório GitHub.
2. No Cloudflare, acesse **Workers & Pages → Create → Pages → Connect to Git**.
3. Autorize o GitHub e selecione o repositório.
4. Para este site estático, configure:
   - Framework preset: **None**
   - Build command: deixe vazio
   - Build output directory: ` / ` (raiz do projeto)
5. Clique em **Deploy**.

O Cloudflare Pages fará um deploy inicial e, depois, observará novos commits na branch conectada. Cada `git push` para `main` acionará uma nova publicação.

> Observação: a pipeline do GitHub Actions realiza Setup, Validação e Build. O deploy real é executado pela integração nativa GitHub ↔ Cloudflare Pages, conforme o roteiro do laboratório da disciplina. O job Deploy do workflow é informativo, não executa upload para a Cloudflare.

## Teste de alteração real para o vídeo
1. Altere um texto visível em `index.html`, por exemplo o título principal.
2. Execute:
   ```bash
   git add .
   git commit -m "Atualiza conteúdo da página inicial"
   git push
   ```
3. Mostre a execução em **GitHub → Actions**.
4. Aguarde o deploy no Cloudflare Pages.
5. Atualize a URL pública `.pages.dev` e mostre a alteração.

## Comandos para publicar no GitHub pela primeira vez
Crie um repositório vazio no GitHub e, na pasta do projeto, execute:

```bash
git init
git add .
git commit -m "Projeto inicial NexaTech"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git
git push -u origin main
```

Substitua a URL de exemplo pela URL real do seu repositório.
