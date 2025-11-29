<div align="center" style="background-color: #000">

<img src="https://i.imgur.com/HfKlxGv.png" width=600 style="display:block; margin: 0 auto; margint-top: 20px; background-color: #000" />
</div>

Biblioteca de análise prosódica para textos em Português Brasileiro (PT-BR). Auxilia sistemas de Text-to-Speech (TTS) na geração de falas mais naturais e expressivas através de metadados prosódicos baseados em sintaxe e regras fonológicas.

## Como foi feito

Esta biblioteca foi desenvolvida para preencher uma lacuna na geração de voz sintética em português brasileiro, implementando algoritmos de análise prosódica baseados em pesquisa acadêmica. O sistema não gera áudio diretamente, mas fornece metadados prosódicos essenciais (curvas de pitch, duração, atitude) que permitem a motores TTS criarem vozes mais expressivas e naturais.

### Técnicas utilizadas:
- **Análise Sintática**: Detecção automática de intenções através de pontuação e palavras-chave
- **Regras Fonológicas**: Implementação de classificações tônicas (Oxítona/Paroxítona/Proparoxítona)
- **Modelos Prosódicos**: Curvas de entonação baseadas em atos de fala pragmáticos
- **Unicode Normalization**: Remoção de acentos para processamento fonológico consistente
- **Expressões Regulares**: Padrões eficientes para detecção de terminações e estruturas
- **TypeScript**: Tipagem forte para interfaces de análise prosódica

## Como funciona

A biblioteca funciona através de três componentes principais que analisam uma frase de entrada:

1. **Detector de Intenção**: Identifica a atitude pragmática baseada em pontuação e palavras-chave
2. **Analisador Léxico**: Classifica a tonicidade da última palavra para ajustes prosódicos
3. **Gerador de Instruções**: Produz diretrizes abstratas para motores TTS

### Atitudes suportadas:
- **NEUTRA**: Sentença declarativa padrão
- **QUESTAO_SN**: Perguntas Sim/Não (subida final)
- **QUESTAO_QU**: Perguntas abertas (pico na palavra interrogativa)
- **COMANDO**: Ordem direta (ataque alto, declínio rápido)
- **IRONIA**: Sentido oposto (curva complexa com pico final)
- **INCERTEZA**: Dúvida (tom hesitante com pausas)
- **OBVIA**: Informação conhecida (ênfase ascendente)

### Exemplo de uso:
```typescript
import { AnalisadorProsodico } from '@purecore/prosodybr';

const analisador = new AnalisadorProsodico();

// Análise automática baseada em pontuação
const resultado = analisador.analisarFrase("Você vai sair agora!");

console.log(resultado.atitude_detectada); // "COMANDO"

// Instruções para TTS
console.log(resultado.instrucoes_tts);
/*
{
  curva_pitch: "Ataque alto (H*L), declínio rápido",
  modificacao_duracao: "Encurtamento relativo (rispidez)",
  descricao_pragmatica: "Ordem direta. Requer ataque forte no início da frase."
}
*/
```

## Como testar

1. **Instalação**: `npm install @purecore/prosodybr`
2. **Uso básico**:
```typescript
import { AnalisadorProsodico } from '@purecore/prosodybr';

const analisador = new AnalisadorProsodico();

// Teste com diferentes tipos de frase
console.log(analisador.analisarFrase("Você vai sair agora!"));
console.log(analisador.analisarFrase("Será que ele vem?"));
console.log(analisador.analisarFrase("Claro que sim..."));

// Forçando atitude específica
console.log(analisador.analisarFrase("Que interessante.", "IRONIA"));
```

3. **Testes recomendados**:
   - Frases interrogativas: `"Onde você está?"`, `"Será que funciona?"`
   - Frases imperativas: `"Saia imediatamente!"`, `"Pare agora mesmo!"`
   - Expressões irônicas: `"Claro que eu acredito..."`, `"Que surpresa..."`

## Funcionalidades

### ✅ Detecção de Atitude Pragmática
Identifica intenções comunicativas através de análise sintática e lexical.

### ✅ Análise Fonológica
Classifica palavras por tonicidade (Oxítona, Paroxítona, Proparoxítona) baseada em regras do português brasileiro.

### ✅ Instruções TTS Abstratas
Gera diretrizes para ajuste de:
- **Frequência Fundamental (F0)**: Curvas de pitch para entonação
- **Duração Fonética**: Modificações de tempo em sílabas tônicas
- **Intensidade**: Ênfase pragmática

### ✅ Base Científica
Implementação baseada em pesquisas acadêmicas validadas:
- Thomaz, L. A. (2012): Modelagem de Prosódia para Conversores Texto-Fala
- Santos, P. da S. (2010): Uma proposta de descrição prosódica dos atos de fala

## CHANGELOG

Para ver todas as mudanças e melhorias implementadas, consulte o [CHANGELOG.md](./CHANGELOG.md).

---

**Fontes de informação:**
- [Thomaz (2012) - Modelagem de Prosódia](https://www.teses.usp.br/teses/disponiveis/55/55134/tde-24092012-143033/)
- [Santos (2010) - Descrição Prosódica dos Atos de Fala](https://www.teses.usp.br/teses/disponiveis/8/8133/tde-08072011-154816/)
- [MDN Web Docs - Unicode Normalization](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/normalize)
- [Wikipédia - Prosódia](https://pt.wikipedia.org/wiki/Pros%C3%B3dia)