CRC:
#include <stdio.h>

int main() {
    int data[10], gen[5], temp[15], crc[5];
    int i, j, dataBits, genBits;

    // Input data
    printf("Enter number of data bits: ");
    scanf("%d", &dataBits);
    printf("Enter data bits: ");
    for(i = 0; i < dataBits; i++)
        scanf("%d", &data[i]);

    // Input generator
    printf("Enter number of generator bits: ");
    scanf("%d", &genBits);
    printf("Enter generator bits: ");
    for(i = 0; i < genBits; i++)
        scanf("%d", &gen[i]);

    // Copy data to temp and append zeros
    for(i = 0; i < dataBits; i++)
        temp[i] = data[i];
    for(i = dataBits; i < dataBits + genBits - 1; i++)
        temp[i] = 0;

    // Division
    for(i = 0; i < dataBits; i++) {
        if(temp[i] == 1) {
            for(j = 0; j < genBits; j++)
                temp[i + j] = temp[i + j] ^ gen[j];
        }
    }

    // Remainder is CRC
    for(i = 0; i < genBits - 1; i++)
        crc[i] = temp[dataBits + i];

    // Display
    printf("CRC bits: ");
    for(i = 0; i < genBits - 1; i++)
        printf("%d", crc[i]);

    printf("\nTransmitted frame: ");
    for(i = 0; i < dataBits; i++)
        printf("%d", data[i]);
    for(i = 0; i < genBits - 1; i++)
        printf("%d", crc[i]);

    return 0;
}
output:::
Enter number of data bits: 6
Enter data bits: 1 0 0 1 0 0
Enter number of generator bits: 4
Enter generator bits: 1 1 0 1
CRC bits: 001
Transmitted frame: 100100001
