# 🐕‍🦺 CEPK Rush — Corrida do Kennedito

Jogo 2D estilo Sonic (SNES) com o mascote do colégio: **Kennedito**, um cachorro
antropomórfico de pé, com **boné verde do Colégio Presidente Kennedy (CEPK)**,
**capa/gola verde esvoaçante**, **traje de couro marrom com medalhão dourado**,
**cinto com fivela dourada** e **botas marrons**.

O jogo tem **login**, **menu decorado com abas**, **10 avatares**,
**escolha de personagem**, **histórico de partidas**, **dois modos de jogo**,
um **Kennedito interativo na tela de login/cadastro** e um **banco de dados
SQLite** para guardar as contas e o progresso de cada um.

> **Versão 4.1:** novos personagens (**Tails**, **Luigi**, **Bowser** e
> **Pdhorodecki**) e o **Chuchuty jogável** agora aparece sempre montado na
> motinha elétrica — o chefe da fase secreta continua igual.
>
> **Versão 4.0:** modo **INFINITO** com as 4 fases em loop e **+1% de
> velocidade por volta**, além do modo **ARCADE** com a fase secreta.

## Como jogar
- **É só acessar o link no repositório principal que te redirecionará para o jogo**

### Controles

| Tecla | Ação |
|---|---|
| **ESPAÇO** (ou ↑ / W) | Pular obstáculos |
| **CTRL** (ou ↓ / S) | Abaixar / passar por baixo das barras |
| **ESPAÇO** na tela de derrota | Continuar |
| **MENU** (botão no topo) | Voltar ao menu |

No celular aparecem botões **PULAR** e **ABAIXAR** (ou toque na tela para pular).

## 👤 Conta e menu

- Antes de jogar é preciso **entrar** ou **criar uma conta** (nome + senha).
- As senhas são guardadas com **hash scrypt** — nunca em texto puro.
- A sessão fica em um cookie `HttpOnly` por 30 dias.
- Depois do login aparece o **menu decorado**, com o avatar do jogador, nome,
  vitórias, recorde, modo atual e quatro abas:

  | Aba | O que tem |
  |---|---|
  | **JOGAR** | personagem atual, velocidade, modo, botão de troca de modo e **INICIAR** |
  | **PERSONAGENS** | Kennedito, Sonic, Mario e Chuchuty (bloqueado no começo) |
  | **HISTÓRICO** | estatísticas e as **15 partidas mais recentes** |
  | **PERFIL** | os **10 avatares** e o botão **SAIR DA CONTA** |

### 🎮 Modos de jogo

O botão **TROCAR PARA INFINITO / TROCAR PARA ARCADE** fica na aba **JOGAR**.
O modo escolhido é salvo na conta. **Ao trocar de modo a pontuação atual é
zerada**; recorde, moedas, vidas e personagem são mantidos.

| Modo | Como funciona |
|---|---|
| **ARCADE** | As 4 fases principais + a **fase secreta** escondida no pilar preto. Chegar a 3000 pontos (ou passar pelo pilar) vence a partida. |
| **INFINITO** | Só as 4 fases principais, repetindo para sempre. **Sem fase secreta e sem tela de vitória.** A cada volta completa nas 4 fases (3000 pontos) a corrida fica **1% mais rápida** (cumulativo). |

No modo infinito o HUD mostra `INFINITO V2`, `V3`... (a volta atual) e a
velocidade aparece como `3 +2%`, por exemplo. A pontuação não tem o teto de
3000 e o game over continua registrando a partida no histórico.

### 🐶 Kennedito no login e no cadastro

O Kennedito aparece em pixel art ao lado do título e **interage** com as telas
de entrar/criar conta:

- acena e conversa no balão de fala;
- fica curioso quando você digita o nome;
- **cobre os olhos com as patas quando você digita a senha** (“TÔ DE OLHO
  FECHADO!”);
- fica triste e repete a mensagem quando algo dá errado;
- comemora com confete quando o login ou o cadastro dá certo;
- pode ser clicado (ele dá um pulinho e late).

### 🧑‍🤝‍🧑 Avatares

- São **10 avatares em pixel art**, feitos em SVG (sem imagens externas):
  **5 etnias × 2 gêneros** — branca, negra, parda, asiática e indígena,
  nas versões feminina e masculina.
- O avatar escolhido fica salvo na conta e aparece no topo do menu.

### 🎭 Personagens

| Personagem | Como liberar |
|---|---|
| **Kennedito** | disponível desde o início (personagem principal) |
| **Sonic** | disponível desde o início |
| **Tails** | disponível desde o início |
| **Mario** | disponível desde o início |
| **Luigi** | disponível desde o início |
| **Bowser** | disponível desde o início |
| **Pdhorodecki** | disponível desde o início (o dev do CEPK) |
| **Chuchuty** | **só depois de escapar da fase secreta** |

