# Projeto: manual e fluxo de publicações do escritório

Guia para quem for alterar este projeto (pessoa ou IA) sem precisar reanalisar o código.
Leia este arquivo primeiro. O `README.md` é o manual de uso para a equipe; este é o manual de manutenção.

- **Site:** https://ygorsoaresadv-blip.github.io/fluxograma-als/
- **Repositório:** https://github.com/ygorsoaresadv-blip/fluxograma-als (branch `main`, GitHub Pages na raiz)
- **Arquivo do site:** um único `index.html` (~3.300 linhas, ~1,5 MB), sem dependências, sem build. Abre com duplo clique.
- **Pasta local:** `Desktop\atualização do fluxograma\repo` (o clone). Fora dele ficam `worker-api-para-o-futuro\` (ver seção 9) e, se existir, `.claude\launch.json` (servidor de prévia).
- **Dono / ponto único de dúvida:** Ygor Pinheiro, advogado júnior trabalhista.

## 1. O que o site faz

| Tela | Rota (hash) | O que é |
|---|---|---|
| Início | `#inicio` | Apresentação, régua PZ/FT, portas de entrada e a grade dos cartões por fase |
| Triagem de publicações (**desativada**: `TRIAGEM_ATIVA = false`) | `#triagem` | Cola-se a publicação, a aba lê os dados, sugere o cartão e monta as agendas (título, data, observações) |
| Como tratar uma publicação | `#passos` | As seis etapas do trabalho |
| Cartões de teor | `#t/7.0` … `#t/9.6` | 23 cartões, um por tipo de publicação, em três fases |
| Manual | `#m/regras`, `#m/pessoas`, `#m/glossario`, `#m/etiqueta` | Seis regras, quem é quem, glossário e o fluxo da etiqueta roxa |
| Compêndio de jurisprudência | `#sumulas`, `#s/<id>` | 1.690 verbetes do TST e do STF, com busca estilo Spotlight |
| Calculadora de prazos | `#calc` | Fatal → prazo interno, e publicação → fatal (com feriados) |
| Tribunais e OAB | `#tribunais` | Tabelas de códigos CNJ e inscrições da OAB do André |
| Principais legislações | `#leis` | Links para o texto oficial no Planalto (CF, CLT, CPC, CC, FGTS); lista `LEIS` no código |
| Organização de docs da reclamada | `#docs` | Manual de organização dos documentos para a contestação, com prompt copiável |
| Substabelecimento e juntada | `substabelecimento.html` (página à parte) | Cola-se a ata e baixam-se os dois .docx. Item de `NAV` com `href`, que `itemNav` desenha como link. É o atalho em destaque da tela inicial e o botão da barra do topo enquanto a triagem estiver desativada |

`substabelecimento.html` é **gerado** pelo projeto "Gerador de Substabelecimento" (pasta `SUBS APP`, com testes e modelos .docx). Não edite à mão: altere lá e rode `node scripts/build.mjs --voltar=index.html --saida=<este repo>/substabelecimento.html`.

Rotas antigas que não existem mais (`#triagem` antiga, `#treino`, `#m/nomenclatura`, `#m/fora`) caem na tela inicial.

## 2. Estrutura do `index.html`

Ordem do arquivo: `<style>` → HTML do esqueleto (índice lateral, barra, `#palco`) → blocos de dados → `<script>`.

1. **CSS** (linhas ~12–670): tokens em `:root` (ver seção 6), depois uma seção por tela. Comentários `/* ---------- nome ---------- */` marcam cada uma.
2. **Blocos de texto puro**, cada um em `<script id="..." type="text/plain">`:
   - `promptDocs`: o prompt de organização de documentos (botão **Copiar prompt**, rota `#docs`).
   - `emailSolicitacaoDocs`: o e-mail do botão **Copiar e-mail de solicitação** (cartão 7.0 e triagem).
   Servem para guardar textos longos sem escapar nada. Para trocar o texto, edite o bloco; o código não muda.
