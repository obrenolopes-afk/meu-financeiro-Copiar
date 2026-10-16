# Meu Financeiro — versão inicial

Aplicativo web instalável (PWA) para controle financeiro pessoal, com visual premium escuro.

## Recursos desta versão
- Cadastro manual de receitas e despesas.
- Saldo, totais mensais e gastos por categoria.
- Contas e parcelas com status paga/pendente, filtradas pelo mês de vencimento selecionado.
- Cadastro de cartões e estimativa do limite usado com despesas vinculadas.
- Relatórios e insights automáticos locais baseados nos dados cadastrados.
- Exportação de backup JSON e movimentações CSV.
- Armazenamento local no navegador.

## Limitações importantes
- Os insights são regras locais, não um modelo de IA conectado.
- Não há sincronização em nuvem, login ou conexão com bancos.
- Dados do navegador podem ser perdidos ao limpar os dados do site ou trocar de aparelho. Exporte backups.
- Esta versão é um protótipo funcional; teste os cálculos e não a use como único registro financeiro.
- Não armazene números completos de cartão, validade, CVV ou senhas bancárias.

## Como testar no computador
Abra `index.html` em um navegador moderno. Para recursos PWA completos, sirva os arquivos via HTTPS ou servidor local.

## Como testar no iPhone
A forma mais simples é publicar os arquivos em um serviço de hospedagem estática HTTPS (por exemplo, GitHub Pages) e abrir o endereço no Safari:
1. Crie um repositório no GitHub e envie `index.html`, `manifest.webmanifest` e `sw.js` para a raiz.
2. Ative Pages nas configurações do repositório e aguarde o endereço HTTPS.
3. Abra o endereço no Safari do iPhone.
4. Toque em Compartilhar → Adicionar à Tela de Início → Adicionar.
5. Abra pelo novo ícone e faça lançamentos de teste.
6. Exporte um backup em Configurações antes de trocar de aparelho ou limpar dados.

O nome exato de alguns menus pode variar conforme a versão do iOS. Não é necessário publicar na App Store para testar como PWA.

## Próxima etapa para uma versão nativa
Para um app nativo de iPhone, podemos migrar a interface para SwiftUI/Xcode ou uma stack multiplataforma, adicionar testes automatizados, armazenamento mais robusto e, se necessário, sincronização segura. Publicar na App Store exige conta Apple Developer e revisão da Apple.


## Teste do controle mensal
1. Selecione um mês no seletor no topo.
2. Cadastre uma receita e uma despesa com datas nesse mês.
3. Cadastre uma conta com vencimento nesse mês.
4. Mude para outro mês: os totais e a lista de contas devem mudar para o novo período.
5. Volte ao primeiro mês: os lançamentos e a conta devem continuar lá.
6. O cadastro do cartão permanece disponível em todos os meses, mas o uso mostrado é calculado para o mês selecionado.


## Continuidade mês a mês (versão atualizada)
- O saldo principal é acumulado: soma receitas menos despesas registradas até o mês selecionado.
- Os totais de entradas, saídas, categorias e relatórios continuam sendo do mês selecionado.
- Ao registrar uma despesa, é possível escolher de 1 a 24 parcelas mensais; o app cria um lançamento para cada mês, com o valor dividido em centavos para fechar exatamente o total.
- Contas podem ser repetidas por vários meses; cada ocorrência aparece no mês de vencimento escolhido.
- Ao marcar uma conta como paga, o app registra automaticamente uma despesa na data do vencimento. Se reabrir a conta, remove essa despesa gerada.
- Para evitar dupla contagem, não registre também o pagamento total da fatura como despesa se as compras parceladas já estão lançadas individualmente.
- Os dados seguem armazenados apenas no navegador/aparelho atual; não há sincronização entre dispositivos.


## Importação de imagem
- A tela Movimentações permite selecionar um print/foto e extrair possíveis despesas via OCR no navegador (biblioteca Tesseract.js carregada por CDN).
- A extração pode errar valores, datas e descrições; revisar antes de importar é obrigatório. A categorização é baseada em palavras-chave, não IA generativa.
- A imagem é processada no navegador, mas a biblioteca de OCR é carregada de um CDN externo. Evite imagens com dados completos do cartão.