- A escolha do personagem também fica salva na conta.
- O **Chuchuty jogável** é sempre desenhado **sentado na motinha elétrica**
  (mesmo modelo "Lago Azul" da fase secreta), inclusive nas fases normais e no
  menu. O **chefe** da fase secreta continua com o sprite antigo, a pé.
- O **Chuchuty** mostra “???” e um cadeado até o jogador sobreviver aos
  **22 obstáculos** da fase secreta. Apenas **entrar** na fase secreta (ou
  vencer o jogo sem escapar) **não** desbloqueia o personagem.
- O servidor também valida a regra: tentar selecionar o Chuchuty sem o
  desbloqueio retorna erro **403**.

### 📜 Histórico de partidas

- Cada partida entra no histórico com **data, personagem, fase, modo,
  pontuação, moedas e resultado**:
  - **VITÓRIA** — venceu o modo arcade;
  - **GAME OVER** — perdeu as 3 vidas;
  - **CAPTURADO PELO CHUCHUTY** — colidiu na fase secreta e escolheu
    **VOLTAR AO MENU**.
- **TENTAR DE NOVO** na tela de captura continua a **mesma** partida; ela só é
  registrada quando o jogador volta ao menu ou termina a corrida.
- O histórico guarda as **50 partidas mais recentes** por conta e mostra as
  **15 últimas**, além de estatísticas (partidas, vitórias, recorde e fugas do
  Chuchuty).

## Regras

- O personagem corre **automaticamente para a direita**; o mundo é que se move.
- Cada obstáculo ultrapassado vale **+10 pontos** (moedas douradas valem **+5**).
- A velocidade base é **30% maior** que nas versões antigas, em todas as fases.
- A **velocidade aumenta a cada 500 pontos** (indicada no HUD).
- O **tema do mapa muda a cada 750 pontos**:

  | Pontos | Zona |
  |---|---|
  | 0 | GREEN HILL |
  | 750 | CHEMICAL PLANT |
  | 1500 | SKY ISLAND |
  | 2250 | NIGHT STAR |

- **Arcade:** ao chegar em **3000 pontos** aparece a mensagem de vitória (quem
  dispara é o pilar preto da última fase).
- **Infinito:** ao completar 3000 pontos começa a **volta 2**, com **+1% de
  velocidade**; depois a volta 3, 4 e assim por diante.

## 🚨 Fase Secreta — Colégio Estadual Presidente Kennedy (só no ARCADE)

A **última fase (NIGHT STAR)** tem um obstáculo diferente dos outros: no fim
dela aparece o **PILAR PRETO** (o último pilar do jogo). Ele é o único que
**brilha em verde/roxo** e tem uma placa de aviso no HUD:

> *“ÚLTIMA FASE! O PILAR PRETO ESCONDE ALGO…”*

- **Se você passar por baixo dele** (CTRL/↓): termina a fase e **você vence**.
- **Se você colidir com ele** (ficar em pé ou pular nele): você é
  **teletransportado para a FASE SECRETA** — não perde vida!
- No modo **INFINITO** o pilar preto e a fase secreta **não existem**: as 4
  fases apenas se repetem.

### 🧔 Chuchuty perseguindo

- Ao entrar na fase secreta, o **chuchuty** aparece **atrás do personagem** e
  começa a perseguição.
- **Qualquer colisão com um obstáculo** durante a fuga encerra a corrida: o
  personagem é **capturado** (não perde vida, não renasce).
- Aparece a tela **“CAPTURADO PELO CHUCHUTY!”**, com:
  - **TENTAR DE NOVO** — recomeça a fase secreta;
  - **VOLTAR AO MENU**.
- Para escapar, sobreviva aos **22 obstáculos** da fase secreta. Ao final o
  chuchuty desiste, você recebe **+150 de bônus** e volta para a última fase.
- **Escapar da fase secreta libera o Chuchuty como personagem jogável** na
  conta. Se for capturado antes de terminar os 22 obstáculos, o personagem
  continua bloqueado.

### 🛵 O que tem na fase secreta

| Item | Detalhe |
|---|---|
| Tema | **COLEGIO ESTADUAL PRESIDENTE KENNEDY** (prédio, janelas, bandeira e árvores do pátio) |
| Veículo | O personagem vira **piloto de uma motinha elétrica** (modelo “Lago Azul”) |
| Obstáculos de agachar | **Cigarros gigantes** com contorno preto |
| Outros obstáculos | Cone, pilha de livros, robô zelador, **balde**, **cadeira**, **bola** e **carteira escolar** |
| Perseguidor | **chuchuty** — careca, óculos e barba grande ruiva |
| Recompensa | **+150** de bônus por escapar |

## 🪙 Moedas

- Cada moeda coletada **desaparece na hora** (com uma faísca dourada).
- As moedas **reaparecem** nos mesmos lugares quando o personagem perde uma
  vida ou reinicia, porque o mundo é gerado com semente fixa (`WORLD_SEED`).
- Cada moeda vale **+5 pontos** e conta para a troca por vidas extras.

## ❤️ Vidas e moedas de reserva

