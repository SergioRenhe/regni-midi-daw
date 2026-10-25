# Regni MIDI DAW (nome provisório)

Uma DAW **só de MIDI**, feita para quem compõe com sample libraries, principalmente orquestra virtual.
Não tenta competir com o Logic, o Cubase ou o Pro Tools em áudio. Faz uma coisa: tirar do caminho do compositor
os problemas que as DAWs comuns nunca resolveram porque o foco delas era outro.

Status: **ideia registrada em 25/10/2026, nada implementado.** A ideia completa está em [IDEIA.md](IDEIA.md).

## Em uma frase
O grid mostra a **intenção musical**. A DAW cuida da física das libs: latência de cada articulação, keyswitches,
CCs e carregamento do template.

## Relação com os outros produtos Regni
- **Regni Ensemble** (`~/dev/regni-ensemble`) é o motor: hospeda os instrumentos, faz o Switchboard (articulações)
  e a camada de Latência. A DAW é um front-end que conversa com ele, e não reescreve nada disso.
- Filosofia de todo produto Regni: **presets prontos**, por lib e por instrumento, e o usuário **customiza tudo e
  salva os próprios presets**.
