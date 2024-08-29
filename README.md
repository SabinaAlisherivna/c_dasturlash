
#include <stdio.h>
#include "yordamchiKutubxona.h"

#define MAX_SWEETS 5
#define MAX_DRINKS 5

// Mahsulot tuzilmasi
struct Mahsulot {
    char nom[30];
    float narx;
};

// Mahsulotni tanlash va umumiy narxni hisoblash
float mahsulotSotibOl(struct Mahsulot shirinliklar[], int nSweets, struct Mahsulot ichimliklar[], int nDrinks) {
    int tanlov, miqdor;
    float umumiyNarx = 0;
    int jamiMahsulotlar = nSweets + nDrinks;

    printf("\nSotib olish uchun mahsulotni tanlang (0 - tugatish):\n");
    while (1) {
        printf("Tanlovingiz: ");
        scanf("%d", &tanlov);

        if (tanlov == 0) {
            break;
        }

        if (tanlov < 1 || tanlov > jamiMahsulotlar) {
            printf("Noto'g'ri tanlov. Qaytadan urinib ko'ring.\n");
            continue;
        }

        printf("Nechta kerak: ");
        scanf("%d", &miqdor);

        if (tanlov <= nSweets) {
            umumiyNarx += shirinliklar[tanlov - 1].narx * miqdor;
            printf("%s: %d dona\n", shirinliklar[tanlov - 1].nom, miqdor);
        } else {
            umumiyNarx += ichimliklar[tanlov - nSweets - 1].narx * miqdor;
            printf("%s: %d dona\n", ichimliklar[tanlov - nSweets - 1].nom, miqdor);
        }
    }

    return umumiyNarx;
}


// Foydalanuvchidan yana sotib olishni xohlash-xohlamasligini so'rash
int yanaXaridQilish() {
    int tanlov;
    printf("\n Yana nimadir sotib olmoqchimisiz? (1 - Ha, 0 - Yo'q): ");
    scanf("%d", &tanlov);
    return tanlov;
}

int main() {
    struct Mahsulot shirinliklar[MAX_SWEETS] = {
        {"Perojni", 20000.0},
        {"Zefir", 5000.0},
        {"Kekslar", 8000.0},
        {"Mochi", 7000.0},
        {"Rangli quymoqlar", 10000.0}
    };

    struct Mahsulot ichimliklar[MAX_DRINKS] = {
        {"Moxito", 8000.0},
        {"Pepsi", 9000.0},
        {"Kola", 9000.0},
        {"Limonad", 10000.0},
        {"Kofe", 12000.0}
    };

    printf("***Assalomu alekum*** \n Antiqa shirinliklar do'konimizga xush kelibsiz\n\n");

    int yanaXarid = 1;

    while (yanaXarid) {
        // Shirinliklar va ichimliklar menyusini alohida chop etamiz
        shirinliklarMenyusiniChopEt(shirinliklar, MAX_SWEETS);
        ichimliklarMenyusiniChopEt(ichimliklar, MAX_DRINKS);

        float umumiyNarx = mahsulotSotibOl(shirinliklar, MAX_SWEETS, ichimliklar, MAX_DRINKS);

        printf("\n Sizning umumiy xaridingiz: %.2f so'm\n", umumiyNarx);

        tolovTuriniTanlash();

        printf("\nXaridingiz uchun rahmat!\n");

        yanaXarid = yanaXaridQilish();
    }

    printf("\n Bizni tanlaganingiz uchun rahmat! Yaqin orada sizni yana kutamiz.\n");

    return 0;
}

