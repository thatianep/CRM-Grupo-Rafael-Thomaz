# Grupo Rafael Thomaz — CRM (pacote de implantação)

## Por que a página dava 404

O arquivo estava salvo como `index.html.html` (extensão duplicada). O GitHub
Pages (e a maioria dos serviços de hospedagem estática) só reconhece
automaticamente um arquivo chamado exatamente **`index.html`** como página
inicial. Com o nome errado, a URL raiz do site não encontra nada para
servir e devolve 404.

Este pacote já vem com o arquivo renomeado corretamente.

## O que tem aqui

```
deploy/
├── index.html                     ← página do sistema (nome corrigido)
└── google-apps-script/
    └── Code.gs                    ← script que recebe os dados na planilha
```

## 1. Publicar no GitHub Pages

1. Crie um repositório novo no GitHub (ou use um existente).
2. Envie o arquivo `index.html` para a raiz do repositório (junto, se
   quiser, do arquivo de logo `4.png`, que o sistema tenta carregar — se
   não existir, ele cai automaticamente num logo em SVG).
3. Vá em **Settings → Pages**.
4. Em "Branch", selecione a branch (`main`) e a pasta `/ (root)`. Salve.
5. Em alguns minutos o GitHub mostra a URL pública, algo como
   `https://<seu-usuario>.github.io/<repo>/`.
6. Abra essa URL — a tela de login deve aparecer normalmente (sem 404).

Login padrão do Administrador: usuário `GrupoRafaelThomaz`, senha
`GRT102030!`. Troque essa senha assim que possível pelo painel
"Gerenciar Equipe".

## 2. Planilha Google já conectada

Este pacote já vem com a sua URL do Apps Script pré-configurada no
`index.html` (o botão **"Google Planilhas"** no topo do sistema já mostra
"Conectado"). Ou seja, todo agendamento, formulário de Prestação de
Serviços e Diagnóstico Comercial salvo no sistema já é enviado
automaticamente para a sua planilha, em abas separadas (`Agendamentos`,
`Prestação de Serviços`, `Diagnósticos Comerciais`), criadas
automaticamente na primeira gravação.

Garanta que o script `google-apps-script/Code.gs` esteja implantado
nessa planilha (Extensões → Apps Script → cole o conteúdo do arquivo →
Implantar → Nova implantação → tipo "App da Web", executar como "Eu",
acesso "Qualquer pessoa").

**Importante:** sempre que você editar `Code.gs` depois de já ter
implantado, é preciso ir em **Implantar → Gerenciar implantações → editar
(ícone de lápis) → Versão: Nova versão → Implantar**, para que a URL já
usada pelo sistema passe a rodar o código atualizado.

Se um dia precisar trocar de planilha, basta clicar em **"Google
Planilhas"** no sistema e colar a nova URL — isso substitui, só no
navegador de quem clicar, a URL padrão embutida no arquivo.

## Observação de segurança

Como a URL da sua planilha agora está embutida no `index.html`, ela fica
visível a qualquer pessoa que abrir o site ou o código-fonte da página.
Quem tiver essa URL consegue enviar dados para a sua planilha (não
consegue lê-la, só adicionar linhas). Se o repositório for público, tenha
isso em mente; se preferir manter a URL fora do código, é possível
apagar esse valor padrão e colar a URL manualmente pelo botão "Google
Planilhas" em cada navegador que for usar o sistema.

## 3. Dados armazenados

O sistema é 100% client-side: todos os agendamentos, membros da equipe e
formulários ficam salvos no `localStorage` do navegador de quem está
usando. A integração com o Google Planilhas (passo 2) é o jeito de ter
uma cópia centralizada e persistente, acessível por toda a equipe.
