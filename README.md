# Marcello Veículos

Site da **Marcello Veículos**, concessionária na Av. Sapopemba, 14891, Vila Ester, São Paulo – SP.

- Telefone: (11) 2919-0855
- WhatsApp: (11) 96403-7834
- Horário: seg a sex, 9h às 17h30 · sáb, 9h às 12h

## Arquivos

| Arquivo | Função |
|---------|--------|
| `index.html` | O site que os clientes veem |
| `carros.json` | O estoque: dados e fotos dos veículos |
| `admin.html` | Painel para adicionar, editar e remover veículos |

Site estático, sem servidor. Todo o estoque vem do `carros.json`.

## Publicar (GitHub Pages)

1. Envie os 3 arquivos para a raiz do repositório.
2. **Settings → Pages → Deploy from a branch → `main` → `/ (root)`**.
3. Site: `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/`
4. Painel: o mesmo endereço terminando em `/admin.html`.

## Atualizar o estoque

1. Abra `/admin.html` (celular ou computador). Ele carrega o estoque atual sozinho.
2. Adicione, edite ou remova veículos. As fotos são reduzidas automaticamente.
   Toque numa foto para torná-la a capa.
3. Toque em **Baixar carros.json**.
4. No GitHub, abra o repositório, **Add file → Upload files**, envie o `carros.json`
   (substitui o antigo) e confirme o commit.
5. Em cerca de 1 minuto o site está atualizado.

O painel não publica nada sozinho: só quem tem acesso ao repositório altera o site.
Se o painel não achar o estoque, use **Abrir carros.json**.

## Formato do carros.json

Lista de veículos. Campos: `id`, `y` (ano), `ay` (ano fab/modelo, opcional), `n` (marca e modelo),
`v` (versão), `km`, `c` (cor), `g` (câmbio), `p` (preço, `null` = "Consulte o preço"),
`ipva` (1 = pago, opcional), `obs` (opcional) e `fotos` (lista de imagens; a primeira é a capa).

## Segurança

O `index.html` tem uma política de segurança (CSP) que autoriza apenas o seu próprio script
(por hash SHA-256 em `script-src`). Atualizar o estoque **não** exige mexer nisso.
Só se editar o `<script>` do `index.html` será preciso recalcular o hash; caso contrário,
o navegador bloqueia o script e a lista de carros some.

```python
import hashlib, base64
s = open("index.html", encoding="utf-8").read()
i = s.rindex("<script>") + 8; j = s.rindex("</script>")
print("sha256-" + base64.b64encode(hashlib.sha256(s[i:j].encode()).digest()).decode())
```

## Pendências

- Imagem de prévia para links no WhatsApp (`og:image`), que exige o endereço público do site.
- Fotos de mais veículos (via painel).
- Conferir o CEP exibido (03989-000) com o das fotos (08330-180).

## Aviso

Todos os veículos anunciados têm passagem por leilão, conforme informado pela loja.
Preços, quilometragem e disponibilidade podem mudar. Confirme com a loja antes de visitar.
