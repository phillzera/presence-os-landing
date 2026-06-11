# Presence OS — landing (lista de acesso ao beta)

Single page estática, sem build e sem dependências. Um produto **Soberanus**.
Pensada para subir como subdomínio (ex.: `presence.soberanus.com`).

## Subir

É só servir o `index.html`. Algumas opções:

- **Vercel / Netlify / Cloudflare Pages:** aponte o projeto para esta pasta (`landing/`).
  Sem comando de build; output dir = `.` (a própria pasta).
- **Qualquer host estático / S3 / nginx:** copie `index.html` para a raiz do site.
- **Teste local:** `cd landing && python3 -m http.server 8080` e abra `http://localhost:8080`.

Para o subdomínio, crie um registro DNS (CNAME) `presence` apontando para o host
e configure o domínio no painel do provedor.

## Formulário de lista de acesso

O `<form id="waitlist">` é **endpoint-agnóstico** (atributos no próprio form):

- `data-endpoint` **vazio (padrão):** ao enviar, abre um e-mail pré-preenchido
  (`mailto:` para `data-contact`). Funciona sem backend nenhum.
- `data-endpoint="https://..."`: faz `POST` JSON com
  `{ nome, email, linkedin, motivo, produto, origem }`. Compatível com:
  - **Formspree:** `data-endpoint="https://formspree.io/f/SEU_ID"`
  - **Tally / Getform / Basin:** use a URL de endpoint do serviço.
  - **API própria:** qualquer rota que aceite `POST application/json` e responda `2xx`.

Ajuste também `data-contact` (e-mail de contato/fallback). Hoje: `beta@soberanus.com`.

Em caso de sucesso o form troca para o estado "Você está na lista."; em erro de rede,
mostra mensagem e mantém os dados para reenvio.
