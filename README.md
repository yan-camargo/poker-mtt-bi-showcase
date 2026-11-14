<div align="center">

**Português** · [English](README.en.md) · [Español](README.es.md)

# Poker MTT BI

**O app onde acompanho meus torneios de poker: painéis, o financeiro do time e um assistente com IA local que responde e lança as coisas por mim.**

<img src="docs/img/resumo-escuro.png" alt="Tela Resumo no tema escuro" width="900">

<sub>Código fechado · imagens com dados fictícios</sub>

</div>

## Por que existe

Jogo torneios online (MTT) todos os dias, dentro de um time. O time tem regras próprias de divisão: o makeup (prejuízo acumulado, que precisa ser recuperado antes de dividir lucro), o deal (a parte do lucro que fica comigo), o rakeback (parte das taxas pagas que volta) e uma meta semanal. Eu controlava tudo em planilha, e conferir se cada pagamento batia virou trabalho de horas.

Hoje eu marco os registros do dia e o app faz o resto. Mostra como estou indo, calcula o que o time me deve e me avisa quando alguma coisa não bate.

## Resumo

O mês num olhar: lucro, ROI, a curva da carreira, o melhor torneio, o resultado por categoria e por conta, e quanto falta para a meta de rake da semana.

<img src="docs/img/resumo-claro.png" alt="Tela Resumo no tema claro" width="900">

## Diário e Torneios

O calendário mostra cada dia jogado e o resultado dele. Clicando num dia aparecem os destaques. Em Torneios fica a lista completa, com busca, filtros e exportação para planilha.

<img src="docs/img/diario.png" alt="Tela Diário" width="900">

<img src="docs/img/torneios.png" alt="Tela Torneios" width="900">

## Financeiro

O app refaz o makeup dia a dia desde o primeiro torneio, com as regras do time de cada época. Mostra a semana atual, as semanas fechadas, os saques recebidos e quanto falta para liberar o rakeback.

<img src="docs/img/financeiro.png" alt="Tela Financeiro" width="900">

## Pool

Colo o relatório diário que o time manda e o app confere os totais, divide a cota de cada jogador e soma o mês.

<img src="docs/img/pool.png" alt="Tela Pool" width="900">

## Assistente com IA local

Um chat dentro do app, com um modelo de linguagem (Qwen, `qwen3.5:4b`) rodando na minha própria placa de vídeo. Não tem custo de API, e nenhum dado sai do computador.

- **Pergunto em vez de procurar:** "quanto lucrei em novembro?", "qual conta mais perdeu em outubro?", "quanto o time já me pagou em setembro?".
- **Lança por mim:** escrevo "caiu 136,20 do diário de 05/11 no Banco Inter" e ele monta o saque. Nada é gravado até eu clicar em **Gravar**.
- **Me avisa:** saque calculado que não caiu, dia da pool sem relatório, registro que precisa de conferência.

O modelo só entende o pedido. Quem faz as contas é o próprio app, então os números que ele mostra são os mesmos das outras telas.

Escolhi o modelo medindo. Testei 7 modelos locais em 22 pedidos reais. O `qwen3.5:4b` acertou 19, sem inventar filtro e sem tentar gravar sozinho, em 5,4 s por resposta. O `qwen3:8b`, com o dobro do tamanho, acertou os mesmos 19, mas inventou 12 filtros que ninguém pediu e levou 50 s. Três dos seis modelos que rodaram tentaram gravar no banco sem confirmação, e é por isso que só o clique grava. O teste também mostrou que boa parte do erro estava no formato do pedido, não no modelo: quando ele passou a mandar só "mês passado" e o app a calcular as datas, os acertos subiram de 13 para 18.

<img src="docs/img/assistente.png" alt="Assistente respondendo uma pergunta e propondo um saque" width="900">

## Grade

A grade semanal de torneios do time, puxada da planilha dele.

<img src="docs/img/grade.png" alt="Tela Grade" width="900">

## Feito com

Construí orquestrando agentes de IA (Claude Code e Gemini), no estilo *vibe coding*. Eu escrevo as regras e o critério de aceite de cada funcionalidade e divido o trabalho em tarefas pequenas. Os agentes escrevem o código, outro agente revisa cada entrega sem ter visto como ela foi feita, e nada entra sem passar nos mais de 1.800 testes automatizados. Depois eu confiro no uso de todo dia.

Por baixo: C# e .NET 10 no servidor, React e TypeScript na interface, SQLite como banco e Ollama para o modelo local. Roda inteiro no meu computador, com tema claro e escuro.

---

<sub>Feito por **Yan Camargo** · [LinkedIn](https://www.linkedin.com/in/yancaecamargo) · © 2026, todos os direitos reservados ([LICENSE](LICENSE))</sub>
