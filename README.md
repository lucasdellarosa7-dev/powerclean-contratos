# Power Clean · Propostas e Contratos (site)

Sistema de propostas e contratos em **um único arquivo HTML**, sem servidor.
Funciona no computador e no celular, e pode ser publicado de graça no GitHub Pages.

---

## Onde está publicado

Site no ar em **https://lucasdellarosa7-dev.github.io/powerclean-contratos/**
(repositório `powerclean-contratos`, separado do gerador de limpeza).

Para atualizar: suba o `index.html` novo por cima do antigo no repositório
(Add file -> Upload files -> mesmo nome -> Commit). Quem já tiver o site aberto
deve dar **Ctrl+F5** para pegar a versão nova.

## Sincronizar entre a equipe (Firebase)

Hoje cada pessoa guarda os dados no próprio aparelho. Para compartilhar clientes,
kits e histórico entre as 3 pessoas, siga o `FIREBASE-PASSO-A-PASSO.txt`:
é um projeto Firebase **exclusivo deste sistema**, sem nenhuma ligação com o
banco do gerador de limpeza.

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
