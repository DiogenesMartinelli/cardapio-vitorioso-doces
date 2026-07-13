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
O painel fica em https://vitoriosodoces.com.br/admin.html — pode usar de qualquer
computador ou celular.

1. Abra o painel e entre com seu e-mail e senha.
2. Edite o que quiser (a prévia mostra na hora).
3. Clique em **🚀 Publicar no site** → em ~1 minuto o site está atualizado. Pronto!

Na PRIMEIRA vez em cada navegador, o botão Publicar pede um token do GitHub
(instruções completas aparecem no grupo "🚀 Publicação direta" do próprio painel):
github.com/settings/personal-access-tokens/new → acesso somente ao repositório
cardapio-vitorioso-doces → permissão Contents: Read and write → gerar e colar no painel.

O botão **⬇ Baixar** continua existindo como alternativa manual (baixa o index.html
para você subir no GitHub em Add file → Upload files).

## Como o painel é protegido
- O arquivo admin.html publicado é 100% CRIPTOGRAFADO (AES-256-GCM). Quem abre sem a
  senha vê só a tela de login — o código e o conteúdo do painel são indecifráveis,
  mesmo baixando o arquivo. A chave é derivada da sua senha com PBKDF2 (310 mil
  iterações), inviável de quebrar por força bruta.
- O token do GitHub fica salvo criptografado SÓ no navegador em que você colou —
  nunca é enviado para o site nem para o repositório.
- A proteção final continua sendo a sua conta do GitHub: sem ela (ou sem um token
  criado por ela), ninguém altera o site publicado. Ative a verificação em duas
  etapas em https://github.com/settings/security.
- Se um dia quiser trocar a senha do painel: rode
  `node build-admin.js "email|nova-senha"` na pasta do projeto e suba o novo
  admin.html (o arquivo build-admin.js fica só no seu computador).
- Os dados do cardápio (produtos, preços, telefone) são públicos por natureza — é um
  cardápio. Nenhum dado sensível fica no site.

