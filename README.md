# Eksamens-opgave

/*
    Jens Christian Joergensen
    jcja17@student.aau.dk
    A410
    Software*/
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    #define MAX_REG 70
    #define MAX_LOEB 790
    
    struct cykkelloeb
    {
        char loebsnavn[MAX_REG];
        char rytter_navn[MAX_REG];
        int rytter_alder;
        char rytter_hold[MAX_REG];
        char nationalitet[MAX_REG];
        char placering[MAX_REG];
        double koeretid;
        int points;
    };
    typedef struct cykkelloeb cykkelloeb;

    /*mine prototyper*/
    void laes_til_struct(const char *file_name, cykkelloeb loeb[MAX_LOEB]);
    void be_rytter_23(cykkelloeb loeb[MAX_LOEB]);
    void dk_ryttere_flere_loeb(cykkelloeb loeb[MAX_LOEB]);
    int cmphold(const void *ip1, const void *ip2);
    void ti_bedste_ryttere(cykkelloeb loeb[MAX_LOEB]);
    void daarligst (cykkelloeb loeb[MAX_LOEB]);
    
    
    /*min main funktion*/
    int main(int argc, char const *argv[])
    {
        /*ligger statestikken ind fra tekst filen over i mit array af structs*/
        cykkelloeb loeb[MAX_LOEB];
        laes_til_struct("cykkelloeb-2017.txt", loeb);


        printf("Velkomen til UCI's statestik omkring forårsklassikere fra disse fire loeb: Paris Roubaix, Amstell Gold Race, La fleche Wallonne og Liege Alle\n");

         int   i;

   printf("\n  argc = %d\n\n", argc);

   for (i = 0; i < argc; ++i){
      printf("   argv[%d] = %s\n", i, argv[i]);
    }
        printf("Vil du se loebsresultaterne fra de belgiske cykelryttere under 23 aar, de danske ryttere som har deltaget i et eller flere af de loeb, de 10 bedste ryttere, hvilken af de fire hold der har flest ryttere med en placering som OTL eller DNF, den bedste nation eller mediantiden af hvert af de foere loeb\n");

        
        return 0;
    }

    /*Skrevet ind fra cykkelstatestikken til min struct*/

    void laes_til_struct(const char *file_name, cykkelloeb loeb[MAX_LOEB]) {
        FILE *fp;
        fp = fopen(file_name, "r");
        for (int i = 0; i < MAX_LOEB; ++i)
        {
            fscanf(fp, "%s %s %d %s %s %s %lf", loeb[i].loebsnavn, loeb[i].rytter_navn, &loeb[i].rytter_alder, loeb[i].rytter_hold, loeb[i].nationalitet, loeb[i].placering, &loeb[i].koeretid);
        }
        fclose(fp);
    }

    /*De belgiske ryttere under 23 aar*/
    void be_rytter_23(cykkelloeb loeb[MAX_LOEB]) {
        int i = 0;

        for (int i = 0; i < MAX_LOEB; ++i)
        {
            if (strcmp(loeb[i].nationalitet, "BEL") && loeb[i].rytter_alder < 23)
             {

             } 
        }
    }

    /*De danske ryttere efter holdnavn*/

    void dk_ryttere_flere_loeb(cykkelloeb loeb[MAX_LOEB]) {

        cykkelloeb dk_loeb[MAX_LOEB];
        int i = 0;
        int j = 0;

        for (int i = 0; i < MAX_LOEB; ++i)
        {
            if (strcmp(loeb[i].nationalitet, "DEN"))
             {

            dk_loeb[j]=loeb[i];
            j++;
             }
        }
        qsort(dk_loeb, 7, sizeof(cykkelloeb), cmphold);
    }

    int cmphold(const void *ip1, const void *ip2){
  cykkelloeb *h1 = (cykkelloeb *) ip1,
         *h2 = (cykkelloeb *) ip2;

    return strcmp(h1->rytter_hold, h2->rytter_hold);
    }
    
    /*Denne finder de 10 ryttere med flest point*/
    void ti_bedste_ryttere(cykkelloeb loeb[MAX_LOEB]) {
    int points = 0;
    for (int i = 0; i < MAX_LOEB; i++)
    {
        if (atoi(loeb[i].placering) == 0 )
        {
            loeb[i].points += 2;
        }
        if (atoi(loeb[i].placering) == 0 && atoi(loeb[i].placering) == 0)
        {
            /*Grunden til denne del er fordi at man skal lave en udregning som hedder (M-P)/17 og min M er loebsnavn og den er delt op i tre fordi at der findes tre forskellige løb*/
            if (strcmp(loeb[i].loebsnavn, "ParisRoubaix"))
            {
                loeb[i].points += ((102 - atoi(loeb[i].placering)) / 17);
            }
            if (strcmp(loeb[i].loebsnavn, "AmstelGoldRace"))
            {
                loeb[i].points += ((127 - atoi(loeb[i].placering)) / 17);
            }

            if (strcmp(loeb[i].loebsnavn, "LaFlecheWallonne"))
            {
                loeb[i].points += ((166 - atoi(loeb[i].placering)) / 17);
            }
            if (strcmp(loeb[i].loebsnavn, "LiegeBastogneLiege"))
            {
                loeb[i].points += ((153 - atoi(loeb[i].placering)) / 17);
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

  /*Det hold der har flest ryttere med OTL eller DNF*/
    void daarligst (cykkelloeb loeb[MAX_LOEB]) {
        int i = 0;
        int daaOTL = 0;
        int daaDNF = 0;
        for (int i = 0; i < MAX_LOEB; ++i)
         {
             if (strcmp(loeb[i].rytter_hold, loeb[i].rytter_hold))
            {
                 if (strcmp(loeb[i].placering, loeb[i].rytter_hold))
            {
                daaOTL++;
            }
            else if (strcmp(loeb[i].placering, loeb[i].rytter_hold))
            {
                daaDNF++;
            }
            }
            
        }
    }
