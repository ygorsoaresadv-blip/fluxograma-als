# Publicações — manual e fluxo do escritório

Material interno de tratamento de publicações no Astrea, reunido em um único arquivo HTML,
sem dependências, sem instalação e sem servidor. Abre com duplo clique em qualquer navegador.

## O que tem dentro

- **Como tratar uma publicação.** As seis etapas do trabalho, da abertura no Astrea até a
  conclusão, na ordem em que acontecem.
- **22 cartões de teor**, um por tipo de publicação, agrupados nas três fases do processo
  (conhecimento, recursal e execução), com as agendas a criar, as datas e o responsável.
  Cada cartão traz um passo a passo marcável e o que ter em mãos antes de perguntar ao Ygor.
- **Calculadora de prazos**, com duas contas: do prazo fatal para o prazo interno, que
  devolve o título da agenda pronto para copiar, e da publicação para o prazo fatal.
  Conhece fins de semana, feriados nacionais, Carnaval, Sexta-feira Santa, Corpus Christi
  e o recesso de 20/12 a 20/01, e mostra quais dias pulou.
- **Manual completo**: as seis regras gerais, quem é quem e o glossário de siglas e termos.
- **Compêndio de jurisprudência**: 1.690 verbetes do TST e do STF em matéria trabalhista —
  544 súmulas, 709 orientações jurisprudenciais (SDI-1, SDI-2, SDC e Tribunal Pleno, incluindo
  as transitórias), 120 precedentes normativos e 317 temas de recursos repetitivos (IRR, IAC
  e IRDR) — com teor integral, status atual, temas e histórico de redações. A busca, em estilo Spotlight, entende a
  espécie pelo número (`331`, `OJ 191`, `SDI-2 54`, `PN 119`, `tema 128`, `SV 22`), aceita
  palavra-chave e frase entre aspas, e há atalhos de espécie, uma chave para ver só o que está em
  vigor e, em *Mais filtros*, tribunal, órgão, tema, status e ordem. Os resultados vêm em lista e
  cada verbete se abre no próprio lugar.
  Cada verbete tem botão para copiar o teor pronto para citação e para copiar o link direto.
- **Fluxo extraordinário da etiqueta roxa** (`C/ JULIANA TCHANI`), que se sobrepõe a todos os cartões.
  A Dra. Juliana Tchani recebe exclusivamente esses processos; o cível é do Dr. Mateus.
- **Tribunais e OAB**: código de segmento e sigla de TJ, TRF e TRT, e as inscrições do André.

## Como usar

| Ação | Como |
|---|---|
| Buscar um teor | Digite na busca da coluna esquerda, ou tecle `/` |
| Buscar pelas palavras do juiz | A busca aceita trechos da publicação, como `manifestem sobre os cálculos` |
| Filtrar por área | Trabalhista, cível ou previdenciário, nas pastilhas do topo do índice |
| Montar o título da agenda | **Calculadora**, aba *Do fatal para o prazo interno* |
| Acompanhar o tratamento | O passo a passo dentro de cada cartão, que zera ao fechar o arquivo |
| Consultar a jurisprudência | Botão **Compêndio** no topo, ou `Compêndio de jurisprudência` no índice |
| Achar o verbete pelo número | Na busca do compêndio: `331`, `OJ 191`, `SDI-2 54`, `PN 119`, `tema 128`, `SV 22` |
| Achar o verbete pelo teor | Palavras soltas, ou frase entre aspas, como `"empresa interposta"` |
| Ver só uma espécie | Atalhos logo abaixo da busca: Súmulas, OJs, Precedentes, Temas repetitivos |
| Ver só as OJs de uma seção | **Mais filtros** → Órgão: SDI-1, SDI-2, SDC ou Tribunal Pleno |
| Percorrer os resultados pelo teclado | Setas ↑ ↓ a partir da busca; Enter abre o verbete, Esc volta à busca |
| Ver se o termo buscado também é jurisprudência | A busca da coluna esquerda mostra quantos verbetes casam e leva até eles |
| Citar em peça | Botão **Copiar teor** no rodapé do cartão; sai com tribunal, número, teor e fonte |
| Link direto para um cartão | O endereço muda sozinho, por exemplo `#t/8.2`; o manual usa `#m/regras`, as outras telas usam `#passos`, `#calc` e `#tribunais`, e cada verbete tem o seu, como `#s/tst-331`, `#s/oj-sdi1-191`, `#s/pn-119` e `#s/irr-128` |

Funciona em celular e mantém sempre o tema claro, nas cores da identidade do escritório. A contagem de prazos é sempre em dias úteis.

## Sobre o compêndio de jurisprudência

