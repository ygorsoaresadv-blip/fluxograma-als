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
| Apresentar para a equipe | Botão **Apresentar**; navegue com `←` `→` ou barra de espaço, saia com `Esc` |
| Imprimir ou gerar PDF | Botão **Imprimir tudo**; monta o documento inteiro |
| Link direto para um cartão | O endereço muda sozinho, por exemplo `#t/8.2`; o manual usa `#m/regras`, e as telas novas usam `#triagem`, `#passos`, `#calc` e `#treino` |

Funciona em celular. A contagem de prazos é sempre em dias úteis.

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

## Dúvidas sobre o conteúdo

Ponto único: advogado júnior trabalhista (Ygor Pinheiro).
