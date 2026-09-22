# Publicações — manual e fluxo do escritório

Material interno de tratamento de publicações no Astrea, reunido em um único arquivo HTML,
sem dependências, sem instalação e sem servidor. Abre com duplo clique em qualquer navegador.

## O que tem dentro

- **Triagem guiada.** Três ou quatro perguntas sobre o teor levam ao cartão certo, sem
  exigir que a pessoa já saiba o nome da peça. Começa sempre pela etiqueta roxa.
- **Como tratar uma publicação.** As seis etapas do trabalho, da abertura no Astrea até a
  conclusão, na ordem em que acontecem.
- **22 cartões de teor**, um por tipo de publicação, agrupados nas três fases do processo
  (conhecimento, recursal e execução), com as agendas a criar, as datas e o responsável.
  Cada cartão traz um passo a passo marcável e o que ter em mãos antes de perguntar ao Ygor.
- **Calculadora de prazos**, com duas contas: do prazo fatal para o prazo interno, que
  devolve o título da agenda pronto para copiar, e da publicação para o prazo fatal.
  Conhece fins de semana, feriados nacionais, Carnaval, Sexta-feira Santa, Corpus Christi
  e o recesso de 20/12 a 20/01, e mostra quais dias pulou.
- **Treino**: oito publicações descritas como chegam, para reconhecer os teores antes de
  tratar publicação sozinha.
- **Manual completo**: as sete regras gerais, quem é quem, como nomear e datar uma agenda,
  glossário de siglas e termos, e o que não passa pelo tratamento de publicações.
- **Compêndio de súmulas**: 544 súmulas do TST e do STF em matéria trabalhista, com teor
  integral, status atual, temas e histórico de redações. Busca por número (`331`, `SV 22`),
  por palavra-chave ou por frase entre aspas, filtros de tribunal, status e tema, e botões
  para copiar o teor pronto para citação ou o link direto da súmula.
- **Fluxo extraordinário da etiqueta roxa** (`C/ JULIANA TCHANI`), que se sobrepõe a todos os cartões.
- **Tribunais e OAB**: código de segmento e sigla de TJ, TRF e TRT, e as inscrições do André.

## Como usar

| Ação | Como |
|---|---|
| Não sei qual cartão é | **Triagem guiada**, na página inicial ou no índice |
| Buscar um teor | Digite na busca da coluna esquerda, ou tecle `/` |
| Buscar pelas palavras do juiz | A busca aceita trechos da publicação, como `manifestem sobre os cálculos` |
| Filtrar por área | Trabalhista, cível ou previdenciário, nas pastilhas do topo do índice |
| Montar o título da agenda | **Calculadora**, aba *Do fatal para o prazo interno* |
| Acompanhar o tratamento | O passo a passo dentro de cada cartão, que zera ao fechar o arquivo |
| Consultar uma súmula | Botão **Compêndio** no topo, ou `Compêndio de súmulas` no índice |
| Achar a súmula pelo número | Na busca do compêndio: `331`, `SV 22`, `STF 440` |
| Achar a súmula pelo teor | Palavras soltas, ou frase entre aspas, como `"empresa interposta"` |
| Ver se o termo buscado também é súmula | A busca da coluna esquerda mostra quantas súmulas casam e leva até elas |
| Citar uma súmula em peça | Botão **Copiar teor** no rodapé do cartão; sai com tribunal, número, teor e fonte |
| Apresentar para a equipe | Botão **Apresentar**, no pé do índice; navegue com `←` `→` ou barra de espaço, saia com `Esc` |
| Imprimir ou gerar PDF | Botão **Imprimir tudo**, no pé do índice; monta o documento inteiro |
| Link direto para um cartão | O endereço muda sozinho, por exemplo `#t/8.2`; o manual usa `#m/regras`, as telas novas usam `#triagem`, `#passos`, `#calc` e `#treino`, e cada súmula tem o seu, como `#s/tst-331` |

Funciona em celular. A contagem de prazos é sempre em dias úteis.

## Sobre o compêndio de súmulas

É conferência rápida, não a fonte. O status e o teor mudam por resolução do tribunal, e o
acervo aqui foi verificado em 21/09/2026, a partir da pesquisa de jurisprudência do TST e do
portal de súmulas do STF. Antes de citar em peça, confira na fonte oficial — o link está no
rodapé de cada cartão. As súmulas canceladas continuam no acervo, com a tarja cinza, porque
aparecem em publicação antiga e em acórdão; para escondê-las, use *Ver só as que estão em vigor*.

O acervo vive em um bloco `<script id="sumulasDados" type="application/json">` dentro do
próprio `index.html`, e só é interpretado quando faz falta, para não atrasar a abertura. Por
causa dele o arquivo passou de 128 KB para cerca de 830 KB, o que o GitHub Pages entrega
compactado e o navegador lê em fração de segundo.

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

Ao criar um cartão novo, lembre de três lugares: o objeto `D.teores`, o vocabulário de busca
em `CHAVES` e a árvore de perguntas em `TRIAGEM`. Sem o segundo, a busca não acha o cartão
pelas palavras da publicação; sem o terceiro, a triagem não chega até ele.

Ao mexer no compêndio, altere apenas o bloco `sumulasDados`. Cada súmula é um objeto com
`id`, `tribunal`, `tipo`, `numero`, `teor`, `status`, `temas`, `historico`, `fonte_url` e
`verificado_em`. Os filtros de status e a lista de temas se montam sozinhos a partir dos
dados: um tema novo vira pastilha sem que se toque no código.

## Dúvidas sobre o conteúdo

Ponto único: advogado júnior trabalhista (Ygor Pinheiro).