3. **`<script id="sumulasDados" type="application/json">`**: o acervo do compêndio (uma única linha enorme). Só é interpretado quando a tela é aberta.
4. **`<script>` principal**, nesta ordem:
   - `const D = {teores, manual, tribunais}`: **todo o conteúdo do fluxograma**, em uma linha JSON (ver seção 3).
   - `CHAVES`: vocabulário de busca por cartão.
   - Dias úteis com feriados: `pascoa`, `feriadosDoAno`, `emRecesso`, `somaUteis`, `subUteis` (usados pela calculadora).
   - `PECAS`, `PRAZOS_FIXOS`: siglas, folgas e prazos legais (calculadora).
   - Índice: `ICO` (ícones SVG), `NAV` (seções e telas do índice), `blocoCartoes`, `pintaIndice`, `faseAberta` (ver seção 2.1).
   - Telas (`telaInicio`, `telaTeor`, `telaManual`, `telaCalculadora`, `telaTribunais`, `telaSumulas`), régua PZ/FT (`regua`).
   - Compêndio: `sumDados`, `sumInterpreta`, `sumBusca`, `sumPainel`, `sumCartao`, `sumDesenha`…
   - **Triagem**: bloco `/* ---------- triagem ---------- */` (seção 5).
   - `telaDocs` e `DOCS_*` (organização de documentos).
   - Roteamento `ir(rota)`, `rotaValida`, `migalhaDe`, eventos (`click`, `input`, `change`, `keydown`), arranque (`ROTAS_FIXAS`).

### 2.1 O índice lateral

Organizado pelo uso, em cinco seções: **Dia a dia** (triagem, como tratar, etiqueta roxa), **Cartões de teor**
(filtro de área + as três fases recolhíveis), **Ferramentas** (calculadora, organização de docs), **Consulta**
(compêndio, legislações, tribunais) e **Manual** (regras, quem é quem, glossário).

- A lista `NAV` é a fonte única: desenha o índice, os atalhos da tela inicial e alimenta a busca. **Tela nova entra em `NAV`** (com `rota`, `t`, `ico`, `d` e palavras `ch` para a busca) e em `ROTAS_FIXAS` (que `rotaValida` usa).
- As fases abertas ficam em `faseAberta`, guardado no `localStorage` (`indice-fases`). Abrir um cartão abre a fase dele; buscar abre todas as fases com resultado.
- A busca lateral filtra cartões (`casa`) e telas (`casaNav`, que também procura nos nomes de `MAN.pessoas`, nos termos do glossário e nos títulos das regras).
- No celular, o índice abre como gaveta com um véu atrás (`#veu`); tocar no véu ou teclar Esc fecha.
- Rota inválida ou antiga cai na tela inicial em qualquer caminho (`rotaValida` dentro de `ir`).

## 3. Como é um cartão (`D.teores[]`)

```json
{
  "sec": "7.7", "fase": "conhecimento|recursal|execucao",
  "area": "TODAS AS ÁREAS | TRABALHISTA | CÍVEL | PREVIDENCIÁRIO | ...",
  "titulo": "…", "id": "como identificar a publicação",
  "agendas": [
    {"tipo": "PRAZO|AUDIÊNCIA", "titulo": "…", "data": "texto do campo Data",
     "resp": "responsável", "email": "chave do modelo de e-mail (opcional)"}
  ],
  "semAgenda": "texto, só quando não há agenda",
  "nota": "bloco Atenção em cor da fase",
  "alerta": "bloco Atenção em vermelho, abaixo da nota (opcional)"
}
```

- A ordem em `D.teores` é a ordem na tela. O cartão **7.0** (Habilitação de reclamada) é o primeiro.
- `area` define em quais filtros do índice o cartão aparece (`areasDe`).
- Quebra de linha em `data` e `resp` vira linha nova na tela.
- O resto do manual vive em `D.manual`: `pessoas` (tabela Quem é quem), `regras` (seis regras), `glossario`, `etiqueta` (fluxo roxo).

