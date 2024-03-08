## 👋 Bem vindo ao Visage Track Project!

## Funcionamento dos Blobs
Aluno: Jáder Louis de Souza Gonçalves
Projeto: Reconhecimento de expressões faciais em ambientes controlados gerados proceduralmente utilizando técnicas avançadas de Geometria Analítica, Algebra Linear e Calculo Numerico. 
Orientador: Prof Dr. Lucas Marques

![[unir 1.png]]

# Documentação do funcionamento dos 'Blobs'![[WhatsApp Image 2024-02-12 at 16.09.49.jpeg]]

Para entender o comportamento dos Blobs é essencial entender a formula de GLC (Gerador Linear Congruente), que é a base de tudo isso

$$
X_{n+1} = (aX_n + c) \mod m

$$
- Xn+1​ representa o próximo número na sequência,
- a é o multiplicador,
- Xn​ é o número atual ou a semente,
- c é o incremento,
- m é o módulo.

Usando a formula para gerar números aleatórios:
$$
X_{n+1} = (aX_n + c) \mod m

$$
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




[]AZ\x

---






# Visão Lógica:

$$
\begin{align*}
&\text{Dado } estadoSomaOuSub, x, \text{ e } state: \\
&\text{Se } estadoSomaOuSub = 1: \\
&\quad blobInterest = blobInterest + x \\
&\text{Senão se } estadoSomaOuSub = 0: \\
&\quad blobInterest = blobInterest - x \\
& \\
&\text{Dado } state, \text{ aplique as seguintes regras:} \\
&\text{Se } state = 2 \text{ ou } state = 1: \\
&\quad \text{Seja } randomChance = \text{GLC mod } 3 \\
&\quad \text{Se } randomChance = 0: laziness = laziness - 20 \\
&\quad \text{Se } randomChance = 1: blobInterest = blobInterest + 10 \\
&\quad \text{Se } randomChance = 2: \begin{cases} blobInterest = blobInterest - 30 \\ laziness = laziness + 1 \end{cases} \\
&\text{Se } state = 6: \\
&\quad \text{Seja } randomChance = \text{GLC mod } 3 \\
&\quad \text{Se } randomChance = 2: blobInterest = blobInterest + 50 \\
&\text{Se } state = 7 \text{ ou } state = 4: \\
&\quad \text{Seja } randomChance = \text{GLC mod } 3 \\
&\quad \text{Se } randomChance = 0: laziness = laziness + 20 \\
&\quad \text{Se } randomChance = 1: blobInterest = blobInterest - 15 \\
&\quad \text{Se } randomChance = 2: \begin{cases} blobInterest = blobInterest + 30 \\ laziness = laziness + 1 \end{cases} \\
& \\
&\text{Atualização de } blobInterest \text{ com base em } daysCount: \\
&\text{Se } \text{tempo} \mod 30 < 3: \\
&\quad daysCount = daysCount + 1 \\
&\quad \text{Se } daysCount \geq 32: daysSub = 31 \text{ senão } daysSub = daysCount \\
&\quad \text{Seja } chance = \text{GLC mod } 100 \\
&\quad \text{Se } chance \geq laziness: blobInterest = interest - daysSub \\
&\quad \text{Senão}: blobInterest = interest + daysSub \\
&\quad commitment = \text{GLC mod } (90 - 10) + 10 \\
\end{align*}
$$

> [!NOTE] O que está acontecendo ? 
>Inicialmente, o interesse do personagem é ajustado para cima ou para baixo por um valor `x`, dependendo do estado `estadoSomaOuSub`. Se este estado for 1, o interesse aumenta; se for 0, o interesse diminui.

Em seguida, dependendo do estado atual do personagem (`state`), diferentes ações são tomadas:

- Nos estados 2 ou 1, a preguiça pode diminuir, o interesse pode aumentar ou diminuir, e a preguiça pode aumentar ligeiramente, baseado em uma chance aleatória determinada por um gerador linear congruente (GLC).
- No estado 6, há uma chance de o interesse aumentar significativamente se uma condição específica de chance aleatória for atendida.
- Nos estados 7 ou 4, a preguiça pode aumentar, o interesse pode diminuir, ou ambos o interesse aumentar e a preguiça aumentar ligeiramente, também baseado em chances aleatórias.

Além disso, o sistema inclui uma lógica de atualização periódica que ajusta o interesse com base no número de dias passados (`daysCount`). Esta atualização ocorre em intervalos regulares de tempo e pode aumentar ou diminuir o interesse, dependendo do nível atual de preguiça e de um fator de chance aleatória. O comprometimento é também ajustado aleatoriamente dentro de um intervalo específico durante essas atualizações.

---
# Formula Relativa da Variação ao Longo do Tempo
$$
\begin{align*}
& blobInterest \mathrel{+}= (estadoSomaOuSub = 1) \cdot x - (estadoSomaOuSub = 0) \cdot x, \\ \\
& rc = (aX_n + c) \mod m \mod 3, \\ 
& laziness \mathrel{-}= 20 \cdot (\text{{state}} \in \{1, 2\} \land rc = 0) + 20 \cdot ((\text{{state}} = 7 \lor \text{{state}} = 4) \land rc = 0) + (\text{{state}} = 2 \land rc = 2), \\ \\
& blobInterest \mathrel{+}= 10 \cdot ((\text{{state}} \in \{1, 2\} \lor \text{{state}} = 6) \land rc = 1) - 30 \cdot (\text{{state}} \in \{1, 2\} \land rc = 2) + 50 \cdot (\text{{state}} = 6 \land rc = 2) - 15 \cdot ((\text{{state}} = 7 \lor \text{{state}} = 4) \land rc = 1) + 30 \cdot ((\text{{state}} = 7 \lor \text{{state}} = 4) \land rc = 2), \\ \\
& daysCount \mathrel{+}= 1 \cdot (\text{{tempo}} \mod 30 < 3), \\
& daysSub = \min(\text{{daysCount}}, 31), \\
& chance = (aX_{n+1} + c) \mod m \mod 100, \\
& blobInterest \mathrel{-}= daysSub \cdot (chance \geq laziness) + daysSub \cdot (chance < laziness), \\
& commitment = ((aX_{n+2} + c) \mod m \mod 80) + 10.
\end{align*}

$$
