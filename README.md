# Jeu_De_La_Vie

# Diagramme de classe

```mermaid
classDiagram

    class Jeu{
        -grille : Grille
        -regle : Regle
        -mode : Mode
        -nb_iteration : int
        
        Jeu()
        Jeu(grille, regle, mode, nb_iteration)
        Jeu(const *j Jeu)
        ~Jeu()

        getGrille() grille
        getNbinteration() int

        setGrille(grille Grille) void
        setNbiteration(int nb_interation) void

        +début()
        +milieu() # Il contient la boucle while 
        +fin()

        affiche()=0 
    }

    class Grille{
        -nb_lignes : int
        -nb_colonnes : int 
        -matrice : list[Cellule]

        Grille()
        Grille(nb_lignes, nb_colonnes, matrice liste)
        Grille(const *g Grille)
        ~Grille()

        +getNblignes() int
        +getNbcolonnes() int
        +getMatrice() list
        +getCellule(int ligne; int colonne) Cellule
        
        +setNblignes(int ligne) void
        +setNbcolonnes(int colonne) void
        +setMatrice(list matrice) void
        +setCellule(Cellule cellule) void

        +compterVoisinsVivants(int ligne, int colonne) int
        +calculerSuivante(Regle regle) Grille
        +Comparaison(Grille autre) bool
        +grilleVide() bool
    }

    class Cellule{
        #position_x : int
        #position_y : int
        etat : Etat*

        Cellule()
        Cellule(position_x, position_y)
        ~Cellule()

        +getPositionX() int
        +getPositionY() int
        +getEtat() Etat

        +setPositionX(int X) void
        +setPositionY(int Y) void 
        +setEtat(Etat* etat) void

        +estVivante() bool
    }

    class Vivant{
        +etat_vivant() bool
    }

    class Mort{
        +etat_mort() bool
    }

    class Etat{
        +estVivant() bool*
    }

    class Fichier{
        -chemin : string
        -contenu : string

        Fichier()
        Fichier(string chemin)
        ~Fichier()

        +getChemin() string
        +setChemin(string _chemin) void

        -Lire() string
        -Ecrire(string Text) void
    }

    class Mode{
        <<Abstract>>
        +afficher(Grille grille, int iteration) void*
    }

    class Console{
        -string dossierSortie
        +afficher(Grille grille, int iteration) void
    }

    class Interface{
        -int delaiMs
        +afficher(Grille grille, int iteration) void
        +setDelai(int delaiMs) void
    }

    class Regle{
        <<Abstract>>
        +calculerEtat(Cellule cellule, int nbVoisins) Etat*
    }

    class Conway{
        +calculerEtat(Cellule cellule, int nbVoisins) Etat*
    }


Jeu *<|--Grille
Jeu-->Mode
Jeu-->Regle
Mode<|--Console
Mode<|--Interface
Grille<|--Cellule
Fichier ..> Grille
Console ..> Fichier
Cellule-->Etat
Etat<|--Vivant
Etat<|--Mort
Regle<|--Conway
Grille "1" *-- "n x m" Cellule
```