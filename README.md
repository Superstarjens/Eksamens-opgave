# Eksamens-opgve


    /*
    Jens Christian Joergensen
    jcja17@student.aau.dk
    A410
    Software*/
    #include <stdio.h>
    #include <stdlib.h>
    #define MAX 300
    
    FILE *fp
    fp = fopen("cykkelloeb-2017", "r");
    struct cykkelloeb
    {
        char loebsnavn[MAX];
        char rytter_navn[MAX];
        int rytter_alder[MAX];
        char rytter_hold[MAX];
        char nationalitet[MAX];
        int placering[MAX];
        double koeretid[MAX];
    };
    fclose(fp);    

    typedef struct cykkelloeb cykkelloeb;

    void choices (int * choice);
    void dk_ryttere_flere_loeb(char * nationalitet, char * rytter_hold, char * rytter_navn);
    int cmphold();
    int main(int argc, char const *argv[])
    {
        printf("Velkomen til UCI's statestik omkring forårsklassikere fra disse fire loeb: Paris Roubaix, Amstell Gold Race, La fleche Wallonne og Liege Alle\n");

         int   i;

   printf("\n  argc = %d\n\n", argc);

   for (i = 0; i < argc; ++i)
      printf("   argv[%d] = %s\n", i, argv[i]);

        printf("Vil du se loebsresultaterne fra de belgiske cykelryttere under 23 aar, de danske ryttere som har deltaget i et eller flere af de loeb,
                de 10 bedste ryttere, hvilken af de fire hold der har flest ryttere med en placering som OTL eller DNF, den bedste nation eller mediantiden af hvert af de foere loeb\n");
        scanf("%d", &choice);


        return 0;
    }

    void choices (int * choice) {
        switch (choice){
            case 1: {
                int br_25 = be_rytter_23(*rytter_alder, *nationalitet);
                printf("De belgiske ryttere har fordelt sig sådan: %i\n", br_25);
                break;
            }

            case 2: {
                char dk_ryt = dk_ryttere_flere_loeb(*rytter_navn, *rytter_hold, *nationalitet);
                printf("De danske ryttere som har deltaget i et eller flere looes er: %c\n", dk_ryt);
                break;
            }

            case 3: {
                char ti_bedste = ti_bedste_ryttere(*rytter_navn, *placering);
                printf("De 10 ryttere der har flest points er: %c\n", 10_bedste);
                break;
            }

            case 4: {
                char daeligste = OTL_DNF(*rytter_hohld, *placering);
                printf("Det hold der har flest ryttere som koerte over OTL er: %c\n", daeligste);
                printf("Det hold der har flest ryttere som koerte over DNF er: %c\n", daeligste);
                break;
            }

            case 5: {
                char bedste_nation = nation(*nationalitet, *placering);
                printf("Ud af ale nationerne der har været med har denne gjort det bedst %c\n", bedste_nation);
                break;
            }

            case 6: {
                char mediantid_fra_loeb = mediantid(*loebsnavn, *koeretid);
                printf("Ud fra de fire cykkelloeb er deres mediantid: %c\n", mediantid_fra_loeb);
                break;
            }
            default: {
                printf("Findes ikke\n");
            }
        }
    }

    /*De belgiske ryttere under 23 aar*/
    void be_rytter_23(int * rytter_alder, char * nationalitet) {

    while (nationalitet == BEL && rytter_alder =< 23) {
        printf("%c %i\n", nationalitet, rytter_alder);
    }

    /*return while (nationalitet == BEL && rytter_alder =< 23);*/
    }

    /*De danske ryttere efter holdnavn*/

    void dk_ryttere_flere_loeb(char * nationalitet, char * rytter_hold, char * rytter_navn) {
        while (nationalitet == DEN) {
            qsort(rytter_hold, 3, sizeof(int), cmphold)
            printf("%c %c %c\n", rytter_navn, rytter_hold, nationalitet);
        }
    }

    int cmphold() {
        strcmp(hold1, hold2);
    }

    void ti_bedste_ryttere(char * rytter_navn, int *placering) {
        
    }
