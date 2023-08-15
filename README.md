#include <stdio.h>
#include <stdlib.h>

typedef struct {
    float altura;
    float largura;
    float profundidade;
} REGISTRO;

int main() {
    REGISTRO *registros = NULL;
    int opcao, posicao;
    int tamanho = 0;

    do {
        puts("1 - Inserir registro");
        puts("2 - Alterar registro");
        puts("3 - Excluir registro");
        puts("4 - Mostrar registros");
        puts("5 - Sair");
        scanf("%i", &opcao);

        switch (opcao) {
            case 1:
            case 2:
                puts("Informe uma posicao");
                scanf("%i", &posicao);

                if (posicao < 0 || posicao >= tamanho) {
                    printf("Posicao invalida.\n");
                    break;
                }

                if (opcao == 1) {
                    printf("Informe a altura: ");
                    scanf("%f", &registros[posicao].altura);
                    printf("Informe a largura: ");
                    scanf("%f", &registros[posicao].largura);
                    printf("Informe a profundidade: ");
                    scanf("%f", &registros[posicao].profundidade);
                } else if (opcao == 2) {
                    printf("Informe a nova altura: ");
                    scanf("%f", &registros[posicao].altura);
                    printf("Informe a nova largura: ");
                    scanf("%f", &registros[posicao].largura);
                    printf("Informe a nova profundidade: ");
                    scanf("%f", &registros[posicao].profundidade);
                }
                break;

            case 3:
                puts("Informe uma posicao");
                scanf("%i", &posicao);

                if (posicao < 0 || posicao >= tamanho) {
                    printf("Posicao invalida.\n");
                    break;
                }

                registros[posicao].altura = 0;
                registros[posicao].largura = 0;
                registros[posicao].profundidade = 0;
                break;

            case 4:
                for (int i = 0; i < tamanho; i++) {
                    printf("Registro %d:\n", i);
                    printf("Altura: %.2f\n", registros[i].altura);
                    printf("Largura: %.2f\n", registros[i].largura);
                    printf("Profundidade: %.2f\n", registros[i].profundidade);
                }
                break;
                
            case 5:
                // Libera a memória alocada antes de sair
                free(registros);
                break;

            default:
                break;
        }

        if (opcao == 1) {
            tamanho++;
            registros = realloc(registros, tamanho * sizeof(REGISTRO));
            if (registros == NULL) {
                printf("Erro ao alocar memoria.\n");
                return 1;
            }
        }

    } while (opcao != 5);
}
