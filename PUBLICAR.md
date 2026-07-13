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
O painel de administração NÃO fica na internet — ele roda só no seu computador
(privacidade máxima: ninguém nem vê a tela de login).

1. Dê dois cliques em **Abrir-Painel.bat** (na pasta C:\CardapioVitoriosoDoces).
2. Faça login com seu e-mail e senha.
3. Edite o que quiser (a prévia mostra na hora) e clique em **⬇ Baixar site atualizado**.
4. Substitua o index.html da pasta C:\CardapioVitoriosoDoces pelo baixado e rode:

       git add index.html
       git commit -m "Atualiza cardapio"
       git push

   OU, se preferir sem comandos: no GitHub, abra o repositório →
   **Add file → Upload files** → arraste o `index.html` baixado → **Commit changes**.
5. Em ~1 minuto o site está atualizado.

## Segurança
- O painel roda apenas no seu computador — não é publicado no site. Ninguém na internet
  tem acesso a ele.
- Mesmo localmente ele pede e-mail e senha, e a senha não fica gravada em lugar nenhum
  (só uma impressão digital PBKDF2 com 310 mil iterações, inviável de quebrar).
- A proteção DE VERDADE do site publicado é a sua conta do GitHub: só quem tem acesso a
  ela consegue alterar o que está no ar. Ative a verificação em duas etapas em
  https://github.com/settings/security.
- Não reutilize a senha do painel em outros serviços.
- Os dados do cardápio (produtos, preços, telefone) são públicos por natureza — é um
  cardápio. Nenhum dado sensível fica no site.

