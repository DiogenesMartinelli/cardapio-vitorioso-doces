# Como publicar o cardápio (GitHub Pages + domínio da Hostinger)

## 1. Criar o repositório no GitHub (uma vez só)
1. Entre em https://github.com (crie a conta se ainda não tiver — use o e-mail diogenesm85@gmail.com).
2. Acesse https://github.com/new
3. Nome do repositório: `cardapio-vitorioso-doces`
4. Deixe como **Public** (o GitHub Pages gratuito exige repositório público).
5. NÃO marque "Add a README". Clique em **Create repository**.

## 2. Enviar os arquivos (uma vez só)
No computador, na pasta C:\CardapioVitoriosoDoces, rode (troque DiogenesMartinelli):

    git remote add origin https://github.com/DiogenesMartinelli/cardapio-vitorioso-doces.git
    git push -u origin main

Vai abrir uma janela do GitHub pedindo login — entre com sua conta e pronto.

## 3. Ativar o GitHub Pages
1. No repositório → **Settings** → **Pages**.
2. Em "Build and deployment" → Source: **Deploy from a branch**.
3. Branch: **main** / pasta **/ (root)** → **Save**.
4. Em ~2 minutos o site estará em `https://DiogenesMartinelli.github.io/cardapio-vitorioso-doces/`
   - Cardápio: essa URL
   - Painel: essa URL + `/admin.html`

## 4. Conectar o domínio da Hostinger
No GitHub: Settings → Pages → **Custom domain** → digite seu domínio (`vitoriosodoces.com.br`) → Save.
Depois marque **Enforce HTTPS** (aparece após o DNS propagar).

Na Hostinger (hPanel → Domínios → seu domínio → DNS / Zona DNS), crie estes registros:

| Tipo  | Nome | Valor                    |
|-------|------|--------------------------|
| A     | @    | 185.199.108.153          |
| A     | @    | 185.199.109.153          |
| A     | @    | 185.199.110.153          |
| A     | @    | 185.199.111.153          |
| CNAME | www  | DiogenesMartinelli.github.io    |

(Apague registros A e CNAME antigos de @ e www que apontem para a Hostinger.)
A propagação leva de alguns minutos a algumas horas. Depois disso:
- Cardápio: `https://vitoriosodoces.com.br`
- Painel: `https://vitoriosodoces.com.br/admin.html`

## 5. Como atualizar o cardápio no dia a dia
1. Abra o painel (`/admin.html`) e faça login com seu e-mail e senha.
2. Edite o que quiser (a prévia mostra na hora) e clique em **⬇ Baixar site atualizado**.
3. No GitHub, abra o repositório → clique no arquivo `index.html` → botão de lápis não é necessário:
   use **Add file → Upload files**, arraste o `index.html` baixado e clique em **Commit changes**.
4. Em ~1 minuto o site está atualizado.

## Segurança
- O painel pede e-mail e senha, e a senha não fica gravada em lugar nenhum (só uma impressão
  digital criptográfica). Mesmo assim, a proteção DE VERDADE é a sua conta do GitHub: só quem
  tem acesso a ela consegue alterar o site publicado. Ative a verificação em duas etapas em
  https://github.com/settings/security.
- Não reutilize a senha do painel em outros serviços.

