# A ideia: DAW só de MIDI para orquestra virtual

> Registrada em 25/10/2026, a partir de uma conversa do Sergio durante o redesenho do Switchboard do Regni Ensemble.
> Nada aqui foi implementado. As afirmações sobre o que outras DAWs fazem estão marcadas com **(verificar)**.
> Elas precisam ser conferidas no manual de cada uma (fonte primária) antes de virar argumento de produto.

## Por que existir

As DAWs mais usadas cresceram em torno de gravação de áudio, mixagem e produção de banda e eletrônico. Quem escreve
para orquestra virtual passa o dia brigando com problemas que, para esse público, são o centro do trabalho:

## Os problemas que ela ataca

### 1. A latência das articulações (o problema principal)
Cada articulação de uma sample library demora um tempo diferente para "soar". Um legato de cordas pode levar
~200–300 ms; um staccato, quase nada. E isso não é um número fixo: varia com

- a **transição**: a primeira nota de um legato responde rápido, já a nota *ligada* demora mais;
- a velocity e a dinâmica (CC1);
- a região do teclado;
- a lib e o patch.

**O que acontece hoje.** Ao vivo ninguém consegue eliminar esse atraso, porque o sample não toca antes da tecla.
Por isso o músico **toca adiantado, de ouvido**. A DAW grava a nota onde a tecla foi apertada, ou seja, adiantada
e fora do grid. A solução comum é um *track delay* negativo, que só age no playback e é um número por track, não por
articulação **(verificar: Logic, Cubase, Studio One, Dorico, Reaper)**. O compositor acaba quantizando e
arrastando nota na mão.

**O que a gente quer.**
- **Gravar a nota onde ela soou**: o momento da tecla mais o delay daquela articulação naquela situação.
  A nota cai no grid do jeito que o músico quis.
- **No playback, mandar a nota adiantada** exatamente pela mesma quantia.
- O grid passa a mostrar a intenção musical, e a física da lib fica escondida.
- Uma opção para quem *não* toca adiantado (aí não há compensação na gravação, só no playback).
- Os delays vêm de **presets prontos por lib** (medidos por nós), com regras (transição, velocity, dinâmica,
  região), e o usuário edita e salva os próprios.

Isso **não dá para fazer só com um plugin** dentro de outra DAW: quem grava o MIDI é a DAW, antes de o plugin
recebê-lo. É a razão principal para este produto existir.

### 2. Articulação por nota, sem dor
Trocar de articulação hoje é configurar articulation sets ou expression maps presos à DAW e à lib, montados à mão
ou comprados prontos e fixos (Babylonwaves) **(verificar o que cada DAW já oferece por nota)**.

O que a gente quer, na mesma lógica de três camadas do Switchboard do Ensemble:
- **Paleta:** as suas articulações, com os seus nomes e teclas, customizável, com várias paletas;
- **Instrumento:** o que a lib realmente tem;
- **Conexões:** o cabo entre a paleta e o instrumento, com presets prontos.

Mais: articulação como propriedade da nota no piano roll, não como notas de keyswitch poluindo o roll.

### 3. "Chase" de estado ao começar no meio
Começar o playback no meio da música e ouvir a articulação ou o CC errado, porque o último keyswitch ou CC ficou
antes do ponto de início **(verificar como cada DAW faz o chase de keyswitch)**. A DAW deve sempre saber e mandar o
estado certo de cada instrumento em qualquer ponto.

### 4. Templates enormes
Templates de orquestra com centenas de instrumentos demoram para abrir, pesam na RAM e travam o projeto. O Regni
Ensemble já hospeda os instrumentos fora da DAW. Aqui ele vira nativo: o template é carregado uma vez e o projeto só
aponta para ele.

### 5. CCs pensados para orquestra
Dinâmica (CC1), expressão (CC11) e vibrato desenhados como curvas musicais. Coisas como "esta seção toda faz um
crescendo", e ajustar a dinâmica de várias linhas juntas.

## O que ela PRECISA ter mesmo sendo "só MIDI"
- tempo map e mudanças de compasso;
- **sync de vídeo**, porque o público é de trilha sonora;
- exportar stems (renderização de áudio, feita pelo Ensemble);
- piano roll e edição de MIDI de primeira.

## O que ela NÃO faz (de propósito)
- gravação de áudio, comping, edição de voz;
- mixagem profunda (no máximo níveis e stems);
- correr atrás de toda feature de DAW genérica.

## Perguntas em aberto
- Como a gente mede o delay de cada articulação de cada lib (automático, por análise do áudio renderizado?).
- O formato dos presets de latência e de paleta, compartilhável entre os produtos e entre usuários.
- Notação: integrar com o Regni Notação ou ficar só no piano roll?
- Plataforma: só macOS no início? JUCE, como o Ensemble?
- Nome do produto.

## Antes de começar a construir
1. Ler os manuais (Logic, Cubase, Studio One, Dorico, Reaper) e confirmar ou derrubar cada **(verificar)** acima.
2. Ter a camada de Latência e o Switchboard do Ensemble prontos e testados no uso real. Eles são o motor.