- O personagem começa com **3 vidas** (corações no HUD).
- Ao colidir com um obstáculo você **perde 1 vida** e a corrida continua
  (renasce com invencibilidade piscando).
- **A cada 50 moedas coletadas o personagem recupera 1 vida.**
  As 50 moedas usadas **saem do contador**.
- **Com as 3 vidas cheias** as moedas ficam **guardadas na carteira** (o HUD
  mostra `RESERVA` = quantas vidas extras estão guardadas).
- **Ao perder uma vida**, se houver 50 moedas guardadas, elas são consumidas e
  a vida é devolvida automaticamente (aviso “VIDA RECUPERADA!”).
- Ao perder as **3 vidas**, a carteira de moedas é **zerada** (o total
  histórico `earned` continua salvo).
- **Ao reiniciar** depois de um game over ou de uma vitória, a carteira também
  começa **zerada**.

## 💾 Progresso salvo (SQLite + localStorage)

***OBS:*** Infelizmente o Banco de Dados só funciona no render se você assinar o plus, oque significa que a cada deploy o Banco perde seus dados

- O save oficial fica no **banco SQLite** (`data/jogo.db`), por usuário:
  pontos, vidas, moedas, total coletado, recorde, vitórias, rodadas, avatar,
  personagem, **modo de jogo**, se a última partida foi vencida e se o
  Chuchuty foi liberado.
- O navegador mantém uma cópia em `localStorage` (`sonic_cao_save_v1`) como
  espelho local. A chave antiga foi mantida de propósito para **não perder o
  progresso** de quem já jogava.
- O save é enviado ao servidor a cada pontuação/moeda/vida e ao fechar a aba.
- Contas antigas são migradas automaticamente (novas colunas via `ALTER TABLE`),
  sem perder o progresso.
- O desbloqueio do Chuchuty é gravado pelo servidor somente pela rota
  `/api/secret-cleared`, chamada quando o jogador **escapa** da fase secreta.
  O save normal não altera esse desbloqueio.

### Banco de dados

| Tabela | Conteúdo |
|---|---|
| `users` | id, nome único, salt e hash da senha, data de criação |
| `saves` | progresso, avatar, personagem, modo e desbloqueio de cada usuário |
| `runs` | histórico de partidas (máximo de 50 por usuário) |
| `sessions` | tokens de sessão com validade |

### API

| Rota | Método | O que faz |
|---|---|---|
| `/api/register` | POST | cria a conta e já inicia a sessão |
| `/api/login` | POST | entra na conta |
| `/api/logout` | POST | encerra a sessão |
| `/api/me` | GET | devolve usuário e save da sessão |
| `/api/save` | POST | grava o progresso do usuário |
| `/api/mode` | POST | troca entre arcade e infinito (zera a pontuação atual) |
| `/api/profile` | POST | salva o avatar e o personagem escolhidos |
| `/api/secret-cleared` | POST | libera o Chuchuty após escapar da fase secreta |
| `/api/runs` | POST | registra uma partida no histórico |
| `/api/history` | GET | devolve as 15 últimas partidas + estatísticas |

## Obstáculos

- 🔺 **Espinho / engradado / robô (Motobug) / barril / hidrante / caixa alta** → pule por cima.
- 🟡 **Barra baixa** → abaixe com **CTRL** para passar por baixo.
- ⬛ **Pilar preto** (só na última fase do arcade) → portal para a fase secreta.
- 🚬 **Cigarro** (só na fase secreta) → abaixe com **CTRL**; agora tem contorno preto.
- 🪣 **Balde / cadeira / bola / carteira** (só na fase secreta) → pule por cima.
- 🧔 **Chuchuty** (só na fase secreta) → persegue o jogador; um toque em
  qualquer obstáculo = capturado.

## Arquivos

- `index.html` — estrutura, HUD, telas de login, menu com abas e captura.
- `auth.js` — login/cadastro, abas, avatares, personagens, modos, histórico e save.
- `game.js` — física, sprites dos personagens, obstáculos, fases, modos arcade
  e infinito, perseguição, regras de desbloqueio e registro das partidas.
- `kennedito.js` — pet em pixel art que interage com o login e o cadastro.
- `server.js` — servidor HTTP + API + banco SQLite.
- `package.json` — configuração do Node/Render.
- `data/jogo.db` — banco criado automaticamente (fora do Git).

### Parâmetros de teste (URL)

`index.html?debug=1&score=1500&lives=2&coins=55&theme=3&win=1` — força
pontuação, vidas, moedas, tema e/ou tela de vitória.

| Parâmetro | O que faz |
|---|---|
| `mode=infinite` | abre no modo infinito |
| `phase=0..3` | joga direto numa das 4 fases |
| `secret=1` | entra direto na **fase secreta** (de moto) |
| `boss=1` | entra no fim da fase secreta, com o chuchuty perseguindo |
| `over=1` | abre a tela de game over |
| `win=1` | abre a tela de vitória |

> Os parâmetros de teste funcionam depois do login.
