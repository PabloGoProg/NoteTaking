Las redes neuronales recurrentes, a diferencia de las redes neuronales artificiales, relacionan el pasado inmediato con el presente.

1. $h_t = f(h_{t-1}, X_t)$ definición del estado actual
2. $h_t = tanh(W_{hh}h_{t-1}+W_{xh}X_t)$ Paso por la función de activación.
3. $Y_t =$

Ante entradas de gran tamaño o tamaños muy pequeños, se presentan problemas de _desvanecimiento o explosión de gradiente_.
***
## LSTM
1. Compuerta del olvido: $f_t = \alpha(W_f*[h_{t-1}, x_t] + b_f)$ relación del instante pasado con la entrada actual

	Se incluye una relación con la información relevante de momentos pasados $C_t = f_t+C_{t-1}+t_i*C_t$.
1. 
