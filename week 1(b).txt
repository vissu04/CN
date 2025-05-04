#include <stdio.h>
#include <string.h>

int main() {
    char b[100];
    int i = 0;


    printf("\nEnter the string:\n");
    fgets(b, sizeof(b), stdin);


    size_t len = strlen(b);
    if (b[len - 1] == '\n') {
        b[len - 1] = '\0';
    }


    printf("\nAfter stuffing:\n");
    printf("DLESTX");


    while (i < strlen(b)) {

        if ((b[i] == 'd' || b[i] == 'D') &&
            (b[i+1] == 'i' || b[i+1] == 'I') &&
            (b[i+2] == 'e' || b[i+2] == 'E')) {

            printf("DLE");
            i += 3;
        } else {
            printf("%c", b[i]);
            i++;
        }
    }

    printf("DLEETX\n");
}
