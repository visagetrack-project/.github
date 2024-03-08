# 👋 Bem-vindo ao Visage Track Project!

O Visage Track Project é dedicado ao Reconhecimento de expressões faciais em ambientes controlados, gerados proceduralmente utilizando técnicas avançadas de Geometria Analítica, Álgebra Linear e Cálculo Numérico.

**Alunos:** Jáder Louis, Wyllgner França, Nicolas Sales
**Projeto:** Reconhecimento de expressões faciais em ambientes controlados gerados proceduralmente.  
**Orientador:** Prof. Dr. Lucas Marques

![Perfil do Usuário](https://github.com/visagetrack-project/.github/blob/687927c5ac1b96ad2807e33c2aa88ed99c9fa6e5/profile/unir%201.png)
# Funcionamento do Projeto

O projeto opera da seguinte forma: escolhemos utilizar um ambiente Unity controlado, uma vez que não podemos usar imagens de pessoas reais para treinamento. Assim, criamos seres denominados "blobs" nesse ambiente controlado na Unity, utilizando a fórmula blob para definir suas personalidades e traços característicos, os quais são gerados aleatoriamente. Isso introduz um grande fator de imprevisibilidade ao projeto.

O projeto é dividido em várias partes: Web, Comunicação, IA (Inteligência Artificial) e o Ambiente de Controle.

## WEB

Os repositórios web estão disponíveis em:

- **Repositório Web:** [vt-web](https://github.com/visagetrack-project/vt-web.git) - Ambiente web desenvolvido em Flutter, incluindo sistema de autenticação e banco de dados Firebase.
- **API Primária:** [vt-api](https://github.com/visagetrack-project/vt-api.git) - Escrita em Go, essa API faz a comunicação direta com a web e é essencial para o funcionamento do projeto.

## Comunicação

### API Primária

A API primária, cujo repositório pode ser encontrado em [vt-api](https://github.com/visagetrack-project/vt-api.git), gerencia as requisições do servidor web e recebe dados processados da API secundária.

### API Secundária

Localizada em [vt-model](https://github.com/visagetrack-project/vt-model), esta API é responsável pelo processamento das imagens. O arquivo [api_communication.py](https://github.com/visagetrack-project/vt-model/blob/main/api_communication.py) é utilizado para capturar, transformar os dados e enviá-los para a API primária. Importante destacar que `main.py` não chama esse arquivo diretamente; em vez disso, uma API terciária gerencia essa comunicação automaticamente, além de gerar gráficos.

### API Terciária

Esta API, escrita em C# e hospedada em um repositório privado, é responsável por gerar as imagens e enviá-las para serem processadas pela IA. Ela também recebe as imagens processadas de volta da API secundária. Além disso, essa API é responsável por criar um novo ambiente Unity a cada requisição através do endpoint `/createNewAmbient{params1}/{params2}/{params3}`, preparando o cenário para as operações das demais APIs.

## IA

### Sobre o MobileNet

O `MobileNet` é uma arquitetura de Rede Neural Convolucional (CNN) projetada para aplicações móveis e embarcadas, destacando-se por sua eficiência computacional e baixo consumo de recursos. Essa família de modelos é amplamente reconhecida por seu desempenho excepcional em tarefas de visão computacional, como classificação e detecção de objetos, oferecendo um equilíbrio ideal entre precisão e velocidade para dispositivos com capacidade de processamento limitada.

### Processo Geral Incorporando o MobileNet

1. **Conversão do Modelo para TFLite**: O modelo pré-treinado `MobileNet` é inicialmente convertido para TensorFlow Lite (TFLite), adaptando-o para um uso mais eficiente em dispositivos móveis e de baixa potência.

2. **Classificação de Imagens**: Utilizando o modelo convertido, o script aplica o `MobileNet` para classificar objetos em imagens. A função `tflite_classify_image` processa a imagem de entrada, realiza a inferência com o modelo TFLite e identifica as principais classes dos objetos presentes na imagem.

3. **Geração de Arquivos XML e CSV**: As informações da classificação são salvas em arquivos XML, que detalham as classificações por imagem, e em um arquivo CSV, que agrega as classes identificadas e suas respectivas probabilidades.

### Funcionamento do MobileNet no Script

- **Inferência Eficiente**: O script analisa a imagem recebida, utilizando o `MobileNet` para classificar os objetos detectados. Através de uma estrutura otimizada e técnicas de processamento avançadas, o modelo oferece rapidez e precisão na classificação, mesmo em dispositivos com recursos limitados.

- **Pós-processamento e Análise**: Após a classificação, um pós-processamento é realizado para extrair as classes dos objetos e suas probabilidades. Essas informações são empregadas para atualizar as imagens com etiquetas indicativas, gerar arquivos XML para cada classificação e compilar um resumo no arquivo CSV.

- **Comunicação**: Em seguida, é recebido um vetor contendo 10 estados, com valores de 0 a 8, que representam as medições realizadas pela IA. Esses dados são processados em [analysis.py](https://github.com/visagetrack-project/vt-model/blob/main/analysis.py) e enviados para a API primária.

### Aplicação do MobileNet

Os resultados da classificação podem ser visualizados na seguinte imagem: ![blobs.jpeg](https://github.com/visagetrack-project/.github/blob/a0ad6ef25561d476ca5be027df0538b9d013afd8/profile/blobs.jpeg)


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

