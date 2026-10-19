# Flux OS — Repositório de Aplicativos

Repositório oficial de aplicativos `.apx` do Flux OS.

## Como funciona

Os apps são hospedados aqui no GitHub e instalados via:
- **Terminal:** `flux-pkg install <app>`
- **Flux Store:** GUI gráfica para navegar e instalar

## Estrutura

```
/
├── apps/                    # Pacotes .apx
│   ├── flux-terminal/
│   │   └── flux-terminal-1.0.0.apx
│   ├── flux-notes/
│   │   └── flux-notes-1.0.0.apx
│   └── ...
├── index.json              # Índice de apps (metadata)
└── README.md
```

## index.json

Formato do índice de apps:

```json
{
  "version": "1.0",
  "updated": "2026-10-19",
  "apps": [
    {
      "id": "flux-terminal",
      "name": "Flux Terminal",
      "version": "1.0.0",
      "description": "Terminal moderno com abas e transparência",
      "author": "Flux OS",
      "license": "MIT",
      "category": "System",
      "icon": "https://raw.githubusercontent.com/USER/flux-apps/main/apps/flux-terminal/icon.png",
      "download": "https://github.com/USER/flux-apps/releases/download/v1.0.0/flux-terminal-1.0.0.apx",
      "size": 123456,
      "sha256": "abc123...",
      "dependencies": ["pyside6"],
      "screenshots": [],
      "tags": ["terminal", "shell", "console"]
    }
  ]
}
```

## Como publicar um app

1. Crie o app com `flux-apx-build`
2. Adicione o `.apx` na pasta `apps/<slug>/`
3. Atualize o `index.json` com os metadados
4. Crie uma release no GitHub com o `.apx`
5. Atualize o `download` no index.json para a URL da release

## Como instalar (via terminal)

```bash
# Instalar app específico
flux-pkg install flux-terminal

# Buscar apps
flux-pkg search terminal

# Listar apps disponíveis
flux-pkg list-remote

# Atualizar app
flux-pkg update flux-terminal
```

## Como instalar (via Flux Store)

1. Abra o Flux Store no menu
2. Navegue pelas categorias
3. Clique em "Instalar"
4. Pronto!

## Contribuindo

1. Fork este repositório
2. Crie seu app seguindo o guia em `docs/GUIA_APPS_NATIVOS.txt`
3. Adicione o `.apx` e atualize o `index.json`
4. Abra um Pull Request

## Licença

Todos os apps seguem suas próprias licenças. Veja o `manifest.toml` de cada app.
