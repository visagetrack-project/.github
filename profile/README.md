# 👋 Bem-vindo ao Visage Track Project!

O Visage Track Project é dedicado ao Reconhecimento de expressões faciais em ambientes controlados, gerados proceduralmente utilizando técnicas avançadas de Geometria Analítica, Álgebra Linear e Cálculo Numérico.

**Aluno:** Jáder Louis de Souza Gonçalves  
**Projeto:** Reconhecimento de expressões faciais em ambientes controlados gerados proceduralmente.  
**Orientador:** Prof. Dr. Lucas Marques

![Perfil do Usuário](https://github.com/visagetrack-project/.github/blob/687927c5ac1b96ad2807e33c2aa88ed99c9fa6e5/profile/unir%201.png)

## Documentação do funcionamento dos 'Blobs'

Para entender o comportamento dos Blobs, é essencial compreender a fórmula do Gerador Linear Congruente (GLC), que é a base de tudo isso.

![Documento Blob](https://github.com/visagetrack-project/.github/blob/687927c5ac1b96ad2807e33c2aa88ed99c9fa6e5/profile/WhatsApp%20Image%202024-02-12%20at%2016.09.49.jpeg)

Para entender o comportamento dos Blobs é essencial entender a formula de GLC (Gerador Linear Congruente), que é a base de tudo isso
Usando a formula para gerar números aleatórios:

$$
X_{n+1} = (aX_n + c) \mod m
$$

- Xn+1​ representa o próximo número na sequência,
- a é o multiplicador,
- Xn​ é o número atual ou a semente,
- c é o incremento,
- m é o módulo.


Logo definimos as características iniciais:

$$
\begin{align*}
\text{Sejam } & min = 0 \text{ e } max = 100. \\
\text{Para cada variável } & x \in \{ \text{laziness}, \text{commitment}, \text{interest} \}, \\
& x = X_{n+1} = (aX_n + c) \mod m(min,max).
\end{align*}
$$

$$
\begin{align*}
\text{taxaPraDiminuirEmLaziness} &= \frac{\text{commitment}}{2} + \left( \frac{\text{laziness}}{32 - \text{daysCount}} \right) \\\\
\text{commitment} &> 45 =  \\
x &= \left( \frac{5}{1 + \text{laziness}} \right) \cdot \left( \text{interest} \cdot \frac{\text{taxaPraDiminuirEmLaziness}}{100} \right),  \text{estado} = 1 \\ \\
\text{commitment} &< 45 =  \\
x &= \left( \frac{\text{laziness}}{10} \right) \cdot \left( \text{interest} \cdot \frac{\text{taxaPraDiminuirEmLaziness}}{1000} \right), \text{estado} = 0 \\\\
& x > 10,  x = 10 \\
& x < -10,  x = -10 
\end{align*}
$$

> [!tips] O que exatamente está acontecendo aqui? 
> Aqui estamos filtrando exatamente a reação a cada tipo de comportamento com base no quanto ele esta disposto a continuar, sendo X o interesse, alem de definir a formula para diminuir ou aumentar a preguiça ao longo do tempo.

## Visão Lógica:

As interações e transições de estado dos "Blobs" são definidas por uma série de condições lógicas que levam em consideração os valores de "laziness", "commitment", "interest", além do número de dias passados. Essas condições determinam as mudanças no interesse e na preguiça dos "Blobs", modelando seu comportamento ao longo do tempo.

---

Para mais detalhes sobre a implementação e os cálculos específicos, consulte os documentos de código-fonte e as anotações no repositório.

