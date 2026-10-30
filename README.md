# Assistente-Desportivo
Assistente de postura para treino no browser: deteta a pose com MediaPipe e mostra ângulos do joelho e do tronco em tempo real. Protótipo de agachamento. O vídeo não sai do dispositivo.

> **Aviso:** projeto de demonstração. O feedback é orientativo e não substitui um treinador nem aconselhamento médico. Os limiares são valores de exemplo e ainda não foram validados por um profissional.

## O que faz

- Abre a câmara e desenha o esqueleto sobre o vídeo (MediaPipe Pose Landmarker).
- Calcula e mostra o **ângulo do joelho** (anca, joelho, tornozelo) e a **inclinação do tronco** em relação à vertical.
- Regista a **profundidade máxima** atingida (menor ângulo do joelho).
- Pinta o tronco de verde ou vermelho consoante um limite configurável.
- O processamento é feito no dispositivo: o vídeo não é enviado para nenhum servidor.

## O que ainda não faz

- Contagem de repetições e máquina de estados.
- Avaliação da profundidade no ponto mais baixo de cada repetição.
- Feedback sonoro.
- Peso morto e boxe.
- Histórico de sessões.

## Como usar

A câmara só funciona em HTTPS ou em `localhost`.

```bash
git clone <url-do-repositorio>
cd <pasta>
python3 -m http.server 8000
```

Abre `http://localhost:8000/assistente-agachamento.html`. Para testar no telemóvel, aloja o ficheiro com HTTPS (por exemplo, GitHub Pages).

Na primeira utilização é preciso internet, porque o modelo é descarregado de uma CDN.

## Como posicionar

Telemóvel de lado, a 2 ou 3 metros, com o corpo inteiro visível da cabeça aos pés.

## Como funciona

```
Câmara → Pose Landmarker (33 pontos) → ângulos (com suavização) → regras → canvas
```

- Escolhe automaticamente o lado do corpo mais visível.
- Os ângulos são suavizados com uma média móvel exponencial.

## Limitações

- O MediaPipe não tem pontos ao longo da coluna. Mede-se a **inclinação do tronco** (a partir de ombros e ancas), não a **curvatura da coluna**: uma lombar arredondada pode passar despercebida.
- A precisão diminui com roupa larga, pouca luz ou membros sobrepostos.
- Uma única câmara dá uma pose aproximada em 2D.

## Tecnologias

HTML, CSS e JavaScript (módulos ES), [MediaPipe Tasks Vision](https://developers.google.com/mediapipe), Canvas API.

## Roadmap

1. Contagem de repetições e avaliação no ponto mais baixo.
2. Feedback sonoro (Web Audio API).
3. Peso morto.
4. Boxe (posturas estáticas, como a guarda).
5. Testes com vários utilizadores e revisão dos limiares por um treinador ou fisioterapeuta.
6. Histórico de sessões (opcional).

## Licença

[Escolher licença, por exemplo MIT]

## Autores

[Nomes dos autores]
