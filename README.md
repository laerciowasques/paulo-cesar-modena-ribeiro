# Currículo executivo — Paulo Cesar Modena Ribeiro

Currículo em HTML para leitura por headhunters e para colagem em plataformas de recrutamento. Os textos saem de um único arquivo de dados. Nada além do currículo de origem (`Paulo_Cesar_Modena_Ribeiro.pdf`, 29/10/2026) foi transformado em fato.

A foto entra só na versão web (`paulo-modena.jpg`). As versões executiva e ATS seguem sem foto. O PDF original não é alterado.

## Arquivos

| Arquivo | Função |
|---|---|
| `index.html` | Versão web: coluna única, foto no topo, números reais e resultados antes da carreira |
| `paulo-modena.jpg` | Retrato usado só na versão web |
| `executive_resume.html` | Versão executiva, para apresentação direta |
| `executive_resume_ats.html` | Versão linear, fundo branco, sem colunas nem ícones |
| `resume_data.json` | Fonte dos textos. É este arquivo que se edita |
| `resume_data.js` | Cópia usada quando a página é aberta com duplo clique |

As duas páginas têm PT-BR e EN-US. A versão executiva coloca as realizações antes da cronologia, para a primeira leitura. A versão ATS coloca a experiência antes, na ordem que os sistemas de recrutamento esperam.

## Abrir

Para a página pública, dê duplo clique em `index.html`. A versão para headhunters continua em `executive_resume.html`. Nos dois casos, `resume_data.js` precisa estar na mesma pasta.

Para a página ler o JSON direto, sem regenerar o espelho:

```powershell
python -m http.server 8765
```

Abra `http://localhost:8765/executive_resume.html`.

## Idioma, versão e impressão

No topo: **PT-BR**, **EN-US**, **Versão web**, **Versão executiva**, **Versão ATS** e **Imprimir**. O idioma escolhido fica gravado no navegador.

**Imprimir** abre o diálogo do navegador. Este botão não gera PDF sozinho. No destino, escolha **Salvar como PDF** ou **Microsoft Print to PDF**. Papel A4. Se o texto sair pequeno ou com margem dobrada, no diálogo use margem **Nenhuma** ou **Mínima** — o arquivo já define a margem da página.

A caixa de pendências, o item Apex e o aviso sobre o nível de português não saem na impressão.

Para plataformas de recrutamento, envie o **PDF** da versão ATS. Não envie o HTML: o que está oculto na tela ainda existe no código da página.

## Atualizar os dados

1. Edite `resume_data.json`. Cada texto visível tem `pt` e `en`.
2. Na pasta do projeto, regenere o espelho:

```powershell
python -c "import json, pathlib; p = pathlib.Path('resume_data.json'); data = json.loads(p.read_text(encoding='utf-8')); pathlib.Path('resume_data.js').write_text('/* Espelho de resume_data.json. Edite o JSON e rode o comando do README. */\nwindow.RESUME_DATA = ' + json.dumps(data, ensure_ascii=False, indent=2) + ';\n', encoding='utf-8')"
```

3. Recarregue a página com Ctrl+F5.

Se estiver usando `python -m http.server`, o passo 2 não é necessário: a página lê o JSON.

### Incluir uma experiência no Grupo Delga

Copie um objeto dentro de `experience[0].roles`:

```json
{
  "title": { "pt": "Cargo", "en": "Title" },
  "period": { "pt": "Mmm AAAA – Mmm AAAA", "en": "Mmm YYYY – Mmm YYYY" },
  "scope": { "pt": "Escopo em uma frase.", "en": "Scope in one sentence." },
  "bullets": [
    { "pt": "Ação, contexto e efeito.", "en": "Action, context, and effect." }
  ]
}
```

Experiência fora do grupo vai em `additionalExperience`.

### Incluir certificação, formação ou realização

- Formação: array `education`
- Certificação: array `certifications`. Use `"includeInPrint": false` enquanto o item não estiver claro
- Realização: array `achievements`. O desenho foi pensado para cinco itens
- Tecnologia: array `technology`, dentro da categoria certa, com `level` (`Uso profissional`, `Aplicação em projeto` ou o nível declarado)

### Publicar o portfólio

Preencha a URL. O link passa a aparecer na tela e na impressão.

```json
"portfolio": {
  "label": { "pt": "Portfólio", "en": "Portfolio" },
  "url": "https://...",
  "status": ""
}
```

## Pendências

Itens ausentes no PDF de origem. Não foram inventados.

- Portfólio: URL [PREENCHER]
- Cidade de cada empresa [VALIDAR]. A cidade do cabeçalho é a de residência, São Bernardo do Campo
- Anos de conclusão de FGV, Black Belt (EDTI) e Lean Manufacturing (EDTI) [VALIDAR]
- Item “Apex”, sem instituição, descrição ou data [VALIDAR]. Fica fora da impressão
- Número e seccional do CRC [PREENCHER], se forem publicados. O material só diz “CRC ativo”
- Período como avaliador do Prêmio ANEFAC [VALIDAR]
- Português como nativo [VALIDAR]. Não está declarado; foi registrado assim pela atuação integral no Brasil
- Inglês: intermediário, como no PDF. Não foi elevado
- E-mail disponível é o Gmail pessoal. Não havia e-mail corporativo
- Não há empregador depois de agosto de 2026. Nenhum cargo atual foi presumido. O mestrado segue até setembro de 2027

## O que ficou de fora

- Fotografia, idade, estado civil e documentos pessoais
- IFRS, CPC, fechamento contábil e consolidação societária — não aparecem no material
- Experiência internacional ou multinacional — não aparece no material
- MBA — o que consta é especialização em Controladoria, não MBA
- Quantidade de liderados em cada cargo. O “até 16 profissionais” está só no resumo da carreira
- Percentuais, valores e prazos que o PDF não informa. Onde o texto original é qualitativo, o currículo permanece qualitativo
- “Diretoria” foi tratada como alta gestão, não como conselho de administração

## Cronologia conferida

Não há sobreposição entre os cargos no Grupo Delga.

| Período | Cargo | Organização |
|---|---|---|
| Abr 2001 – Ago 2004 | Líder de Produção | Meta Usinagem |
| Set 2004 – Jul 2005 | Estagiário em Contabilidade | Grupo Delga |
| Ago 2005 – Mai 2010 | Analista de Tesouraria Pleno | Grupo Delga |
| Jun 2010 – Fev 2020 | Analista de Controladoria Sênior | Grupo Delga |
| Mar 2020 – Set 2022 | Supervisor de Planejamento Financeiro | Grupo Delga |
| Out 2022 – Jan 2024 | Gerente de Controles Internos | Grupo Delga |
| Fev 2024 – Ago 2026 | Gerente de Controladoria | Grupo Delga |
| Ago 2009 – Mai 2011 | Professor | SOS Educação Profissional |

A docência coincide com a tesouraria e o início da controladoria sênior. No PDF ela está em experiência adicional, e foi mantida assim.

Formação: bacharelado 2003–2006; especialização 2007–2009; extensão em didática em 2009; mestrado profissional out/2025–set/2027, em andamento.
