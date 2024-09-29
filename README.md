# Hundir-la-flota
Primer jueguito hecho en terminal de Java el año pasado.

/* Fer una primera versió del joc dels vaixells modificat de forma que els 20 vaixells (valor constant) només ocupin una posició cadascun en la matriu de 10x10 elements (valors constants) que representarà el "camp de batalla"
a) Inicialment la matriu haurà d'estar inicialitzada a valors 'neutres' per representar un camp buit
b) El programa assignarà posicions als vaixells de forma aleatòria
c) A partir d'aquest moment, el programa entrarà en un bucle que demanarà unes coordenades a l'usuari. Depenent de si en aquesta posició hi ha un vaixell o no, donarà la resposta adequada a l'usuari, i en qualsevol dels dos casos 
marcarà la posició: amb un valor 0 si ha encertat en un vaixell, o un valor 1 si ha tocat aigua (o una codificació semblant). A continuació mostrarà per pantalla la situació del camp de batalla, amb totes les posicions 
on hagi disparat l'usuari, i mostrant si hi havia un vaixell o un tret a l'aigua. Naturalment, la matriu amb els vaixells original no s'ha de mostar a l'usuari, sinó que treballarem amb una matriu auxiliar per emmagatzemar els 
trets i els vaixells enfonsats.
d) El joc acabarà quan l'usuari ho decideixi o quan hagi enfonsat tots els vaixells. En aquest últim cas, el programa treurà un missatge de felicitació cap a l'usuari. */

    import java.util.Scanner;
    public class SamosAguileraNaiara_6_8 {
        public static void main (String [] args) {
            Scanner input = new Scanner (System.in);
            final int NUM_VAIXELLS = 20; // Els vaixells (nombre) són una constant.
            final int MIDA = 10;
            int [][] posicio; // Anomeno la matriu de les posicions dels vaixells.
            char [][] auxiliar = new char [MIDA][MIDA]; // dEFINEIXO LA MATRIU AUXILIAR.
            int posicioAleatoriaX, posicioAleatoriaY, vaixell, X, Y, vaixellsEnfonsat, movimentFet;

            posicio = new int [MIDA][MIDA];
    
            for (int i = 0; i < MIDA; i++) { // a) Inicialment, la meva matriu tindrà tots valor zero, i quan li introdueixi un vaixell, serà 1.
                for (int j = 0; j < MIDA; j++) {
                    posicio [i][j] = 0;
                }
            }
    
            vaixell = 0; // Inicialitzo abans de fer-la servir.
            for (int i = 0; i < MIDA; i++) { // b) Genero vaixells a posicions aleatories.
                for (int j = 0; j < MIDA; j++) {
                    while (vaixell < NUM_VAIXELLS) {
                        do {  // Genero les posicions i m'aseguro que siguin diferents.
                            posicioAleatoriaX = (int) (Math.random () * MIDA);
                            posicioAleatoriaY = (int) (Math.random () * MIDA);
                        } while (posicio[posicioAleatoriaX][posicioAleatoriaY] == 1);
                        posicio [posicioAleatoriaX][posicioAleatoriaY] = 1; // Assigno un vaixell a aquesta posició aleatoria.
                        vaixell++; // Compto que siguin 20 vaixells.
                    }
                }
            }
    
            System.out.printf("o\33c");
            // Explicació inicial del joc a l'usuari.
            System.out.println("Bienvenido al JUEGO DE LOS BARCOS o 'Hundir La Flota', hay un total de 20 barcos bajo la niebla de guerra, indique en que posición desea atacar.\nSi acierta se mostrará una 'O' en el punto.\nSi falla, una 'X'.\nCuando desee salir del juego introduzca un numero negativo.  \nPresione ENTER para empezar.");    
            input.nextLine (); // Quan acabi de llegir, l'usuari li donarà a enter per començar.
    
            for (int i = 0; i < MIDA; i++) { // Creo la matriu auxiliar amb punts.
                for (int j = 0; j < MIDA; j++) {
                    auxiliar [i][j] = '·';
                }
            }
    
            do {
                System.out.printf("o\33c");
                System.out.printf ("Recuerda: 'O' has hundido un barco\n'X', has fallado\n");
                System.out.printf("\n     ");
                for (int i = 0; i < MIDA; i++){ // Mostro les posicions DE X
                    System.out.printf ("%d  ", i);
                }
                System.out.printf (" X");
                System.out.printf ("\n-----------------------------------\n"); // Separo els números de posició de la matriu.
    
                for (int i = 0; i < MIDA; i++) { // Mostro per pantalla la matriu auxiliar.
                    System.out.printf ("%d | ", i); // Em primta la i, juntament amb una barra.
                    for (int j = 0; j < MIDA; j++) {
                        System.out.printf ("%2s ", auxiliar [i][j]);
                    
                    }
                    System.out.printf (" |");
                    System.out.println ();
                }
                System.out.printf ("Y\n"); // Mostro Y perquè l'usuari ho entengui.
    
                // L'usuari introdueix les coordenades en les quals vol intentar fondre un vaixell.
                do {
                    System.out.printf ("posición de X: ");
                    X = input.nextInt ();
                    System.out.printf ("posición de Y: ");
                    Y = input.nextInt();
        
                    if (auxiliar [X][Y] == 'X' || auxiliar [X][Y] == 'Y') {
                        System.out.printf("EY!\nQue ya has usado este movimiento, no hagas tonterías.\nVuelve a meter otras coordenadas:");
                    }
                } while (X > MIDA-1 || Y > MIDA -1 || auxiliar [X][Y] == 'X' || auxiliar [X][Y] == 'Y' );
    
                vaixellsEnfonsat = 0;
                if (posicio[X][Y] == 0) {
                    auxiliar[X][Y] = 'X';  // Si hi ha un vaixell en aquella posició,
                    vaixellsEnfonsat++;
                }
                else {
                    auxiliar[X][Y] = 'O';
                }
    
                if (vaixellsEnfonsat == 20) {
                    System.out.printf ("Enhorabuena! Has hundido todos los barcos.\nHas ganado!");
                }
            // L'usuari decideix sortir del programa.
                if (X < 0 || Y < 0) {
                    System.out.printf ("\nVaya! Has decidido salir del juego.");
                }
            } while (vaixellsEnfonsat < 20 || X >= 0 || Y >= 0);
        }
    }
