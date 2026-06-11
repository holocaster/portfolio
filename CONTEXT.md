# Contexto

Glossario do projeto. Define a linguagem compartilhada. Sem detalhes de implementacao.

## Termos

- **Portfolio**: pagina unica (one-page) que apresenta a pessoa e reune seus
  projetos no ar, voltada a recrutadores. Idioma: portugues (pt-BR).

- **Projeto**: um trabalho concluido e publicado, acessivel por um link
  proprio. Aparece como um card na grade de projetos. Ex: Chopp Correto.

- **Curriculo**: a trajetoria profissional da pessoa (site mycv.prsites.com.br).
  Decisao: e tratado como duas coisas ao mesmo tempo - um link de topo
  ("Curriculo") por ser sobre a pessoa, e tambem um card de projeto por ser
  um trabalho web publicado.

- **Matriz de Riscos**: terceiro projeto. App de gestao de riscos operacionais
  (pessoas, processos, eventos de risco, planos de acao, matriz probabilidade x
  impacto). Fica atras de login, entao o card exibe credenciais de demo para o
  recrutador conseguir entrar (e uma POC).

## Decisoes de forma

- Direcao visual escolhida: minimalismo editorial (papel quente, tinta,
  um unico tom de destaque).
- Publicacao: arquivos estaticos servidos por nginx no VPS proprio. Sem
  framework e sem etapa de build, por simplicidade.