## 4. Como adicionar ou alterar um cartão

Um cartão novo mexe em **quatro lugares**; esquecer um deles quebra uma parte do site:

1. **`D.teores`**: o objeto do cartão (seção 3).
2. **`CHAVES`**: palavras que aparecem na publicação, sem acento, em minúsculas. Alimenta a busca lateral e o palpite da triagem.
3. **`TRI_REGRAS['x.y']`**: a regra da triagem, que devolve as agendas e as contas de data (seção 5). Sem ela, a triagem reconhece o cartão mas não monta agendas.
4. **`TRI_PEDE['x.y']`** (só se precisar de um detalhe que a estagiária confere no passo 4: `prazo`, `aud`, `audato`, `audtipo`, `per`, `contra`, `alvara`).

Depois: se mudar contagem, folga ou responsável, conferir `PECAS` (calculadora) e o `README.md`.

Para só **mudar texto, responsável ou dia** de um cartão existente, altere em `D.teores` **e** em `TRI_REGRAS` (a triagem tem a sua cópia da regra, em código). Os dois precisam ficar iguais.

## 5. A triagem, por dentro

Fluxo na tela: **1** cola a publicação → **2** confere os dados lidos → **3** confirma o cartão → **4** confere detalhes (só quando o cartão pede) → **5** agendas para o Astrea. Sem IA e sem custo.

- **Leitura (`triExtrai`)**: diário, órgão, publicação, processo CNJ, tipo, classe, partes (com ou sem `Polo:`), advogados, conteúdo. A data de publicação é a base de tudo (se faltar, usa o dia útil seguinte à disponibilização e avisa). Área pelo número CNJ (`J=5` trabalhista, `8` cível, `4` previdenciário); rito juizado se a vara/classe disser "Juizado Especial".
- **Palpite (`triPalpites`)**: pontua cada cartão pelas palavras de `CHAVES` + título que aparecem no texto. O primeiro vem marcado; 7.3, 7.4 e 7.5 vêm juntos quando o texto mostra os três (`triPalpitesExtra`).
- **Detalhes (`triDetalhes`)**: prazo do juiz (`triPrazoJuiz`; sem prazo, **5 dias**, art. 218, § 3º, CPC), data e hora de audiência/perícia (`triDataAto`), tipo e endereço, recurso respondido, valor do alvará.
- **Regras (`TRI_REGRAS`)**: cada cartão devolve `{agendas, alertas, infos, perigos}`. Uma agenda usa estes campos: `tipo`, `sigla`, `leva_pz_ft`, `recursal`, `regra_fatal {base, dias_uteis, referencia}`, `regra_pz {tipo, dias_uteis, referencia}`, `data_ato`, `responsavel`, `observacao`, e os marcadores `titulo_ft` (título só com `- FT dd/mm`), `data_pub` (Data = dia da publicação) e `email_modelo`.
  - `base`: `publicacao`, `data_ato`, `outra_agenda` (com `referencia: "agenda:N:pz|ft"`).
  - `regra_pz.tipo`: `antes_do_fatal`, `depois_da_base`, `igual_a`.
  - Funções ajudantes: `triRecurso`, `triPrazoAg`, `triProvid`, `triResp`.