É conferência rápida, não a fonte. O status e o teor mudam por resolução do tribunal. Antes de
citar em peça, confira na fonte oficial — o link está no rodapé de cada cartão.

| Espécie | Quantos | De onde veio | Conferido em |
|---|---|---|---|
| Súmulas do TST e do STF | 544 | Pesquisa de jurisprudência do TST e portal de súmulas do STF | 21/09/2026 |
| Orientações jurisprudenciais | 709 | Pesquisa de jurisprudência do TST | 22/09/2026 |
| Precedentes normativos | 120 | Pesquisa de jurisprudência do TST | 22/09/2026 |
| Temas de recursos repetitivos | 317 | Índice Temático de Precedentes Qualificados no TST | 22/09/2026 |

O que foi cancelado continua no acervo, com a tarja cinza, porque aparece em publicação antiga
e em acórdão; para esconder, use *Ver só o que está em vigor*. Os temas de recursos repetitivos
sem tese fixada ficam com a tarja azul e a etiqueta **Sem tese fixada**: o que vale ali é a
questão jurídica afetada, e vários deles têm determinação de suspensão de processos no TST,
avisada no próprio cartão.

**O tema de cada verbete é etiqueta de navegação, não classificação oficial.** As súmulas
trouxeram o tema já conferido; nas OJs, nos precedentes normativos e nos temas repetitivos ele
é atribuído aqui por vocabulário jurídico. A regra foi conferida contra as 544 súmulas já
classificadas e acerta ao menos um tema em 85% delas; 8% do acervo cai em *Outros*. O teor é
sempre o texto oficial, e é ele que se cita.

O acervo vive em um bloco `<script id="sumulasDados" type="application/json">` dentro do
próprio `index.html`, e só é interpretado quando faz falta, para não atrasar a abertura. Por
causa dele o arquivo passou de 128 KB para cerca de 1,5 MB, o que o GitHub Pages entrega
compactado e o navegador lê em fração de segundo — cerca de 170 ms para abrir e 50 ms para
interpretar o acervo, uma única vez.

## Sobre a calculadora

Ela é conferência rápida, não a contagem oficial. Pula sábados, domingos, os feriados
nacionais, o Carnaval, a Sexta-feira Santa, o Corpus Christi e o recesso forense, e diz
quais dias pulou. Não conhece feriados estaduais e municipais, pontos facultativos nem
suspensões determinadas pelo tribunal. A data que vale é a do Astrea; havendo divergência,
segue-se o Astrea e avisa-se o Ygor.

## Publicar como site

Em *Settings → Pages*, escolha a branch `main` e a pasta `/ (root)`.
O arquivo já se chama `index.html` e o `.nojekyll` evita que o GitHub tente processar o conteúdo.

> **Antes de publicar, verifique a visibilidade do repositório.** O material traz nomes,
> atribuições internas e regras de prazo do escritório. Em repositório público, o GitHub Pages
> deixa tudo acessível a qualquer pessoa com o endereço. Para uso interno, mantenha o repositório
> privado e distribua o arquivo pela rede do escritório ou pelo SharePoint.

## Manter atualizado

Ao mudar uma conduta, altere o cartão correspondente e registre o motivo na mensagem do commit.
Assim o histórico do repositório passa a ser o registro de por que o fluxo é como é.

Ao criar um cartão novo, lembre de dois lugares: o objeto `D.teores` e o vocabulário de busca
em `CHAVES`. Sem o segundo, a busca não acha o cartão pelas palavras da publicação.

Ao mexer no compêndio, altere apenas o bloco `sumulasDados`, que guarda
`{verificadoEm, fontes, registros}`. Cada verbete é um objeto com `id`, `tribunal`, `tipo`,
`numero`, `teor`, `status` e `temas`, e, conforme a espécie, `orgao`, `questao`, `referencia`,
`historico`, `observacao`, `suspensao`, `alerta` e `fonte` (chave do mapa `fontes`) ou
`fonte_url`. Campo vazio é omitido, para não repetir `null` mil e seiscentas vezes.

Os `tipo` reconhecidos são `sumula`, `sumula_vinculante`, `oj`, `oj_transitoria`, `pn`, `irr`,
`iac` e `irdr`; os `status`, `em_vigor`, `cancelada`, `convertida`, `afetado` e `superada`. As
opções de status e a lista de temas se montam sozinhas a partir dos dados: um tema novo vira
opção sem que se toque no código. Espécie nova, porém, pede uma linha em `SUM_ESPECIES` e o
nome por extenso em `sumNome`.

## Dúvidas sobre o conteúdo

Ponto único: advogado júnior trabalhista (Ygor Pinheiro).
