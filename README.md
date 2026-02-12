# Trabalho de Computação Gráfica: Reflexo e Transparência

Este projeto implementa uma cena 3D interativa utilizando **WebGL 2.0** e **GLSL**, focada na simulação de superfícies reflexivas e translúcidas (como vidro ou espelho) sem o uso de *Cube Maps* ou texturas pré-renderizadas.

## Objetivo
Desenvolver um efeito de reflexo e transparência em um plano. O *shader* simula um material translúcido com reflexo dinâmico, comportando-se como um vidro escuro ou espelho semitransparente, utilizando renderização em múltiplos passos (*Multipass Rendering*).

## Controles e Instruções

Abaixo estão listados os controles para interagir com a cena.

### `reflexoTransparencia.html`
Cena principal onde é possível mover um dos cubos para verificar a atualização do reflexo em tempo real.

| Tecla / Ação | Função |
| :--- | :--- |
| **Setas (↑ ↓ ← →)** | **Mover o Cubo** pelo cenário (X e Z) |
| **W / S** | Mover Câmera para Frente / Trás |
| **A / D** | Mover Câmera para Esquerda / Direita |
| **Q / E** | Mover Câmera Verticalmente (Descer / Subir) |
| **Mouse** | Olhar ao redor (Clique na tela para travar o cursor) |
| **Slider (Interface)** | Ajustar nível de transparência do vidro (0% a 100%) |

---
## Implementação Técnica

O projeto foi desenvolvido atendendo rigorosamente aos seguintes requisitos:

* **Reflexo Dinâmico via Framebuffer:** O reflexo é gerado em tempo real renderizando a cena a partir do ponto de vista virtual do espelho para uma textura, sem o uso de *Cube Maps*.
* **Clipping Plane no Shader:** Implementação de um plano de corte no *Fragment Shader* (utilizando `discard`) para garantir que objetos posicionados atrás do espelho não sejam renderizados na textura de reflexo. Isso elimina a necessidade de selecionar objetos via `if` no JavaScript.
* **Shader Customizado (Fresnel):** Cálculo de iluminação Phong combinado com o efeito **Fresnel**, onde a intensidade do reflexo e a transparência variam dinamicamente conforme o ângulo de visão da câmera em relação ao vidro.
* **Transparência Controlável:** Uso de *uniforms* para alterar o canal alpha do vidro em tempo real através da interface.
* **Texturização Completa:** Todos os objetos, incluindo a superfície do vidro (que possui uma textura de "sujeira/imperfeição"), são texturizados.