- **Datas (`triCalcula`)**: calcula em rodadas, para suportar agendas que dependem umas das outras. Conta **só dias úteis sem sábado e domingo** (`triSomaUteis`, `triSubUteis`); a soma começa no dia seguinte à base e a subtração não conta a base. Feriados ficam com o advogado responsável. Marca em vermelho "prazo curto" (PZ depois do FT ou antes da publicação) e "data já passou".
- **Campo Data no Astrea**: recurso e contrarrazões → dia da publicação (regra 3); demais prazos → PZ; providência sem fatal → a data calculada; audiência → data e hora.
- **Etiqueta roxa**: se marcada, só gera `CIÊNCIA E PROVIDÊNCIA` no dia útil seguinte, para a Dra. Juliana. Não lê o teor.
- **Exceção**: "Nenhum destes" abre um pedido para colar numa **IA gratuita** (Claude, ChatGPT ou Gemini); a resposta é um JSON que a aba lê (`triLeJSON`) e desenha com a tarja "EXCEÇÃO: validar com o Ygor". O pedido é montado por `triSystem`/`triMensagem`/`triPedido` a partir de `D`, então cartões novos entram sozinhos nele.
- **No Astrea só usamos três campos**: título, data (Data limite no prazo; data e hora na audiência) e observações. O responsável aparece só como lembrete.

## 6. Visual

Estilo Apple com as cores da identidade do escritório, **sempre claro** (não há modo escuro, por decisão do Ygor).

- Tokens em `:root`: fundo `--bg #F6F2EA`, cartões `--elev #FFFFFF`, texto `--label #2C2C2A`, verde `--acento #0C3B2E` (e `--acento-txt #1B6B4C`), dourado `--dourado #C6A35C` (e `--dourado-txt #8F6F2E`).
- **Cores de consulta mantidas**: fases (`--verde`, `--azul`, `--laranja`), espécies do compêndio, status, roxo da etiqueta, vermelho de alerta (`--vermelho`, `--vermelho-bg`).
- Fonte: sistema Apple, com Inter como alternativa. Raios `--r-s/m/l/xl`; animação `--mola`.
- Nomes antigos (`--tinta`, `--ouro`, `--papel`, `--carta`, `--conh`…) ainda existem como apelidos e são usados em estilos inline. Não remova.

## 7. Compêndio de jurisprudência

- Cada verbete: `id`, `tribunal`, `tipo` (`sumula`, `sumula_vinculante`, `oj`, `oj_transitoria`, `pn`, `irr`, `iac`, `irdr`), `numero`, `teor` (rubrica em caixa alta, linha em branco, tese), `status` (`em_vigor`, `cancelada`, `convertida`, `afetado`, `superada`…), `temas`, e opcionais `orgao`, `questao`, `referencia`, `historico [{evento, ato, data, observacao}]`, `observacao`, `alerta`, `fonte`/`fonte_url`, `verificado_em`.
- **Para atualizar um verbete** (exemplo real: Tema 39, que saiu de `afetado` para `em_vigor` em 03/10/2026): leia o bloco `sumulasDados`, altere o registro por `id` com um script Node, regrave com `JSON.stringify` e confira com `git diff --stat` (deve mudar uma linha). Atualize `verificado_em`, ponha a fonte oficial em `fonte_url` e registre no `historico`.
- **Fonte do texto**: use a literal da página oficial do TST. O WebFetch devolve resumo traduzido por um modelo pequeno: peça sempre "copie literalmente, em português". Se não houver o acórdão, deixe uma `observacao` mandando conferir antes de citar em peça.
- **O tema é etiqueta de navegação**, não classificação oficial (ver `README.md`).
- Busca: número entende a espécie (`331`, `OJ 191`, `SDI-2 54`, `PN 119`, `tema 128`, `SV 22`); aspas procuram a frase exata. Tela com atalhos de espécie, chave "só em vigor" e "Mais filtros".

## 8. Regras de negócio decididas pelo Ygor

