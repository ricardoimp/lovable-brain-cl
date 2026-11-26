# Lovable Brain

Controle de créditos e gastos do workspace **Loggica Intermediações de Negócio** no Lovable.

O sistema roda como artifact no Claude ("Lovable · Minha economia adorável"): lê os prints do painel Usage details com IA, guarda o histórico de leituras, compara períodos, recomenda o melhor plano (manter, upgrade, downgrade, anual ou recarga avulsa) e traz um assistente de planejamento que gera prompts prontos para o Lovable.

## Estrutura

| Pasta | Conteúdo |
|---|---|
| `app/index.html` | Código do sistema, igual à versão publicada |
| `dados/snapshots/` | Cada leitura de consumo (período, Run, Build, projetos, itens de Run, insights) |
| `dados/config/planos.json` | Tabela de planos Pro, Business e recargas avulsas, plano atual e cotação |
| `dados/config/precos.json` | Preços por crédito em reais, teto de Build e corte de Run do planejamento |

## Conceitos

- **Build**: créditos gastos desenvolvendo com o agente do Lovable. Temporário.
- **Run**: créditos para manter os sistemas no ar (rede, banco, funções, storage, IA). Custo fixo.
- Leituras de períodos diferentes são comparadas por dia ou projetadas para 30 dias.

## Atualização

A cada mudança no sistema o código é publicado e versionado aqui. Os dados são exportados do banco do painel junto com cada commit. Os prints enviados ficam guardados só no painel e não entram no repositório.

## Publicação na Vercel

O repositório já tem `vercel.json` apontando para `app/` como site estático, sem build.

Fora do Claude (ex.: Vercel) o painel abre em **modo leitura**: carrega `app/dados.json`, gerado a partir de `dados/`, e mostra painel, planos, histórico e comparações. Atualizar com prints, assistente de IA e edições ficam escondidos, porque dependem do runtime do Claude. A versão comercial troca essas peças por Supabase (login, banco, storage) e rotas de API na Vercel.

Para atualizar os dados publicados: exporte o banco do painel para `dados/`, gere `app/dados.json` e faça commit. A Vercel republica sozinha.
