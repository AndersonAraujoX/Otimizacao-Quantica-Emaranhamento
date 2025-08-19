# Otimização de Emaranhamento Quântico com Algoritmos Variacionais

Este projeto demonstra a otimização dos parâmetros de um circuito quântico para gerar um estado emaranhado específico, o estado de Bell. A otimização é realizada usando um algoritmo de gradiente descendente estocástico (SGD) com a regra de *parameter-shift* para o cálculo de gradientes, implementado com a biblioteca PennyLane.

## Visão Geral

O objetivo deste notebook é encontrar os parâmetros ideais $(\alpha_1, \alpha_2, \alpha_3)$ para um circuito quântico parametrizado, de modo que o estado de saída do circuito seja o mais próximo possível de um estado de Bell $\left( \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle) \right)$.

Este tipo de otimização é um exemplo de um Algoritmo Quântico Variacional (VQA), que é fundamental em muitas aplicações da computação quântica de curto prazo (NISQ), como a simulação de sistemas quânticos e a otimização de problemas complexos.

## Contexto Teórico

A metodologia utilizada neste notebook tem paralelos com técnicas avançadas em pesquisa quântica, como as discutidas no artigo **"Variational quantum-assisted eigensolver for detecting quantum chaos"** da Nature. Embora o objetivo aqui seja mais simples (gerar um estado de Bell), a abordagem fundamental de usar um circuito parametrizado e um otimizador clássico para minimizar uma função de custo é a mesma.

No artigo, algoritmos variacionais são usados para encontrar os autoestados de sistemas quânticos e estudar propriedades complexas como o caos quântico. A capacidade de preparar eficientemente estados emaranhados específicos, como demonstrado aqui, é um passo crucial para a implementação de tais algoritmos avançados.

-   **Artigo de Referência:** *Variational quantum-assisted eigensolver for detecting quantum chaos*. Nature 13, 54 (2022). [https://www.nature.com/articles/s41534-022-00556-w.pdf](https://www.nature.com/articles/s41534-022-00556-w.pdf)

## Implementação

O código no notebook realiza os seguintes passos:

1.  **Definição do Circuito:** Um circuito quântico de 2 qubits é definido com portas de rotação `RY` e `RZ` parametrizadas e uma porta `CNOT` para gerar emaranhamento.
2.  **Funções de Custo:** Duas funções de custo (`loss` e `loss2`) são implementadas para medir a "distância" ou "sobreposição" entre o estado gerado pelo circuito e o estado de Bell alvo. A otimização busca minimizar o valor dessas funções.
3.  **Otimização:** O algoritmo de gradiente descendente estocástico (SGD) é usado para atualizar iterativamente os parâmetros do circuito. Os gradientes são calculados de forma analítica na plataforma quântica usando a regra de *parameter-shift*.
4.  **Resultados:** O processo de otimização é executado por 15 épocas, e o valor da função de custo é plotado em cada época, mostrando uma convergência para o valor mínimo. Ao final, os parâmetros otimizados são usados para gerar o estado final, e sua matriz de densidade é visualizada, confirmando a alta fidelidade com o estado de Bell.

### Bibliotecas Utilizadas
* **PennyLane:** Para a criação e diferenciação de circuitos quânticos.
* **QuTiP:** Para a manipulação de objetos quânticos, como matrizes de densidade e estados quânticos.
* **NumPy:** Para computação numérica.
* **Matplotlib/Seaborn:** Para a visualização dos resultados.

## Como Executar

1.  **Instale as dependências:**
    ```bash
    pip install pennylane qutip matplotlib seaborn
    ```
2.  **Execute o Notebook:** Abra e execute o arquivo `Otimização_de_emaranhamento.ipynb` em um ambiente Jupyter.

## Resultados

O notebook demonstra que, para ambas as funções de custo, o algoritmo de otimização converge com sucesso, reduzindo o valor da perda a cada época.

![Loss vs Epochs para a primeira função de custo](https://i.imgur.com/k6lP0W3.png)
*Gráfico da função de custo vs. épocas para a primeira implementação.*

![Loss vs Epochs para a segunda função de custo](https://i.imgur.com/G20c2bS.png)
*Gráfico da função de custo vs. épocas para a segunda implementação.*

A matriz de densidade do estado final, gerada com os parâmetros otimizados, aproxima-se com alta fidelidade da matriz de densidade de um estado de Bell puro:

$$
\rho_{Bell} = 
\begin{pmatrix} 
0.5 & 0 & 0 & 0.5 \\ 
0 & 0 & 0 & 0 \\ 
0 & 0 & 0 & 0 \\ 
0.5 & 0 & 0 & 0.5 
\end{pmatrix}
$$

![Matriz de Densidade Final](https://i.imgur.com/w8YdD9W.png)
*Visualização da matriz de densidade do estado gerado após a otimização, mostrando uma forte semelhança com o estado de Bell.*