**Pessoas**
- Dr. André (sócio): audiências trabalhistas de instrução/una **presenciais** (da RF ou dos reclamantes); perícias só para controle; OAB principal SP 284388.
- Gustavo Freire: advogado sênior trabalhista, delegador e revisor (recursos e contrarrazões do trabalhista); audiências trabalhistas de una, inicial e instrução **online**, inclusive da RF.
- Dr. Mateus: advogado pleno trabalhista e **advogado cível** (todo o cível, exceto cálculos e cumprimento de sentença); audiências cíveis (online ou presenciais) e audiências trabalhistas somente de **conciliação online**, inclusive da RF.
- Ygor Pinheiro: advogado júnior trabalhista; cumprimento de sentença, manifestação de cálculos, impugnação ao laudo, e o ponto único de dúvida.
- Elisangela: previdenciário inteiro, e cálculos e cumprimento de sentença do cível.
- Rui: contador externo (liquidação, só trabalhista). Igor Marran: financeiro. Ellen: assistente técnica externa (sem agenda no Astrea).
- **Dra. Juliana Tchani: só o fluxo extraordinário da etiqueta roxa** (`C/ JULIANA TCHANI`). Nunca recebe cartões comuns.
- Letícia Leite: responsável pela agenda SOLICITAR DOCUMENTOS AO CLIENTE (cartão 7.0).
- Estagiária jurídica: trata as publicações e cria as agendas.

**Responsável pela audiência** (cartões 7.0 e 7.2; função `triRespAud`, que depende de área, tipo e modalidade, informados no passo 4 da triagem): trabalhista una, inicial ou instrução online → Gustavo; trabalhista una, inicial ou instrução presencial → André; trabalhista **só** conciliação online → Dr. Mateus; cível, qualquer modalidade → Dr. Mateus. Desde 17/11/2026 o tipo "Inicial" segue a regra de instrução/una (antes era tratado como conciliação). Sem regra definida (caem no André, com alerta): conciliação trabalhista presencial e previdenciário.

**Prazos**
- Toda contagem é em **dias úteis**, sem exceção.
- Sem prazo do juiz nem da lei: **5 dias** (art. 218, § 3º, do CPC).
- **Trabalhista não tem agravo de instrumento** (interlocutórias irrecorríveis). Não tratar como pendência.
- Sigla da audiência: `RT` (trabalhista), `CÍVEL`, `PREV`.
- 8.2 (sentença trabalhista): cumprimento (+20) e liquidação (+15) contam da **data da publicação**, que é a da sentença.
- 7.0 (habilitação de reclamada): audiência é D+0; D-30 solicitar documentos ao cliente (Letícia); D-15 conferir e solicitar documentos complementares, D-10 `CT - TRABALHISTA`, D-2 e-mail com defesa (Gustavo); D+1 ata, D+2 substabelecimento e carta de preposição (Ygor). Títulos só com `- FT dd/mm`, tratado como fatal; campo Data = o FT.
- 7.6 (perícia): contato com cliente D-10 e comunicar Ellen D-5 da perícia.
- 7.7 (quesitos): `SOLICITAR QUESITOS E ASSISTENTES` no dia da publicação; `INDICAR QUESITOS E ASSISTENTES` com PZ = fatal do juízo −2. Alerta fixo: **nunca pedir quesitos e assistentes médicos sem a aprovação do Dr. André; se ele vetar, quesitos genéricos e indicar sem assistentes.**
- 7.8 (laudo): Ellen com PZ = publicação +1 e FT = FT da impugnação −3; impugnação com FT = publicação +5.
- O AI dos cartões 7.3 e 7.5 contra a mesma decisão vira **uma** agenda.

**Conteúdo removido por decisão**: triagem guiada antiga (perguntas), treino, "Nomear e datar", "O que não está aqui", a antiga regra 5 ("Você não calcula o prazo fatal"; ficaram **seis** regras), botões Apresentar e Imprimir, e o checklist "Passo a passo desta publicação" dos cartões (18/11/2026).

## 9. Sem API paga

