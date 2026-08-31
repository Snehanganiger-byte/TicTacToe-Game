# TicTacToe-Game
Java GUI Tic Tac Toe Game
import java.util.Scanner;

public class TicTacToe {

    static char[][] board = {
        {' ', ' ', ' '},
        {' ', ' ', ' '},
        {' ', ' ', ' '}
    };

    static char currentPlayer = 'X';

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.println("===== TIC TAC TOE =====");
        System.out.println("Player 1: X");
        System.out.println("Player 2: O");

        for (int turn = 0; turn < 9; turn++) {

            printBoard();

            System.out.print("Player " + currentPlayer +
                             ", enter row (1-3): ");
            int row = sc.nextInt() - 1;

            System.out.print("Enter column (1-3): ");
            int col = sc.nextInt() - 1;

            if (row < 0 || row > 2 || col < 0 || col > 2) {
                System.out.println("Invalid position! Try again.");
                turn--;
                continue;
            }

            if (board[row][col] != ' ') {
                System.out.println("Position already occupied!");
                turn--;
                continue;
            }

            board[row][col] = currentPlayer;

            if (checkWinner()) {
                printBoard();
                System.out.println("🎉 Player " + currentPlayer + " WINS!");
                sc.close();
                return;
            }

            currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
        }

        printBoard();
        System.out.println("🤝 It's a DRAW!");

        sc.close();
    }

    static void printBoard() {
        System.out.println();
        System.out.println("   1   2   3");
        System.out.println("1  " + board[0][0] + " | " +
                           board[0][1] + " | " + board[0][2]);
        System.out.println("  ---+---+---");
        System.out.println("2  " + board[1][0] + " | " +
                           board[1][1] + " | " + board[1][2]);
        System.out.println("  ---+---+---");
        System.out.println("3  " + board[2][0] + " | " +
                           board[2][1] + " | " + board[2][2]);
        System.out.println();
    }

    static boolean checkWinner() {

        // Rows
        for (int i = 0; i < 3; i++) {
            if (board[i][0] != ' ' &&
                board[i][0] == board[i][1] &&
                board[i][1] == board[i][2]) {
                return true;
            }
        }

        // Columns
        for (int i = 0; i < 3; i++) {
            if (board[0][i] != ' ' &&
                board[0][i] == board[1][i] &&
                board[1][i] == board[2][i]) {
                return true;
            }
        }

        // Diagonals
        if (board[0][0] != ' ' &&
            board[0][0] == board[1][1] &&
            board[1][1] == board[2][2]) {
            return true;
        }

        if (board[0][2] != ' ' &&
            board[0][2] == board[1][1] &&
            board[1][1] == board[2][0]) {
            return true;
        }

        return false;
    }
}
