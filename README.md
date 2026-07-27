# Deia PDV — Releases Públicos

Repositório oficial de releases do **Deia PDV** (Ponto de Venda para Deia Presentes e Perfumaria).

> ⚠️ **Este repositório contém apenas binários de release, manifestos e documentação.**  
> O código-fonte completo permanece em repositório privado por segurança.

---

## 📦 Versão Atual: **1.0.4** (2026-07-27)

| Item | Detalhe |
|------|---------|
| **Instalador (nome fixo OTA)** | [`DeiaPDV_Setup.exe`](https://github.com/Dev-JeffersonMF/PVD-DEIA/releases/latest/download/DeiaPDV_Setup.exe) |
| **Instalador (versão fixa)** | [`DeiaPDV_Setup_v1.0.4.exe`](https://github.com/Dev-JeffersonMF/PVD-DEIA/releases/download/v1.0.4/DeiaPDV_Setup_v1.0.4.exe) |
| **Manifesto de versão** | [`version.json`](https://raw.githubusercontent.com/Dev-JeffersonMF/PVD-DEIA/main/version.json) |
| **Tamanho** | ~82 MB |
| **Compatibilidade** | Windows 10/11 x64 |
| **Obrigatória** | Não |

### 🆕 Novidades v1.0.4
- **Sincronização completa com PDV-DEIA**: Layout dashboard compacto (2 fileiras de cards, sem sobreposição)
- **Correção UAC**: Se usuário cancelar permissão de admin, sistema continua funcionando sem privilégios
- **Correção FBWorker**: Sinal 'done' renomeado para 'resultado' — elimina warnings de desconexão
- **Autenticação anônima**: Login automático sem tela de login (Firebase anonymous auth)
- **Sistema de Caixa/Turno**: Abrir/fechar caixa, registro de vendas no turno, relatório PDF
- **Fallback local Firestore**: Banco local JSON quando Firebase está offline (403/401)
- **Aba Suporte**: WhatsApp direto e informações de contato
- **Plotly e Pandas**: Adicionados como dependências obrigatórias para gráficos do dashboard
- **Interface mais compacta**: Margens reduzidas, sidebar 180px, botões 26px

---

## 📥 Download Direto

### Para usuários (instalação manual)
| Arquivo | Link |
|---------|------|
| Instalador v1.0.4 (fixo) | [DeiaPDV_Setup.exe](https://github.com/Dev-JeffersonMF/PVD-DEIA/releases/latest/download/DeiaPDV_Setup.exe) |
| Instalador v1.0.4 (versão fixa) | [DeiaPDV_Setup_v1.0.4.exe](https://github.com/Dev-JeffersonMF/PVD-DEIA/releases/download/v1.0.4/DeiaPDV_Setup_v1.0.4.exe) |

### Para automação / OTA (atualização automática do app)
O próprio aplicativo consulta:
```
https://raw.githubusercontent.com/Dev-JeffersonMF/PVD-DEIA/main/version.json
```
Se houver versão mais nova, baixa `DeiaPDV_Setup.exe`, instala silenciosamente (`/VERYSILENT`) **preservando todos os dados** (`.env`, `banco_local.json`, `balanco.json`, `turno_historico.json`, `.env.vault`, `chave.json`, `deia_cert.pem`, `deia_key.pem`), e reinicia.

---

## 🔧 version.json (formato)

```json
{
  "versao": "1.0.4",
  "data_publicacao": "2026-07-27",
  "url_instalador": "https://github.com/Dev-JeffersonMF/PVD-DEIA/releases/latest/download/DeiaPDV_Setup.exe",
  "url_versao_fixa": "https://github.com/Dev-JeffersonMF/PVD-DEIA/releases/download/v1.0.4/DeiaPDV_Setup_v1.0.4.exe",
  "notas": "Sincronizadas melhorias do branch PDV-DEIA (layout dashboard compacto, correcao UAC, correcao FBWorker, autenticacao anonima, suporte a caixa/turno, fallback local Firestore). Adicionados plotly e pandas como dependencias obrigatorias. Nova aba Suporte.",
  "obrigatoria": false,
  "tamanho_estimado_mb": 82,
  "compatibilidade": "Windows 10/11 x64"
}
```

---

## 📋 Como Atualizar (para o desenvolvedor)

> Este fluxo é **apenas para o admin/dev** — roda no seu PC de desenvolvimento.

```bash
# 1. Abra o painel de publicação (não incluído no instalador)
python painel_dev.py

# 2. Preencha:
#    - Nova versão: ex: 1.0.5
#    - Novidades: (markdown livre)
#    - ☐ Atualização obrigatória

# 3. Clique "COMPILAR E PUBLICAR UPDATE"
#    O painel faz tudo:
#    ✅ Atualiza VERSAO_LOCAL em updater.py
#    ✅ Atualiza AppVersion no DeiaPDV_installer.iss
#    ✅ Compila com PyInstaller (--clean --noconfirm)
#    ✅ Gera instalador com Inno Setup 6
#    ✅ Renomeia para DeiaPDV_Setup.exe (nome fixo OTA)
#    ✅ Atualiza version.json
#    ✅ Commit + push no repo privado
#    ✅ Cria Release no repo público (PVD-DEIA) com o .exe
#    ✅ Push do version.json no repo público
```

### Pré-requisitos no PC de build
| Ferramenta | Versão mínima | Como instalar |
|------------|---------------|---------------|
| Python | 3.11+ | python.org |
| PyInstaller | 6.21+ | `pip install pyinstaller` |
| Inno Setup | 6.7+ | jrsoftware.org/isdl.php |
| GitHub CLI (`gh`) | 2.40+ | winget install GitHub.cli |
| Git | 2.40+ | git-scm.com |

---

## 🛡️ Segurança

- **Nenhuma chave/credencial** vai para este repositório público.
- O `version.json` contém **apenas metadados de release** (versão, URL, notas).
- O instalador **não inclui** `chave.json` (Admin SDK Firebase) — deve ser copiado manualmente em cada loja.
- Dados sensíveis do usuário (API keys, senha certificado) ficam **criptografados localmente** em `.env.vault` (AES-128).

---

## 📄 Licença

Uso interno — Deia Presentes e Perfumaria.  
Não redistribua sem autorização.

---

## 📞 Suporte

- **E-mail**: jefferson.macedo.fernandes@gmail.com
- **Sistema**: Deia PDV — Matozinhos, MG