O Ygor não quer custo com API. A triagem funciona só com regras locais; as exceções vão para IA gratuita por copiar e colar. O código de um Worker da Cloudflare (que chamaria a API da Anthropic com a chave guardada em segredo) foi escrito e testado e está **fora do repositório**, em `Desktop\atualização do fluxograma\worker-api-para-o-futuro\`. Se um dia valer a pena ligar a API, ele está pronto; nunca coloque chave no `index.html`.

## 10. Como alterar sem quebrar (armadilhas já encontradas)

1. **`index.html` e `README.md` usam CRLF.** Ao editar por script, normalize (`split('\r\n').join('\n')`) e regrave com CRLF. Sem isso, buscas por texto de várias linhas falham.
2. **Não passe regex com `\` pelo shell.** As barras somem. Escreva o script de alteração num arquivo `.js` e rode com `node`, com trocas literais (`s.replace(a, () => b)`, com função, para o `$` não ser interpretado).
3. **Use trocas exatas com checagem**: se o trecho antigo não existir, o script deve parar com erro. Evita edição silenciosa errada.
4. **Valide a sintaxe do script do site depois de editar**: extraia o último `<script>…</script>` e rode `new Function(js)`.
5. **Linhas gigantes** (`const D`, `sumulasDados`): não abra com o Read inteiro; altere por script (parse do JSON, mude, `JSON.stringify`).
6. **Teste no navegador antes de publicar**: servidor local em `http://localhost:5317` lendo o `index.html` (configuração em `Desktop\atualização do fluxograma\.claude\launch.json`, com `node -e` servindo o arquivo). Rotas de teste: `#t/7.0`, `#triagem`, `#docs`, `#s/irr-39`. Cole publicações de exemplo na triagem e confira título, data e responsável de cada agenda. Os testes feitos até aqui cobrem 7.0, 7.2, 7.3–7.5, 7.6, 7.7, 7.8, 8.1, 8.2, 8.8, 9.1, 9.3, 9.6 e etiqueta roxa.
7. **Cache do navegador**: ao testar, use `?v=N` na URL.
8. **Publicar**: `git add`, `git commit`, `git push origin main`. O GitHub às vezes responde "Internal Server Error": repita. **Confirme o envio comparando `git rev-parse HEAD` com `git rev-parse origin/main`** (a mensagem `main -> main` aparece também na rejeição). Depois confira o site com `curl` procurando um trecho novo. Se o Pages demorar demais, um commit vazio (`git commit --allow-empty`) força nova publicação.
9. **Git no computador do Ygor**: autor configurado só neste repositório (`Ygor Pinheiro`, `ygorsoaresadv@gmail.com`). Mensagens de commit em português, dizendo o que mudou e por quê.
10. **Sempre atualize o `README.md`** quando mudar o que o site faz, e este `PROJETO.md` quando mudar uma regra de negócio ou a estrutura.

## 11. Pendências conhecidas (confirmar com o Ygor quando surgir a ocasião)

- Letícia Leite não está na tabela **Quem é quem** (falta cargo e o que recebe).
- Responsáveis do 7.7: foram assumidos `Estagiária jurídica` (solicitar) e o advogado da área, no trabalhista Ygor (indicar). Confirmar.
- No e-mail de solicitação de documentos, o `XX/XX/XXXX` (data limite) é preenchido por quem envia; não há regra automática.
- Na tabela de organização de documentos, o item 14 (uniformes, conjunto 1) vem depois do 13 (EPIs, conjunto 2), como no texto original do Ygor.
- A triagem não conhece feriados, recesso nem suspensões (decisão): só sábado e domingo.
- Datas de audiência, perícia e prazo do juiz são lidas do texto por palavras; sempre conferidas pela estagiária no passo 4.

- Audiência trabalhista de **conciliação presencial** e audiência previdenciária não estão na regra de responsáveis: a triagem as deixa com o André e avisa. Confirmar quem fica. O site escreve "Dr. Mateus" (o Ygor citou "Matheus Soares"); conferir a grafia.

## 12. Artefatos fora do site

Existiram duas prévias no Claude (privadas): o fluxo temporário "Habilitação em lote" (agenda do Freire no sábado) e uma prévia da tela de organização de documentos, hoje já publicada no site. O fluxo temporário **não faz parte** do fluxograma oficial.
