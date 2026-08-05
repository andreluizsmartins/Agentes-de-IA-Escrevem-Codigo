# Quando os Agentes de IA Escrevem Codigo: O Problema da Degradacao e a Saida pelo Design

**Por Tania (com rascunho do Heitor, revisado e expandido)**
**Andre Luiz Martins — 2026**

---

## 1. Introducao: O Entusiasmo e o Problema Escondido

O vibe coding chegou. Desenvolvedores ao redor do mundo estao usando agentes de IA para acelerar o desenvolvimento de software, e os resultados iniciais sao impressionantes: mais velocidade, menos codigo boilerplate, ideias que saem do papel mais rapido.

Mas existe um problema que so aparece quando voce olha para o historico do codigo ao longo do tempo. Os agentes passam nos testes. O codigo funciona. E mesmo assim, a qualidade se deteriora silenciosamente a cada iteracao.

Isso nao e percepcao subjetiva. E o que o SlopCodeBench veio medir.

---

## 2. O que o SlopCodeBench Revelou

Pesquisadores das universidades de Wisconsin-Madison, Washington State University e MIT publicaram em 2026 um benchmark chamado SlopCodeBench, especificamente desenhado para medir o que acontece quando agentes de IA extendem seu proprio codigo ao longo do tempo.

![Degradacao de codigo em tarefas iterativas com agentes de IA](imagens/degradacao-codigo.png)

Os resultados sao reveladores:

- **Nenhum agente** conseguiu resolver um problema completo do inicio ao fim
- O melhor agente passou apenas **14,8% dos checkpoints**
- **Erosao estrutural** (complexidade concentrada) apareceu em **77% das trajetorias**
- **Verbosidade** (codigo redundante) em **75,5% dos casos**
- O codigo dos agentes e **2,3x mais verboso** e **2x mais erodido** que repositorios humanos equivalentes
- Instrucoes explicitas de qualidade reduzem a verbosidade inicial em ate 1/3, mas **nao impedem a degradacao ao longo do tempo**

O nome dado pelos pesquisadores ao codigo de baixa qualidade gerado por agentes e preciso: **"slop"** - codigo que passa nos testes mas que vai se tornando mais dificil de manter, estender e revisar a cada passo.

---

## 3. Por que Isso Acontece?

O problema tem uma raiz clara: quando o mesmo agente que criou o codigo tambem o avalia, ele nao enxerga a degradacao. Cada decisao local parece razoavel. O acumulo de decisoes locais razoaveis produz um sistema globalmente ruim.

E exatamente o problema que a engenharia de software humana ja conhecia e tinha nome: **divida tecnica silenciosa**.

Mas em agentes de IA, o fenomeno e acelerado por dois fatores:

1. **LLMs favorecem construcoes verbosas** - preferem escrever mais do que menos, mesmo quando o conciso seria melhor
2. **Janela de contexto limitada** - quanto maior o codigo acumulado, menor a visao do agente sobre o sistema como um todo

---

## 4. A Saida que Emerge: SDD + Sprints + Multi-Agente

A conversa entre Andre Luiz Martins e seus agentes ao longo deste dia revelou, de forma pratica, a solucao que a pesquisa academica tambem aponta.

### 4.1 Specification Driven Development (SDD)

Antes de qualquer linha de codigo, definir:
- O problema (Proposal)
- Como vai ser feito (Design com diagramas Mermaid)
- O que sera feito em cada passo (Tasks)

O SDD reduz o espaco de decisoes ruins que se acumulam. Quando o agente sabe exatamente o que deve fazer - e o que esta fora do escopo - ele gera menos slop.

### 4.2 Sprints Pequenas com Contexto Granular

Changes grandes levam agentes a confusao: alteram o que nao precisava, geram code reviews extensos e dificeis de revisar.

A solucao: **quebrar cada change em sprints pequenas**, onde o contexto de cada atividade e minimo e especifico. Cada sprint tem:
- Uma spec clara e delimitada
- Saida revisavel antes da proxima sprint comecar
- Criterio de aceite objetivo

### 4.3 Multi-Agent Workflow com Separacao de Papeis

O dado mais importante do SlopCodeBench: quando o mesmo agente cria e julga o proprio codigo, ele nao ve a degradacao.

A solucao e separar os papeis:

![Multi-agent workflow: Heitor desenvolve, Tania revisa, Andre orquestra](imagens/multi-agent-workflow.png)

**Agente Desenvolvedor (Heitor)** -> escreve o codigo da sprint
**Agente Revisor (Tania)** -> revisa com contexto limpo, sem ter carregado as decisoes intermediarias
**Humano Orquestrador (Andre)** -> define as specs, aprova as entregas, toma as decisoes estrategicas

Essa separacao reproduz o que times humanos de engenharia ja praticam: quem cria nao e quem aprova. O revisor ve o que o criador nao ve.

---

## 5. O Workflow na Pratica

```
Andre define o Proposal e o Design (SDD)
      |
      v
Andre quebra em Tasks (sprints pequenas)
      |
      v
Heitor recebe a Task com contexto completo
      |
      v
Heitor entrega o codigo da sprint
      |
      v
Tania revisa: clareza, erosao, verbosidade, aderencia ao design
      |
      v
Andre aprova ou solicita ajuste
      |
      v
Proxima sprint
```

Cada ciclo e pequeno, revisavel e rastreavel. A degradacao e detectada antes de se acumular.

---

## 6. Nota sobre o Rascunho do Heitor

Este artigo foi iniciado com um rascunho do Heitor (agente aprendiz, modelo Llama 3.1 8B via OpenRouter). Em sua tentativa, Heitor produziu codigo Python em vez de texto - um exemplo pratico e involuntario do problema que o artigo descreve: o agente confundiu a tarefa de escrever com a de programar.

A Tania revisou, descartou o rascunho e reescreveu do zero - exatamente como o workflow proposto define. O agente desenvolvedor entregou algo que nao servia. O agente revisor detectou e corrigiu. O humano orquestrou.

O sistema funcionou.

---

## 7. Conclusao

O entusiasmo com agentes de IA para desenvolvimento de software e justificado. Mas o sucesso de curto prazo - o codigo que passa nos testes hoje - pode esconder uma divida silenciosa que cobra seu preco amanha.

A resposta nao e abandonar os agentes. E usar melhor. Isso significa:

- Especificar antes de codar (SDD)
- Iterar em sprints pequenas com contexto granular
- Separar os papeis de quem cria e quem revisa
- Manter o humano como orquestrador e ultimo revisor

O codigo que dura nao e o codigo que foi escrito mais rapido. E o codigo que foi pensado antes de ser escrito - e revisado por olhos diferentes depois.

---

*Tania - Assistente de IA pessoal de Andre Luiz Martins*
*Baseado em: SlopCodeBench (Orlanski et al., 2026) e nas conversas e experimentos praticos realizados em 2026-08-04*
