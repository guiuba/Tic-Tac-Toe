import java.util.Scanner;

public class Main {
    static Scanner scan = new Scanner(System.in);
    static boolean isXyValid = false;
    static int move = 1;
    static String signal;
    static int x = 0, y = 0;
    static boolean isGameOver = false;
    static String[][] gameField = new String[3][3];

    public static void main(String[] args) {
        initializeGameField();
        printGameField();
        playGame();
    }

    public static void initializeGameField() {
        for (int i = 0; i < 9; i++) {
            gameField[i / 3][i % 3] = " ";
        }
    }

    public static void printGameField() {
        System.out.println("---------");
        for (int i = 0; i < gameField.length; i++) {
            System.out.printf("| %s %s %s |\n", gameField[i][0], gameField[i][1], gameField[i][2]);
        }
        System.out.println("---------");
    }

    public static void playGame() {

        while (!isXyValid) {
            while (!isGameOver) {
                if (move % 2 == 1) { // player 'X'
                    signal = "X";
                } else {            // player 'O'
                    signal = "O";
                }
                System.out.println("Enter the coordinates: ");
                try {
                    int xy = Integer.parseInt(scan.nextLine().replace(" ", ""));
                    x = xy / 10;
                    y = xy % 10;
                    if (x > 3 || y > 3) {
                        System.out.println("Coordinates should be from 1 to 3!");
                    } else if (x >= 1 || y >= 1) {
                        if (!gameField[-y + 3][x - 1].equals(" ")) {
                            System.out.println("This cell is occupied! Choose another one!");
                        } else {
                            gameField[-y + 3][x - 1] = signal;
                            printGameField();
                            isGameOver = checkGame();
                            move++;
                            isXyValid = true;
                        }
                    }
                } catch (NumberFormatException e) {
                    System.out.println("You should enter numbers!");
                }
            }

        }
        scan.close();
    }

    public static boolean checkGame() {
        if (gameField[0][0].equals("X") && gameField[0][1].equals("X") && gameField[0][2].equals("X") ||
                gameField[1][0].equals("X") && gameField[1][1].equals("X") && gameField[1][2].equals("X") ||
                gameField[2][0].equals("X") && gameField[2][1].equals("X") && gameField[2][2].equals("X") ||
                gameField[0][0].equals("X") && gameField[1][0].equals("X") && gameField[2][0].equals("X") ||
                gameField[0][1].equals("X") && gameField[1][1].equals("X") && gameField[2][1].equals("X") ||
                gameField[0][2].equals("X") && gameField[1][2].equals("X") && gameField[2][2].equals("X") ||
                gameField[0][0].equals("X") && gameField[1][1].equals("X") && gameField[2][2].equals("X") ||
                gameField[2][0].equals("X") && gameField[1][1].equals("X") && gameField[0][2].equals("X")) {
            System.out.println("X wins");
            return true;
        } else if (gameField[0][0].equals("O") && gameField[0][1].equals("O") && gameField[0][2].equals("O") ||
                gameField[1][0].equals("O") && gameField[1][1].equals("O") && gameField[1][2].equals("O") ||
                gameField[2][0].equals("O") && gameField[2][1].equals("O") && gameField[2][2].equals("O") ||
                gameField[0][0].equals("O") && gameField[1][0].equals("O") && gameField[2][0].equals("O") ||
                gameField[0][1].equals("O") && gameField[1][1].equals("O") && gameField[2][1].equals("O") ||
                gameField[0][2].equals("O") && gameField[1][2].equals("O") && gameField[2][2].equals("O") ||
                gameField[0][0].equals("O") && gameField[1][1].equals("O") && gameField[2][2].equals("O") ||
                gameField[2][0].equals("O") && gameField[1][1].equals("O") && gameField[0][2].equals("O")) {
            System.out.println("O wins");
            return true;
        } else if (move == 9) {
            System.out.println("Draw");
            return true;
        }
        return false;
    }

}
