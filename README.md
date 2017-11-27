# Eksamens-opgave

    /*
    Jens Christian Joergensen
    jcja17@student.aau.dk
    A410
    Software*/
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    #define MAX_name 75;
    
    struct cykkelloeb
    {
        char loebsnavn[MAX];
        char rytter_navn[MAX];
        int rytter_alder;
        char rytter_hold[MAX];
        char nationalitet[MAX];
        char placering[MAX];
        double koeretid;
        int points;
    };
    typedef struct cykkelloeb cykkelloeb;

    void be_rytter_23(cykkelloeb loeb[790]);
    void dk_ryttere_flere_loeb(cykkelloeb loeb[790]);
    int cmphold();
    void ti_bedste_ryttere(cykkelloeb loeb[790]);
    int main(int argc, char const *argv[])
    {
        cykkelloeb loeb[790];
        printf("Velkomen til UCI's statestik omkring forårsklassikere fra disse fire loeb: Paris Roubaix, Amstell Gold Race, La fleche Wallonne og Liege Alle\n");

         int   i, choice;

   printf("\n  argc = %d\n\n", argc);

   for (i = 0; i < argc; ++i)
      printf("   argv[%d] = %s\n", i, argv[i]);

        printf("Vil du se loebsresultaterne fra de belgiske cykelryttere under 23 aar, de danske ryttere som har deltaget i et eller flere af de loeb, de 10 bedste ryttere, hvilken af de fire hold der har flest ryttere med en placering som OTL eller DNF, den bedste nation eller mediantiden af hvert af de foere loeb\n");

        
        return 0;
    }

    /*Skrevet ind fra cykkelstatestikken til min struct*/
    /*De belgiske ryttere under 23 aar*/
    void be_rytter_23(cykkelloeb loeb[790]) {
        int i = 0;

    while (strcmp(loeb[i].nationalitet, "BEL") == 0 && loeb[i].rytter_alder < 23) {
        i++;

        printf("%s %i\n", loeb[i].nationalitet, loeb[i].rytter_alder);
    }

    }

    /*De danske ryttere efter holdnavn*/

    void dk_ryttere_flere_loeb(cykkelloeb loeb[790]) {

        cykkelloeb dk_loeb[790];
        int i = 0;
        int j = 0;

        while (strcmp(loeb[i].nationalitet, "DEN")) {

            j++;

            dk_loeb[j]=loeb[i];
            
            i++;
        }
        qsort(rytter_hold, 3, sizeof(int), cmphold);
            printf("%s %s %s\n", rytter_navn, rytter_hold, nationalitet);
    }

    int cmphold() {
        strcmp(hold1, hold2);
    }

    void ti_bedste_ryttere(cykkelloeb loeb[790]) {
        int points 0;
        for (int i = 0; i < 790; i++)
        {
            if (loeb[i].placering != "DNF" )
            {
                loeb[i].points += 2;
            }
            if (loeb[i].placering != "DNF" && loeb[i].placering != "OTL")
            {
                /*Grunden til denne del er fordi at man skal lave en udregning som hedder (M-P)/17 og min M er loebsnavn og den er delt op i tre fordi at der findes tre forskellige løb*/
                if (strcmp(loeb[i].loebsnavn, "ParisRoubaix"))
                {
                    loeb[i].points += ((102 - loeb[i].placering) / 17);
                }
                if (strcmp(loeb[i].loebsnavn, "AmstelGoldRace"))
                {
                    loeb[i].points += ((127 - loeb[i].placering) / 17);
                }
            }
            if (strcmp(loeb[i].placering, "1"))
            {
                loeb[i].points += 8;
            }
            if (strcmp(loeb[i].placering, "2"))
            {
                loeb[i].points += 5;
            }
            if (strcmp(loeb[i].placering, "3"))
            {
                loeb[i].points += 3;
            }

        }
        
    }
