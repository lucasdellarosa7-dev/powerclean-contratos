# Power Clean · Propostas e Contratos (site)

Sistema de propostas e contratos em **um único arquivo HTML**, sem servidor.
Funciona no computador e no celular, e pode ser publicado de graça no GitHub Pages.

---

## Como publicar no GitHub

1. Entre no repositório onde já está o gerador de propostas de limpeza.
2. Clique em **Add file → Upload files** e arraste o arquivo `index.html`
   (o que está nesta pasta). Se preferir manter os dois sistemas separados,
   renomeie para `contratos.html` antes de subir.
3. Em **Settings → Pages**, confirme que o Source está como **Deploy from a branch**,
   branch `main` e pasta `/ (root)`.
4. Em um ou dois minutos o site fica no ar em
   `https://SEU-USUARIO.github.io/SEU-REPOSITORIO/index.html`.
5. Mande o link para as outras duas pessoas — cada uma abre no navegador
   (dá para "Adicionar à tela de início" no celular e usar como aplicativo).

## Como atualizar depois

Suba o `index.html` novo por cima do antigo (Upload files → mesmo nome → Commit).
Quem já tiver o site aberto deve dar um **Ctrl+F5** para pegar a versão nova.

---

## Como usar

1. **Clientes** — cadastre uma vez; o CEP preenche o endereço sozinho e o CPF é conferido.
2. **Kits** — monte o catálogo (potência, geração, equipamentos e valores).
   Ao escolher um kit, o formulário inteiro é preenchido.
3. **Novo documento** — selecione cliente + kit, confira valores e gere.
   - A porcentagem calcula o valor da forma de pagamento automaticamente.
   - A soma das formas precisa fechar com o total, senão o contrato não é gerado.
4. **Histórico** — tudo que foi gerado fica salvo. Numa proposta aceita, clique em
   **"Fechou! Gerar contrato"** e os dados vão para o contrato prontos.
5. **PDF** — na visualização clique em **Imprimir / Salvar PDF**, escolha destino
   "Salvar como PDF", margens **Padrão** e desmarque **"Cabeçalhos e rodapés"**.

---

## Importante sobre os dados

Os cadastros ficam salvos **no navegador de cada pessoa** (localStorage) — nada é
enviado para a internet, o que protege os dados dos clientes. Como consequência:

- cada pessoa tem a sua própria base de clientes e kits;
- para passar os dados de um aparelho para outro, use **Backup → Baixar backup**
  e, no outro, **Importar e juntar**;
- limpar os dados de navegação do navegador apaga os cadastros — faça backup
  de vez em quando.

---

## Para desenvolvedores

O `index.html` é **gerado**, não editado à mão. As fontes ficam em `../site_src`:

| Arquivo | O que é |
|---|---|
| `index.html` | estrutura da página (com marcadores `__CSS__`, `__LOGO__`…) |
| `estilo.css` | interface + folhas A4 + regras de impressão |
| `dados.js` | armazenamento (localStorage), valor por extenso, CPF/CEP |
| `documentos.js` | montagem da proposta/contrato e paginação A4 |
| `app.js` | interface: abas, clientes, kits, histórico, cálculos |
| `dados_contrato.json` | cláusulas do contrato (exportadas de `gerador/clausulas.py`) |
| `logo_b64.txt` | logo embutida em base64 |

Para regerar o arquivo final:

```bash
python site_src/build.py
```

As cláusulas vêm de `gerador/clausulas.py` (mesma fonte do gerador local em Word).
Se o contrato mudar, edite lá, reexporte o JSON e rode o build de novo.
