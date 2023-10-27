#include <stdio.h>
#include <time.h>

const char MDPniveau1[] = "niveau1";        //mot de passe de chaque niveau
const char MDPniveau2[] = "niveau2";
const char MDPniveau3[] = "niveau3";
const char MDPniveau4[] = "niveau4";

//Fonction pour vérifier si les mots de passe correspondent
int verifierMotDePasse(const char* entreeUtilisateur, const char* motDePasse)
{
    int i = 0;
    while (motDePasse[i] != '\0' && entreeUtilisateur[i] != '\0')
    {
        if (motDePasse[i] != entreeUtilisateur[i])
        {
            return 0;       //Les mots de passe ne correspondent pas
        }
        i++;
    }
    if (motDePasse[i] == '\0' && entreeUtilisateur[i] == '\0') {
        return 1;           // Les mots de passe correspondent
    }
    return 0;               //Les longueurs des mots de passe sont différentes
}

int choixniveau()
{
    char motDePasse[50];
    int x=0;
    printf("Veuillez entrer la clef pour un niveau : ");
    scanf("%s", motDePasse);

    //selection du niveau
    if (verifierMotDePasse(motDePasse,MDPniveau1))
    {
        x=1;
    } else if (verifierMotDePasse(motDePasse,MDPniveau2))
    {
        x=2;
    } else if (verifierMotDePasse(motDePasse,MDPniveau3))
    {
        x=3;
    } else if (verifierMotDePasse(motDePasse,MDPniveau4))
    {
        x=4;
    } else printf("Aucun niveau associe a ce mot de passe.\n");
    return x;
}

int choixJeu(int y)
{
    if (y==0)
    y = choixniveau();
    clock_t debut_timer, fin_timer;
    double temps_ecoule;

    switch (y)                  //selection du niveau de jeu
    {
        case 1:
            debut_timer = clock();
            printf("Jeu 1\n");
            fin_timer = clock();
            temps_ecoule = (double)(fin_timer - debut_timer)/CLOCKS_PER_SEC;
            printf("Le temps ecoule est de %f secondes.\n",temps_ecoule);
            break;
        case 2:
            debut_timer = clock();
            printf("Jeu 2\n");
            fin_timer = clock();
            temps_ecoule = (double)(fin_timer - debut_timer)/CLOCKS_PER_SEC;
            printf("Le temps ecoule est de %f secondes.\n",temps_ecoule);
            break;
        case 3:
            printf("Jeu 3\n");
            break;
        case 4:
            printf("Jeu 4\n");
            break;
    }
}

int main()
{
    int a;
    printf(" 1/ Regle du jeu\n 2/ Lancer du nouveau jeu a partir du niveau 1\n 3/ Charger une partie\n 4/ Lancer un niveau via son mot de passe\n 5/ Scores\n 6/ Quitter\n");
    scanf("%d",&a);

    while ((a>6)||(a<1))                   //blindage de la valeur du menu entre 1 et 6
    {
        printf("Selectionner un menu entre 1 et 6 !\n");    //Dans le cas où n est inférieur à 1 ou supérieur à 6
        scanf("%d",&a);
    }

    switch (a)
    {
        case 1:
            printf("Les regles du jeu sont : \n");
            //essayer d'ouvrir les règles avec un fichier
            break;
        case 2:
            choixJeu(1);
            break;
        case 3:
            printf("Selectionner une partie chargee");
            break;
        case 4:
            choixJeu(0);
            break;
        case 5:
            printf("Votre score est de 500 points.");
            break;
        default:
            printf("Fin du jeu La revanche de Snoopy");
            break;
    }
    return 0;
}
