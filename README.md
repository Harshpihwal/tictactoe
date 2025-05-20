# tictactoe
import java.util.Scanner;

public class TicTacToe {
    private static char[][] board = {
            {' ', ' ', ' '},
            {' ', ' ', ' '},
            {' ', ' ', ' '}
    };
    private static char currentPlayer = 'X';

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        boolean gameEnded = false;

        System.out.println("Welcome to Tic-Tac-Toe!");
        printBoard();

        while (!gameEnded) {
            System.out.println("Player " + currentPlayer + "'s turn.");
            int row, col;

            while (true) {
                System.out.print("Enter row (0, 1, 2): ");
                row = scanner.nextInt();
                System.out.print("Enter column (0, 1, 2): ");
                col = scanner.nextInt();

                if (isValidMove(row, col)) {
                    board[row][col] = currentPlayer;
                    break;
                } else {
                    System.out.println("This move is not valid, try again.");
                }
            }

            printBoard();

            if (checkWinner()) {
                System.out.println("Player " + currentPlayer + " wins!");
                gameEnded = true;
            } else if (isBoardFull()) {
                System.out.println("It's a draw!");
                gameEnded = true;
            } else {
                switchPlayer();
            }
        }

        scanner.close();
    }

    private static void printBoard() {
        System.out.println("  0   1   2");
        for (int i = 0; i < 3; i++) {
            System.out.println(" -----------");
            System.out.print(i + "|");
            for (int j = 0; j < 3; j++) {
                System.out.print(" " + board[i][j] + " |");
            }
            System.out.println();
        }
        System.out.println(" -----------");
    }

    private static boolean isValidMove(int row, int col) {
        return row >= 0 && row < 3 &&
               col >= 0 && col < 3 &&
               board[row][col] == ' ';
    }

    private static boolean isBoardFull() {
        for (int i = 0; i < 3; i++)
            for (int j = 0; j < 3; j++)
                if (board[i][j] == ' ')
                    return false;
        return true;
    }

    private static void switchPlayer() {
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    private static boolean checkWinner() {
        // Rows & Columns
        for (int i = 0; i < 3; i++) {
            if ((board[i][0] == currentPlayer &&
                 board[i][1] == currentPlayer &&
                 board[i][2] == currentPlayer) ||
                (board[0][i] == currentPlayer &&
                 board[1][i] == currentPlayer &&
                 board[2][i] == currentPlayer))
                return true;
        }

        // Diagonals
        if ((board[0][0] == currentPlayer &&
             board[1][1] == currentPlayer &&
             board[2][2] == currentPlayer) ||
            (board[0][2] == currentPlayer &&
             board[1][1] == currentPlayer &&
             board[2][0] == currentPlayer))
            return true;

        return false;
    }
}
