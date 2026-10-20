# Flux OS — Repositório de Aplicativos

Repositório oficial de aplicativos `.apx` do Flux OS.

- **Índice:** [index.json](./index.json)
- **Instalação via loja:** Flux Store (GUI)
- **Instalação via terminal:** `flux pkg install <app>`

---

## Estrutura do repositório

```
/
├── apps/                      # Ícones dos apps (PNG)
│   ├── flux-terminal/
│   │   └── icon.png
│   ├── flux-notes/
│   │   └── icon.png
│   └── ...
├── index.json                 # Índice de apps (metadata)
└── README.md                  # Este arquivo
```

Os pacotes `.apx` em si são publicados como **assets de releases** no GitHub
(na aba *Releases* deste repositório). O `index.json` aponta para a URL de download
de cada release.

---

## O que é um `.apx`?

Um pacote `.apx` é um arquivo **tar.gz** que contém um aplicativo auto-contido
do Flux OS. Ele é instalado para `/Programas/<slug>/` e registrado no menu
automaticamente.

### Estrutura interna de um `.apx`

```
meu-app.apx  (tar.gz)
├── manifest.toml      # Metadados (obrigatório)
├── app                # Binário/executável principal (nome livre, declarado no manifest)
├── icon.png           # Ícone (PNG quadrado, declare no manifest)
└── ...                # Qualquer outro arquivo do app (bibliotecas, assets, etc.)
```

---

## Como criar um `.apx`

### 1. Crie a estrutura

```bash
mkdir meu-app && cd meu-app
```

### 2. Escreva o `manifest.toml`

```toml
[app]
nome = "Meu App"                    # Nome exibido no menu/loja
slug = "meu-app"                    # Identificador (minúsculas, hífens, máx. 30)
versao = "1.0.0"                    # Versão semântica
exec = "app"                        # Caminho do executável (relativo ao pacote)
icon = "icon.png"                   # Caminho do ícone (relativo ao pacote)
descricao = "Descrição curta do app"
autor = "Seu Nome"
licenca = "MIT"
categorias = ["Utilities"]          # System, Office, Utilities, Multimedia, Development

# Dependências (opcionais, apenas informativas)
[deps]
python = ">=3.10"
```

### 3. Coloque o executável e o ícone

- O `exec` deve ser um arquivo **executável** (binário compilado ou script com shebang).
- O `icon` deve ser um PNG quadrado (recomendado 256×256 ou 512×512, fundo transparente).

Exemplo mínimo (script Python):

```bash
#!/usr/bin/env python3
print("Olá do Flux OS!")
```

```bash
chmod +x app
```

### 4. Empacote com `flux-apx-build`

```bash
# Empacota e gera meu-app.apx no diretório atual
flux-apx-build .

# Ou com caminho de saída específico
flux-apx-build --output meu-app-1.0.0.apx .

# Valida um .apx existente
flux-apx-build --validate meu-app-1.0.0.apx
```

### 5. Instale localmente para testar

```bash
flux pkg install meu-app-1.0.0.apx
```

O app aparece no menu em seguida.

---

## Como publicar no repositório

1. **Crie a release no GitHub** com o `.apx` como asset
   (ex.: tag `v1.0.0`, asset `meu-app-1.0.0.apx`).
2. **Adicione o ícone** em `apps/meu-app/icon.png` neste repositório.
3. **Atualize o `index.json`** — adicione uma entrada em `apps` com:

   ```json
   {
     "id": "meu-app",
     "name": "Meu App",
     "version": "1.0.0",
     "description": "Descrição curta",
     "author": "Seu Nome",
     "license": "MIT",
     "category": "Utilities",
     "icon": "https://raw.githubusercontent.com/samuuul12/flux-apps/main/apps/meu-app/icon.png",
     "download": "https://github.com/samuuul12/flux-apps/releases/download/v1.0.0/meu-app-1.0.0.apx",
     "size": 123456,
     "sha256": "",
     "tags": ["exemplo"]
   }
   ```

4. **Abra um Pull Request** com as alterações.

---

## Formato do `index.json`

```json
{
  "version": "1.0",
  "updated": "2026-10-19",
  "repo_name": "Flux OS Apps",
  "base_url": "https://github.com/samuuul12/flux-apps",
  "apps": [ ... ],
  "categories": [
    {"id": "all", "name": "Todos"},
    {"id": "system", "name": "Sistema"},
    {"id": "office", "name": "Escritório"},
    {"id": "utilities", "name": "Utilitários"},
    {"id": "development", "name": "Desenvolvimento"},
    {"id": "multimedia", "name": "Multimídia"}
  ]
}
```

| Campo | Descrição |
|---|---|
| `id` | Slug único do app (igual ao do manifest) |
| `name` | Nome exibido na loja |
| `version` | Versão publicada |
| `description` | Descrição curta |
| `icon` | URL bruta do PNG (`raw.githubusercontent.com/.../apps/<id>/icon.png`) |
| `download` | URL do `.apx` na release |
| `size` | Tamanho em bytes (0 se desconhecido) |
| `sha256` | Hash do arquivo (opcional) |
| `dependencies` | Lista de deps (informativa) |
| `featured` | `true` para destaque na loja |
| `system` | `true` para apps de sistema (não recomendado remover) |

---

## Comandos do `flux`

```bash
# Listar apps instalados
flux pkg list

# Buscar apps instalados
flux pkg search terminal

# Instalar (por slug ou por caminho .apx)
flux pkg install flux-terminal
flux pkg install ./meu-app.apx

# Info de um app instalado
flux pkg info flux-terminal

# Atualizar um app
flux pkg update flux-terminal

# Remover um app
flux pkg remove flux-terminal
```

> Veja todos os comandos com `flux help`.

---

## Contribuindo

1. Fork este repositório.
2. Crie seu app seguindo o guia acima.
3. Adicione o ícone em `apps/<slug>/icon.png` e atualize o `index.json`.
4. Publique a release com o `.apx`.
5. Abra um Pull Request.

## Licença

Todos os apps seguem suas próprias licenças. Veja o `manifest.toml` de cada app.
