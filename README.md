# Atividade-49

#include <stdio.h>
#include <stdlib.h>
#include <math.h>

// Função para calcular a distância euclidiana entre dois vetores
double euclidean_distance(const double *vec1, const double *vec2, int size) {
    double sum = 0.0;
    for (int i = 0; i < size; i++) {
        double diff = vec1[i] - vec2[i];
        sum += diff * diff;
    }
    return sqrt(sum);
}

// Função para reconhecer um padrão dado um conjunto de padrões conhecidos e um vetor de entrada
void recognize_pattern(const double **known_patterns, int num_patterns, const double *input_vector, int size, double *result_pattern) {
    double min_distance = INFINITY; // Inicializar para um valor grande
    int best_match_index = -1;

    for (int i = 0; i < num_patterns; i++) {
        double distance = euclidean_distance(known_patterns[i], input_vector, size);
        if (distance < min_distance) {
            min_distance = distance;
            best_match_index = i;
        }
    }

    // Copiar o melhor padrão de correspondência para result_pattern
    for (int i = 0; i < size; i++) {
        result_pattern[i] = known_patterns[best_match_index][i];
    }
}

int main() {
    int num_patterns, size;

    // Leitura do número de padrões e tamanho dos vetores
    printf("Digite o numero de padroes: ");
    scanf("%d", &num_patterns);
    printf("Digite o tamanho dos vetores: ");
    scanf("%d", &size);

    // Alocação dinâmica de memória para padrões e vetor de entrada
    double *known_patterns = (double *)malloc(num_patterns * sizeof(double *));
    for (int i = 0; i < num_patterns; i++) {
        known_patterns[i] = (double *)malloc(size * sizeof(double));
    }

    double *input_vector = (double *)malloc(size * sizeof(double));
    double *result_pattern = (double *)malloc(size * sizeof(double));

    // Leitura dos padrões conhecidos
    printf("Digite os padroes conhecidos:\n");
    for (int i = 0; i < num_patterns; i++) {
        printf("Padrao %d: ", i + 1);
        for (int j = 0; j < size; j++) {
            scanf("%lf", &known_patterns[i][j]);
        }
    }

    // Leitura do vetor de entrada
    printf("Digite o vetor de entrada: ");
    for (int i = 0; i < size; i++) {
        scanf("%lf", &input_vector[i]);
    }

    // Reconhecimento do padrão
    recognize_pattern((const double **)known_patterns, num_patterns, input_vector, size, result_pattern);

    // Impressão do padrão reconhecido
    printf("Padrao reconhecido: ");
    for (int i = 0; i < size; i++) {
        printf("%f ", result_pattern[i]);
    }
    printf("\n");

    // Liberação de memória
    for (int i = 0; i < num_patterns; i++) {
        free(known_patterns[i]);
    }
    free(known_patterns);
    free(input_vector);
    free(result_pattern);

    return 0;
}
