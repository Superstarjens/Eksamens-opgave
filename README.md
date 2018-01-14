# Eksamens-opgave

    /*Jens Christian Joergensen
    jcja17@student.aau.dk
    A410
    Software*/
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    #define MAX_REG 70
    #define MAX_LOEB 790

    /*Alle de gange jeg bruger loeb[i].noget så er det for at slippe for at skulle skrive hver enkelte parameter fra min struct ind som noget sepperat og så referere til det når man laver det i hver funktion så for at slippe for det bruger jeg loeb[i].noget som bare referere til den bestemte ting i min struct og det er en *Kristian Otte har vist og forklaret mig*/
    /*Mit program kan desværre ikke køre, da det har et problem i min leas_til_struct og hverken jeg eller dem der har kigget på det kan finde problemet desværre for den vil godt kompile, men ikke køre*/

    
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
    char be_rytter_23(cykkelloeb loeb[MAX_LOEB]);
    char dk_ryttere_flere_loeb(cykkelloeb loeb[MAX_LOEB]);
    int cmphold(const void *ip1, const void *ip2);
    char ti_bedste_ryttere(cykkelloeb loeb[MAX_LOEB]);
    char daarligst (cykkelloeb loeb[MAX_LOEB]);
    
    
    /*min main funktion*/
    int main(int argc, char const *argv[])
    {
        int choice;
        /*ligger statestikken ind fra tekst filen over i mit array af structs*/
        cykkelloeb loeb[MAX_LOEB];
        laes_til_struct("cykkelloeb_2017.txt", loeb);


        printf("Velkomen til UCI's statestik omkring foraarsklassikere fra disse fire loeb: Paris Roubaix, Amstell Gold Race, La fleche Wallonne og Liege Alle\n");

         int   i;

   printf("\n  argc = %d\n\n", argc);

   for (i = 0; i < argc; ++i)
    {
      printf("   argv[%d] = %s\n", i, argv[i]);
    }
        printf("Vil du se a: loebsresultaterne fra de belgiske cykelryttere under 23 aar, b: de danske ryttere som har deltaget i et eller flere af de loeb, c: de 10 bedste ryttere, d: hvilken af holdene har flest ryttere med en placering som OTL eller DNF i hvert af de fire loeb\n");

        scanf("%d", &choice);

        for (int i = 0; i < MAX_LOEB; ++i)
        {
            
        switch(choice)
        {
            case 1: {
                char a = be_rytter_23(&loeb[MAX_LOEB]);
                printf("De belgiske cykelryttere under 23 aar er %c\n", a);
                break;
            }
            case 2: {
                char b = dk_ryttere_flere_loeb(&loeb[MAX_LOEB]);
                printf("De danske ryttere der har vaaret med i et eller flere loeb %c\n", b);
                break;
            }
            case 3: {
                char c = ti_bedste_ryttere(&loeb [MAX_LOEB]);
                printf("De 10 ryttere der har fået flest points er: %c\n", c);
                break;
            }
            case 4: {
                char d = daarligst(&loeb[MAX_LOEB]);
                printf("Det hold der har flest ryttere som enten er OTL eller DNF er %c\n", d);
                break;
            }
            default:
            {
                printf("Cyklen døde: :( \n");
            }
        }
        }
        
        return 0;
        }

    /*Skrevet ind fra cykkelstatestikken til min struct. Den er taget og lavet om på fra Kurt Noermark's sidste gang hvor han lavede et program som skrev de danske regioner ud fra et seperat dokument*/

    void laes_til_struct(const char *file_name, cykkelloeb loeb[MAX_LOEB])
    {
        FILE *fp;
        fp = fopen("cykkelloeb_2017.txt", "r+");
        for (int i = 0; i < MAX_LOEB; ++i)
        {
            fscanf(fp, "%s %s %d %s %s %s %lf", loeb[i].loebsnavn, loeb[i].rytter_navn, &loeb[i].rytter_alder, loeb[i].rytter_hold, loeb[i].nationalitet, loeb[i].placering, &loeb[i].koeretid);
        }
        fclose(fp);
    }

    /*De belgiske ryttere under 23 aar*/
    char be_rytter_23(cykkelloeb loeb[MAX_LOEB])
    {
        int i = 0;

        for (int i = 0; i < MAX_LOEB; ++i)
        {
            if (strcmp(loeb[i].nationalitet, "BEL") && loeb[i].rytter_alder < 23)
             {
                printf("%s %s %d %s %s %s %lf", loeb[i].loebsnavn, loeb[i].rytter_navn, loeb[i].rytter_alder, loeb[i].rytter_hold, loeb[i].nationalitet, loeb[i].placering, loeb[i].koeretid);
             }
        }
        return printf("%s %s %d %s %s %s %lf", loeb[i].loebsnavn, loeb[i].rytter_navn, loeb[i].rytter_alder, loeb[i].rytter_hold, loeb[i].nationalitet, loeb[i].placering, loeb[i].koeretid);
    }

    /*De danske ryttere efter holdnavn*/

    char dk_ryttere_flere_loeb(cykkelloeb loeb[MAX_LOEB])
    {

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

        return dk_loeb;
    }

    int cmphold(const void *ip1, const void *ip2)
    {
    cykkelloeb *h1 = (cykkelloeb *) ip1,
               *h2 = (cykkelloeb *) ip2;

    return strcmp(h1->rytter_hold, h2->rytter_hold);
    }
    
    /*Denne finder de 10 ryttere med flest point*/
    char ti_bedste_ryttere(cykkelloeb loeb[MAX_LOEB])
    {
    int points = 0;
    for (int i = 0; i < MAX_LOEB; i++)
    {
        /*Jeppe Arnfelt har hjulpet og forklaret mig hvad atoi er og gør så jeg kunne bruge den*/
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
    return points;
    }
    /*Der staar i opgaven at man skal sortere rytterne efter point, men jeg kan  ikke se det kan være muligt da mit points system er en integer*/

    /*Det hold der har flest ryttere med OTL eller DNF, den kan dog ikke ligge dem sammen med rytter_hold på grund af manglende fejl et sted*/
    char daarligst (cykkelloeb loeb[MAX_LOEB])
    {
        int i = 0;
        int daaOTL = 0;
        int daaDNF = 0;
        for (int i = 0; i < MAX_LOEB; ++i)
         {
             if (strcmp(loeb[i].rytter_hold, loeb[i].rytter_hold))
            {
                 if (strcmp(loeb[i].placering, "OTL"))
            {
                daaOTL++;
            }
            else if (strcmp(loeb[i].placering, "DNF"))
            {
                daaDNF++;
            }
            }
        }
        return daaDNF;
    }
