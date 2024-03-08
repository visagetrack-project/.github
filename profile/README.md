# 👋 Bem-vindo ao Visage Track Project!

O Visage Track Project é dedicado ao Reconhecimento de expressões faciais em ambientes controlados, gerados proceduralmente utilizando técnicas avançadas de Geometria Analítica, Álgebra Linear e Cálculo Numérico.

**Aluno:** Jáder Louis de Souza Gonçalves  
**Projeto:** Reconhecimento de expressões faciais em ambientes controlados gerados proceduralmente.  
**Orientador:** Prof. Dr. Lucas Marques

![Perfil do Usuário](https://github.com/visagetrack-project/.github/blob/687927c5ac1b96ad2807e33c2aa88ed99c9fa6e5/profile/unir%201.png)

## Documentação do funcionamento dos 'Blobs'

Para entender o comportamento dos Blobs, é essencial compreender a fórmula do Gerador Linear Congruente (GLC), que é a base de tudo isso.

![Documento Blob](https://github.com/visagetrack-project/.github/blob/687927c5ac1b96ad2807e33c2aa88ed99c9fa6e5/profile/WhatsApp%20Image%202024-02-12%20at%2016.09.49.jpeg)

A fórmula GLC é usada para gerar números aleatórios:

$$
X_{n+1} = (aX_n + c) \mod m
$$

Definimos as características iniciais para cada variável \(x\) (laziness, commitment, interest) dentro dos limites \(min = 0\) e \(max = 100\), usando a fórmula para gerar valores aleatórios dentro desses limites.

As taxas de alteração em "laziness" e o impacto do "commitment" e "interest" sobre essas variáveis são calculadas com base nas fórmulas fornecidas, ajustando dinamicamente o comportamento e o estado dos "Blobs" ao longo do tempo.

## Visão Lógica:

As interações e transições de estado dos "Blobs" são definidas por uma série de condições lógicas que levam em consideração os valores de "laziness", "commitment", "interest", além do número de dias passados. Essas condições determinam as mudanças no interesse e na preguiça dos "Blobs", modelando seu comportamento ao longo do tempo.

---

Para mais detalhes sobre a implementação e os cálculos específicos, consulte os documentos de código-fonte e as anotações no repositório.

