# Trabalho de Computação Gráfica: Reflexo e Transparência

Este projeto implementa uma cena 3D interativa utilizando **WebGL 2.0** e **GLSL**, focada na simulação de superfícies reflexivas e translúcidas (como vidro ou espelho) sem o uso de *Cube Maps* ou texturas pré-renderizadas.

## 🎯 Objetivo
Desenvolver um efeito de reflexo e transparência em um plano. O *shader* simula um material translúcido com reflexo dinâmico, comportando-se como um vidro escuro ou espelho semitransparente.

## 🛠 Requisitos Técnicos Implementados

### 1. Shader Customizado
* Implementação própria dos shaders (`vertex` e `fragment`).
* Cálculo de **Reflexão (Fresnel)**: A intensidade do reflexo e da transparência varia com base no ângulo de visão da câmera em relação à normal da superfície.
* Não foram utilizadas texturas prontas para o cálculo do reflexo (tudo é calculado em tempo real).

### 2. Reflexo e Transparência Dinâmicos
* **Renderização Multi-pass com Stencil Buffer**: O reflexo é gerado renderizando a cena invertida (escalada em Z = -1) apenas onde o espelho está visível.
*
* O uso do *Stencil Buffer* garante que o reflexo fique contido apenas na área do espelho.

### 3. Transparência Controlada
* A opacidade da superfície reflexiva é ajustável em tempo real por meio de uma variável `uniform`, controlada via interface (slider).

### 4. Textura Padrão
* Todos os objetos da cena, inclusive a superfície de vidro, possuem mapeamento de textura (UV mapping).

### 5. Clipping Plane
* Utilização de um plano de corte (*Clipping Plane*) no shader para evitar que objetos situados "atrás" do espelho sejam renderizados incorretamente no reflexo.
* A seleção não é feita via `if` na CPU, mas sim matematicamente no Shader.

### 6. Câmera Flyby
* Implementação de uma câmera livre que permite movimentação e rotação pelo cenário.

---

## 🎮 Controles e Instruções

Abaixo estão listados os controles para os dois cenários disponíveis no projeto.

### 📄 1. `trabalho.html` (Cena Principal)
Esta é a cena que atende aos requisitos oficiais da entrega, contendo objetos estáticos e o espelho com física de luz (Fresnel).

| Tecla / Ação | Função |
| :--- | :--- |
| **W / S** | Mover Câmera para Frente / Trás |
| **A / D** | Mover Câmera para Esquerda / Direita |
| **Q / E** | Girar Câmera (Yaw - Eixo Y) |
| **Mouse** | Olhar ao redor (Pitch e Yaw) |
| **Clique** | Travar o mouse na tela (Pointer Lock) |
| **Slider (Interface)** | Ajustar a transparência/opacidade do vidro (0% a 100%) |

> **Nota:** O efeito *Fresnel* fará com que o vidro pareça mais opaco quando visto de ângulos rasos, independente do valor do slider.

### 📄 2. `testeMovimentandoCubo.html` (Teste de Física/Movimento)
Cena utilizada para testes, onde é possível mover um dos cubos para verificar a atualização do reflexo em tempo real.

| Tecla / Ação | Função |
| :--- | :--- |
| **Setas (↑ ↓ ← →)** | **Mover o Cubo** pelo cenário (X e Z) |
| **W / S** | Mover Câmera para Frente / Trás |
| **A / D** | Mover Câmera para Esquerda / Direita |
| **Q / E** | Girar Câmera |
| **Mouse** | Olhar ao redor |
| **Slider** | Ajustar transparência do espelho |

---