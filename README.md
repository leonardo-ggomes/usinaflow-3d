# 🏭 Usina Flow — Simulador Industrial 3D

> Planta isométrica interativa de uma usina de açúcar e etanol construída em Three.js com equipamentos industriais procedurais — caldeiras, colunas de destilação, dornas de fermentação, esteiras e mais.

![Three.js](https://img.shields.io/badge/Three.js-r128-black?style=flat-square&logo=threedotjs)
![WebGL](https://img.shields.io/badge/WebGL-2.0-red?style=flat-square)
![HTML5](https://img.shields.io/badge/HTML5-single--file-E34F26?style=flat-square&logo=html5&logoColor=white)
![Zero deps](https://img.shields.io/badge/deps-zero--local-00c896?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-cc44ff?style=flat-square)

---

## 🎯 Sobre o Projeto

**Usina Flow** é uma visualização educativa 3D de uma usina sucroalcooleira completa, renderizada em tempo real com Three.js. Cada equipamento é construído proceduralmente com geometrias reais — `LatheGeometry` para vasos de pressão, `TubeGeometry` para tubulações e escadas helicoidais, `ExtrudeGeometry` para estruturas metálicas — com materiais PBR (metalness/roughness) que simulam aço escovado, concreto, borracha e cobre oxidado.

A câmera é totalmente livre: orbita, pan, zoom e toque mobile. O tour guiado percorre as 6 etapas da cadeia de produção com telemetria em tempo real.

---

## ✨ Funcionalidades

### 🔩 Equipamentos Procedurais

Cada equipamento é uma função dedicada composta de 15–40 peças geométricas independentes:

| Equipamento | Técnica geométrica | Destaque |
|---|---|---|
| **Caldeira de Alta Pressão** | `LatheGeometry` + `CylinderGeometry` | Vaso de pressão com dished ends, fornalha, superaquecedores, válvulas de segurança, escada helicoidal, passarela, bomba de alimentação |
| **Colunas de Destilação** | `LatheGeometry` + `TorusGeometry` | Casco com flanges de bandejas, plataformas perfuradas, escada vertical, refervedor, tambor de refluxo, instrumentação |
| **Dornas de Fermentação** | `LatheGeometry` + `TubeGeometry` | Casco cônico real, agitador 3 andares de pás, motor no topo, escada helicoidal, bocais, suporte em 4 patas |
| **Evaporadores Multi-efeito** | `LatheGeometry` | Calandria + corpo de vapor separados, saída vapor, vidro de nível, anel identificador, suporte |
| **Centrífugas** | `LatheGeometry` | Carcaça + cesto perfurado interno, tampa, motor, calha de descarga, saída de mel |
| **Tanques de Armazenamento** | `LatheGeometry` + `TubeGeometry` | Teto flutuante com pontoons reais, escada helicoidal, fundação de concreto, válvula respiradora |
| **Esteiras Transportadoras** | `CylinderGeometry` + `BoxGeometry` | Rolos idler a cada 0.6m, rolos de retorno, polias de acionamento, estrutura I-beam, motor lateral |
| **Caminhões Canavieiros** | `BoxGeometry` + `CylinderGeometry` | Chassis, cabine, vidros translúcidos, 4 eixos com rodas + cubo, carga de cana procedural aleatória |
| **Clarificador Contínuo** | `CylinderGeometry` | Corpo cilíndrico + cone de fundo, eixo central, braços rastelo, cobertura |
| **Turbina a Vapor** | `CylinderGeometry` | Carcaça, rotor, 7 discos de palhetas, acoplamento ao gerador |

### 🎨 Materiais PBR

Todos os materiais usam `MeshStandardMaterial` com metalness/roughness calibrados:

| Material | Metalness | Roughness | Uso |
|---|---|---|---|
| Aço escovado | 0.85 | 0.30 | Equipamentos gerais |
| Aço novo | 0.90 | 0.20 | Rolos, eixos, palhetas |
| Aço enferrujado | 0.50 | 0.70 | Tanques de vinhaça |
| Concreto | 0.00 | 0.95 | Fundações, skirts, chaminés |
| Borracha | 0.00 | 0.95 | Correias, rodas |
| Cobre oxidado | 0.60 | 0.50 | Superaquecedores, instrumentação |
| Vidro | 0.00 | 0.05 | Vidros de nível, cabine |
| Fogo emissivo | — | — | Fornalha com flickering animado |

### ⚡ Cadeia de Produção em 6 Etapas

| Etapa | Equipamentos principais | Produto |
|---|---|---|
| **1. Recepção & Moagem** | Caminhões, balança, pórtico, mesa alimentadora, 5 ternos de moenda | Caldo misto + bagaço |
| **2. Tratamento do Caldo** | Aquecedores, clarificador contínuo, filtro rotativo, tanque de cal | Caldo clarificado |
| **3. Fermentação** | 6 dornas Ø5.2m × 6m, lavador CO₂, cuba de vinho, centrífuga de levedura | Vinho 8–12% etanol |
| **4. Destilação** | 5 colunas (A/A1/B/B1/D), tambores de refluxo, tanques AEHC/AEAC, tanque vinhaça | Etanol 96°GL / 99,7°GL |
| **5. Cozimento & Açúcar** | 5 evaporadores, 3 tachos a vácuo, 4 centrífugas, secador rotativo, silo | Açúcar VHP 99,7° pol |
| **6. Cogeração** | 2 caldeiras 67 kgf/cm², turbina 30 MW, gerador, pilha de bagaço | 250 kWh/t cana |

### 🌫️ Efeitos Visuais

- **Sistema de partículas de vapor** — chaminés (200 partículas), topos das colunas (60), respiros das dornas (30). Velocidade, dispersão e reset automático procedural.
- **Flickering da fornalha** — material emissivo com `emissiveIntensity` aleatório a cada 5 frames
- **Rede de tubulações** — vapor (vermelho, elevado), suco (verde), condensado (azul), vinhaça (marrom) com suportes a cada 4m e esferas de joelho
- **Névoa exponencial** — `FogExp2` para profundidade de campo

### 📷 Câmera Livre

| Ação | Mouse | Touch |
|---|---|---|
| Orbitar | Botão esquerdo + arrastar | 1 dedo |
| Pan (mover) | Botão direito + arrastar / Shift + arrastar | 2 dedos arrastar |
| Zoom | Scroll | Pinch |
| Reset | Botão `⊹ CÂMERA` | — |

---

## 🚀 Como Usar

### Requisitos

Nenhuma dependência local. Three.js r128 carregado via CDN (Cloudflare).

| Browser | Versão mínima |
|---|---|
| Chrome / Edge | 80+ |
| Firefox | 75+ |
| Safari | 14+ |
| Mobile Chrome / Safari | 2021+ |

### Executar

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/usina-flow.git
cd usina-flow

# Abrir direto (funciona via file://)
open index.html

# Ou servidor local
npx serve .
python3 -m http.server 8080
```

> Funciona com `file://` diretamente — sem build step, sem npm, sem bundler.

---

## 🗂️ Estrutura

```
usina-flow/
└── index.html    # Aplicação completa — single file HTML + Three.js + CSS
```

Projeto **single-file** intencional: todo o CSS, JS, geometria e lógica em um único arquivo HTML autocontido. Three.js carregado via CDN.

---

## 🏗️ Arquitetura Técnica

### Stack

- **Three.js r128** — renderização WebGL, materiais PBR, sombras PCFSoft
- **OrbitControls inline** — implementação própria sem `three/examples/jsm` para compatibilidade `file://`
- **WebGL 2.0** — `logarithmicDepthBuffer` para precisão em cenas grandes
- **ACES Filmic Tone Mapping** — `ACESFilmicToneMapping` + `toneMappingExposure 1.1`
- **Shadow Maps** — `PCFSoftShadowMap` 2048×2048, `DirectionalLight` + `shadow.camera` calibrada

### Funções de Equipamento

Cada equipamento é uma função pura que retorna um `THREE.Group`:

```
buildTruck(px, pz, ry)           → caminhão com cana procedural
buildConveyor(len, width, tilt)  → esteira com rolos, correia, motor
buildMillRoller(px, py, pz)      → terno de moenda com 3 rolos e engrenagem
buildDorna(px, pz, r, h)         → dorna com LatheGeometry + agitador + escada
buildDistColumn(px, pz, r, h)    → coluna de destilação completa
buildBoiler(px, pz)              → caldeira com vaso, fornalha, acessórios
buildEvaporator(px, pz, effect)  → evaporador multi-efeito
buildCentrifuge(px, pz)          → centrífuga com cesto interno
buildTank(px, pz, r, h, ...)     → tanque com teto flutuante
```

### Sistema de Câmera

Câmera esférica com interpolação suave (`lerp 0.08` por frame):

```javascript
// Coordenadas esféricas → cartesianas
x = tx + radius * sin(phi) * sin(theta)
y = ty + radius * cos(phi)
z = tz + radius * sin(phi) * cos(theta)
```

Cada etapa define um preset de câmera `{theta, phi, radius, tx, ty, tz}` para o tour guiado.

### Sistema de Partículas

Partículas de vapor implementadas com `BufferGeometry` + `PointsMaterial` — sem sprites externos. Reset automático quando `life <= 0`, com perturbação lateral aleatória a cada frame.

---

## 📚 Conceitos de Engenharia Abordados

- **Ciclo Rankine** — conversão bagaço → vapor → energia elétrica
- **Processo Melle-Boinot** — fermentação contínua com recirculação de levedura
- **Destilação extrativa** — separação por diferença de pressão de vapor (5 colunas)
- **Evaporação de múltiplo-efeito** — reaproveitamento de vapor entre efeitos
- **Cristalização a vácuo** — nucleação e crescimento de cristais de sacarose
- **Balanço de vapor** — 67 kgf entrada, 2.5 kgf escape para processo, excedente para condensação
- **Fertirrigação** — vinhaça como reposição de K, Ca, Mg no canavial
- **Cogeração de energia** — usina autossuficiente + venda de excedente (250 kWh/t cana)

---

## 🤝 Contribuindo

```bash
git checkout -b feat/novo-equipamento
git commit -m "feat: adiciona centrífuga de levedura"
git push origin feat/novo-equipamento
```

### Ideias para expansão

- [ ] Modelos `.glb` externos para substituir geometria procedural nos equipamentos principais
- [ ] Fluxo de material animado ao longo das tubulações (partículas na rede de pipes)
- [ ] Painel de controle DCS — clique num equipamento abre modal com dados de processo
- [ ] Modo falha — simular parada de equipamento e propagação na cadeia
- [ ] Separação dia/noite com luzes de operação noturna
- [ ] Diagrama P&ID sobreposto (toggle)
- [ ] Modo comparativo — configuração safra × entressafra

---

## 📄 Licença

MIT — veja [`LICENSE`](LICENSE) para detalhes.

---

<div align="center">

Construído com Three.js r128 · WebGL 2.0 · geometria 100% procedural · single file

</div>
