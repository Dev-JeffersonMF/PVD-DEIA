# Deia PDV — Releases Públicos

Repositório oficial de releases do **Deia PDV** (Ponto de Venda para Deia Presentes e Perfumaria).

> ⚠️ **Este repositório contém apenas binários de release, manifestos e documentação.**  
> O código-fonte completo permanece em repositório privado por segurança.

---

## 📦 Versão Atual: **1.0.3** (2026-07-27)

| Item | Detalhe |
|------|---------|
| **Instalador (nome fixo OTA)** | [`DeiaPDV_Setup.exe`](https://github.com/Dev-JeffersonMF/PVD-DEIA/releases/latest/download/DeiaPDV_Setup.exe) |
| **Instalador (versão fixa)** | [`DeiaPDV_Setup_v1.0.3.exe`](https://github.com/Dev-JeffersonMF/PVD-DEIA/releases/download/v1.0.3/DeiaPDV_Setup_v1.0.3.exe) |
| **Manifesto de versão** | [`version.json`](https://raw.githubusercontent.com/Dev-JeffersonMF/PVD-DEIA/main/version.json) |
| **Tamanho** | ~78 MB |
| **Compatibilidade** | Windows 10/11 x64 |
| **Obrigatória** | Não |

### 🆕 Novidades v1.0.2
- **Aba Caixa completa**: Botões "🟢 Abrir Caixa" / "🔴 Fechar Caixa" + diálogo "Sair" com confirmação
- **Relatório PDF profissional** (ReportLab) do fechamento de caixa com totais por forma de pagamento
- **Busca inteligente no PDV**: Pesquisa por **código OU nome** com pontuação (exato → começa com → contém)
- **Cofre de APIs criptografado** (AES-128 PBKDF2 200k iterações) — OpenRouter, NVIDIA NIM, DeepSeek, GitHub
- **Suporte a Notas Fiscais via IA**: Upload de imagem/PDF → OCR (Gemini Flash + Tesseract local) → parse automático
- **Animações fluidas 3D**: Sidebar slide, transições de páginas, hover 3D nos botões
- **Hardening**: `closeEvent` limpo (para timers, threads, Flask), rotação de `BACKUP_PENDENTE`, senha do certificado digital no cofre
- **Clientes/Crediário novos**: Máscara CPF/CNPJ progressiva, validação ao vivo, parcelas editáveis, WhatsApp automático

---

## 📥 Download Direto

### Para usuários (instalação manual)
| Arquivo | Link |
|---------|------|
| Instalador v1.0.3 (fixo) | [DeiaPDV_Setup.exe](https://github.com/Dev-JeffersonMF/PVD-DEIA/releases/latest/download/DeiaPDV_Setup.exe) |
| Instalador v1.0.3 (versão fixa) | [DeiaPDV_Setup_v1.0.3.exe](https://github.com/Dev-JeffersonMF/PVD-DEIA/releases/download/v1.0.2/DeiaPDV_Setup_v1.0.3.exe) |

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
  "versao": "1.0.3",
  "data_publicacao": "2026-07-27",
  "url_instalador": "https://github.com/Dev-JeffersonMF/PVD-DEIA/releases/latest/download/DeiaPDV_Setup.exe",
  "url_versao_fixa": "https://github.com/Dev-JeffersonMF/PVD-DEIA/releases/download/v1.0.3/DeiaPDV_Setup_v1.0.2.exe",
  "notas": "Aba Caixa completa (Abrir/Fechar Caixa + Relatorio PDF ReportLab). Buscar produtos por codigo OU nome. Cofre de APIs AES-128. Suporte a Notas Fiscais via IA (Gemini Flash + Tesseract). Animacoes fluidas 3D. Hardening (closeEvent limpo + rotacao backup). Clientes/Crediario novos.",
  "obrigatoria": false,
  "tamanho_estimado_mb": 78,
  "compatibilidade": "Windows 10/11 x64",
  "releases_historico": [
    {
      "versao": "1.0.3",
      "status": "atual",
      "url": "https://github.com/Dev-JeffersonMF/PVD-DEIA/releases/download/v1.0.2/DeiaPDV_Setup_v1.0.3.exe",
      "data": "2026-07-27",
      "notas": "Aba Caixa + Relatorio PDF + Cofre + IA NF + Animacoes 3D"
    }
  ]
}
```

---

## 📋 Como Atualizar (para o desenvolvedor)

> Este fluxo é **apenas para o admin/dev** — roda no seu PC de desenvolvimento.

```bash
# 1. Abra o painel de publicação (não incluído no instalador)
python painel_dev.py

# 2. Preencha:
#    - Nova versão: ex: 1.0.3
#    - Novidades: (markdown livre)
#    - ☐ Atualização obrigatória

# 3. Clique "COMPILAR E PUBLICAR UPDATE"
#    O painel faz tudo:
#    ✅ Atualiza VERSAO_LOCAL em updater.py
#    ✅ Atualiza AppVersion no DeiaPDV_installer.iss
#    ✅ Compila com PyInstaller (--clean --noconfirm)
#    ✅ Gera instalador com Inno Setup 6
#    ✅ Renomeia para DeiaPDV_Setup.exe (nome fixo OTA)
#    ✅ Atualiza version.json (repos de código + releases)
#    ✅ Commit + push no repo privado
#    ✅ Cria Release no repo público (deia-pdv-releases) com o .exe
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
