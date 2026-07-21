# 📝 Como editar o meu portfólio

Este guia explica, passo a passo e em linguagem simples, como mudar **qualquer
informação** que aparece no card do seu perfil do GitHub (nome, função, skills,
contatos, cores etc.).

> **A regra de ouro:** você **nunca** edita os arquivos `dark.svg` e `light.svg`
> na mão. Eles são **gerados automaticamente** por um script Python. Você muda o
> texto em **um único arquivo** e depois roda o script — ele reescreve os dois SVGs.

---

## 🎯 Resumo em 3 passos

1. Abra o arquivo **`scripts/build_profile.py`**.
2. Edite o texto que você quer trocar (quase tudo fica no bloco `DATA`, bem no topo).
3. Rode o comando abaixo para gerar os SVGs de novo:

   ```powershell
   py scripts/build_profile.py
   ```

   > Rode sempre a partir da **pasta raiz do projeto** (`lucasrafaellima`).
   > Se `py` não funcionar, tente `python scripts/build_profile.py`.

4. Envie as mudanças para o GitHub (veja a seção [Publicar](#-publicar-no-github)).

Pronto. Se aparecer no terminal `wrote dark.svg` e `wrote light.svg`, deu certo. ✅

---

## ✏️ Mudar textos e informações (o mais comum)

Abra `scripts/build_profile.py` e procure, logo no começo, o bloco **`DATA`**.
Cada linha é um campo do card. É só trocar o texto **entre aspas** à direita:

```python
DATA = {
    "user":     "lucasrafaellima",              # seu @ do GitHub
    "Subject":  "Lucas Rafael",                 # seu nome
    "Role":     "Full Stack · Angular/Java",    # sua função/cargo
    "Origin":   "Arapiraca - AL, Brazil",       # sua cidade/país
    "Status":   "Building • Learning • Shipping",
    "Currently":"Flutter apps · Studying iOS/Kotlin",  # o que está fazendo agora
    "ToolChain":"VS Code, Git, Docker, Postman, Figma", # ferramentas
    "OpenTo":   "Freelance · Full-time · Collabs",      # aberto a...
    "Lang":     "Dart, Java, Python, C#, TypeScript",   # linguagens
    "Mobile":   "Flutter, Android, React Native",
    "Frontend": "React, TypeScript, Tailwind",
    "Backend":  "Node.js, SpringBoot",
    "Database": "PostgreSQL, MySQL, Oracle",
    "Mail":     "lucasrafaellima03@gmail.com",  # seu e-mail
    "Portfolio":"",                             # link do site (vazio = não aparece)
    "LinkedIn": "",                             # seu LinkedIn
    "Instagram":"@lucasrafaellimaaa",
    "WhatsApp": "",
    "Github":   "lucasrafaellima",
}
```

### Onde cada campo aparece no card

| Campo no `DATA` | Onde aparece no card |
|-----------------|----------------------|
| `user` / `Github` | Nome grande no topo e nos links |
| `Subject` | Linha **Subject** (seu nome) |
| `Role` | Linha **Role** (função) |
| `Origin` | Linha **Origin** (localização) |
| `Status`, `Currently`, `ToolChain` | Linhas de status |
| `Lang`, `Mobile`, `Frontend`, `Backend`, `Database` | Bloco **Core** (skills) |
| `OpenTo` | Linha **Open · To** |
| `Mail`, `Portfolio`, `LinkedIn`, `Instagram`, `WhatsApp`, `Github` | Bloco **Contact** |

### ⚠️ Cuidados ao editar

- Mexa **só no texto entre aspas**. Não apague as aspas `"`, nem a vírgula `,` do fim.
- **Deixe vazio** (`""`) qualquer campo que você não quer mostrar — ex.: `"WhatsApp": "",`.
- Use acentos e emojis à vontade — o arquivo é salvo em UTF-8.
- Não precisa se preocupar com o "alinhamento" das colunas: o script alinha sozinho.

---

## 📅 Mudar "há quantos dias você programa"

No topo do card aparece algo como `up 1980d`. Isso é calculado a partir da data
em que você começou a programar. Para ajustar, procure esta linha em
`scripts/build_profile.py`:

```python
CODING_SINCE = datetime.date(2021, 1, 1)   # ano, mês, dia
```

Troque para a sua data real (formato: `ano, mês, dia`) e rode o script de novo.

---

## 🖼️ Trocar a sua foto (retrato em ASCII)

O desenho do seu rosto no card é gerado a partir de uma foto:

1. Substitua o arquivo **`assets/portrait.jpg`** pela sua foto (mantenha o mesmo
   nome, `portrait.jpg`). Uma foto de rosto, com boa luz e fundo simples, funciona melhor.
2. Rode `py scripts/build_profile.py` de novo.

Se quiser ajustar o **enquadramento** ou o **tamanho/detalhe** do desenho, mexa nestes
valores no topo do script (só depois de trocar a foto):

```python
COLS = 108                       # maior = mais detalhe/maior
CROP = (0.15, 0.12, 0.85, 0.67)  # recorte da foto (esquerda, topo, direita, base)
```

> `CROP` são frações de 0 a 1. Ex.: aumentar o último número mostra mais do queixo/peito.
> Ajuste aos poucos e vá rodando o script para ver o resultado.

---

## 🎨 Mudar as cores

As cores dos temas **claro** e **escuro** ficam no bloco `PALETTES`, dentro do
`scripts/build_profile.py` (procure por `PALETTES`). Cada cor é um código hex
(ex.: `#10B981`). Troque o valor e rode o script.

> Dica: se você não conhece códigos de cor, procure "color picker" no Google,
> escolha a cor e copie o código `#......`.

---

## 👀 Como ver o resultado antes de publicar

Os SVGs têm animação que **só toca no GitHub**. Se você abrir o `dark.svg` no
navegador local, pode aparecer **em branco** (é normal — a animação começa "apagada").

A forma mais confiável de conferir é publicar (próxima seção) e olhar seu perfil
em `https://github.com/lucasrafaellima`.

---

## 🚀 Publicar no GitHub

Depois de editar e rodar o script, mande as mudanças para o GitHub:

```powershell
git add .
git commit -m "Atualiza informacoes do perfil"
git push
```

Em alguns segundos, seu perfil em `github.com/lucasrafaellima` mostra o card novo.
(Pode ser preciso atualizar a página com **Ctrl+F5** para limpar o cache da imagem.)

> Existe também uma automação (GitHub Actions) que atualiza sozinha, todo dia,
> os números de estatísticas e a data. Você não precisa fazer nada para isso.

---

## ❓ Deu algum erro?

| Problema | Solução |
|----------|---------|
| `py` não é reconhecido | Use `python scripts/build_profile.py`. Se ainda falhar, instale o Python. |
| `ModuleNotFoundError: No module named 'PIL'` | Rode `py -m pip install pillow` e tente de novo. |
| Rodou mas o card não mudou no GitHub | Faça `git push` e atualize a página com **Ctrl+F5**. |
| Card apareceu em branco no navegador | Normal no preview local — veja direto no seu perfil do GitHub. |
| Quebrou o `DATA` (erro de sintaxe) | Confira se cada linha termina com `,` e se as aspas `"` estão fechadas. |

---

## 📌 Lembretes rápidos

- Edite **só** `scripts/build_profile.py` (e a foto). **Nunca** os `.svg` na mão.
- Sempre rode `py scripts/build_profile.py` **depois** de editar.
- Campo vazio (`""`) = não aparece no card.
- Detalhes técnicos mais profundos estão no arquivo `CLAUDE.md` na raiz do projeto.
