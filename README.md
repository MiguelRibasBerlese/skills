# NexMint Claude Skills

Skills customizadas da NexMint Labs para o Claude Code.  
Desenvolvidas e mantidas por Miguel Ribas Berlese & Enzo Shimada Daun.

---

## Skills disponíveis

| Skill | Arquivos | Linhas |
|-------|----------|--------|
| `biblioteca-fundamentos` | SKILL.md + 8 references | ~2.300 linhas |
| `ciberseguranca-pentest` | SKILL.md + 5 references | ~1.500 linhas |
| `engenharia-software-pro` | SKILL.md + 4 references | ~800 linhas |

---

## Instalação no Claude Code (Windows)

```powershell
# 1. Clonar o repositório
git clone https://github.com/MiguelRibasBerlese/skills.git "$env:TEMP\nexmint-skills"

# 2. Copiar cada skill para a pasta correta do Claude Code
$dest = "$env:USERPROFILE\.claude\skills"
Copy-Item "$env:TEMP\nexmint-skills\biblioteca-fundamentos" $dest -Recurse -Force
Copy-Item "$env:TEMP\nexmint-skills\ciberseguranca-pentest" $dest -Recurse -Force
Copy-Item "$env:TEMP\nexmint-skills\engenharia-software-pro" $dest -Recurse -Force

# 3. Confirmar instalação
Get-ChildItem $dest | Where-Object { $_.Name -in @("biblioteca-fundamentos","ciberseguranca-pentest","engenharia-software-pro") }
```

## Instalação no Claude Code (macOS/Linux)

```bash
# 1. Clonar o repositório
git clone https://github.com/MiguelRibasBerlese/skills.git /tmp/nexmint-skills

# 2. Copiar cada skill para a pasta correta do Claude Code
DEST="$HOME/.claude/skills"
cp -r /tmp/nexmint-skills/biblioteca-fundamentos $DEST/
cp -r /tmp/nexmint-skills/ciberseguranca-pentest $DEST/
cp -r /tmp/nexmint-skills/engenharia-software-pro $DEST/
```

## Atualizar skills (Windows)

```powershell
git clone https://github.com/MiguelRibasBerlese/skills.git "$env:TEMP\nexmint-skills"
$dest = "$env:USERPROFILE\.claude\skills"
Copy-Item "$env:TEMP\nexmint-skills\biblioteca-fundamentos" $dest -Recurse -Force
Copy-Item "$env:TEMP\nexmint-skills\ciberseguranca-pentest" $dest -Recurse -Force
Copy-Item "$env:TEMP\nexmint-skills\engenharia-software-pro" $dest -Recurse -Force
```

---

## Estrutura

```
skills/
├── biblioteca-fundamentos/
│   ├── SKILL.md
│   └── references/
│       ├── 01-lideranca-e-proposito.md
│       ├── 02-produto-e-execucao.md
│       ├── 03-vendas-e-persuasao.md
│       ├── 04-marketing-e-posicionamento.md
│       ├── 05-financas-e-riqueza.md
│       ├── 06-produtividade-e-performance.md
│       ├── 07-psicologia-e-influencia.md
│       └── 08-mentalidade-e-desenvolvimento.md
├── ciberseguranca-pentest/
│   ├── SKILL.md
│   └── references/
│       ├── 01-fundamentos.md
│       ├── 02-metodologia-pentest.md
│       ├── 03-ferramentas-e-defesas.md
│       ├── 04-threat-intelligence.md
│       └── 05-infra-critica.md
└── engenharia-software-pro/
    ├── SKILL.md
    └── references/
        ├── 01-fundamentos-e-craft.md
        ├── 02-arquitetura-e-sistemas.md
        ├── 03-stack-web.md
        └── 04-desenvolvimento-com-ia.md
```

---

**NexMint Labs** · nexmint.com.br
