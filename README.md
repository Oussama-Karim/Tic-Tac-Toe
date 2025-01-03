# Tic-Tac-Toe
#include <stdio.h>
#include <stdlib.h>
#include <stdio.h>

char board[3][3];  // 3x3 game board
char currentPlayer; // Tracks the current player ('X' or 'O')

// Functions
void initializeBoard();
void printBoard();
int isBoardFull();
int checkWin();
void playerMove();

int main() {
    // Initialize game
    initializeBoard();
    currentPlayer = 'X'; // Player X starts

    while (1) {
        printBoard(); // Display current board
        playerMove();  

        // Check for a win
        if (checkWin()) {
            printBoard();
            printf("Player %c wins!\n", currentPlayer);
            break;
        }

        // Check for a draw
        if (isBoardFull()) {
            printBoard();
            printf("It's a draw!\n");
            break;
        }

        // Switch players
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    return 0;
}

// Function to initialize the board
void initializeBoard() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            board[i][j] = ' '; // Empty space
        }
    }
}

// Function to print the current state of the board
void printBoard() {
    printf("\n");
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            printf(" %c ", board[i][j]);
            if (j < 2) printf("|");
        }
        printf("\n");
        if (i < 2) {
            printf("---|---|---\n");
        }
    }
    printf("\n");
}

// Function to check if the board is full (draw condition)
int isBoardFull() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] == ' ') {
                return 0; // Not full
            }
        }
    }
    return 1; // Board is full
}

// Function to check if the current player has won
int checkWin() {
    // Check rows and columns
    for (int i = 0; i < 3; i++) {
        if ((board[i][0] == currentPlayer && board[i][1] == currentPlayer && board[i][2] == currentPlayer) ||
            (board[0][i] == currentPlayer && board[1][i] == currentPlayer && board[2][i] == currentPlayer)) {
            return 1;
        }
    }

    // Check diagonals
    if ((board[0][0] == currentPlayer && board[1][1] == currentPlayer && board[2][2] == currentPlayer) ||
        (board[0][2] == currentPlayer && board[1][1] == currentPlayer && board[2][0] == currentPlayer)) {
        return 1;
    }

    return 0;
}

// Function to get player's move
void playerMove() {
    int row, col;

    while (1) {
        printf("Player %c, enter row and column (1-3) for your move: ", currentPlayer);
        scanf("%d %d", &row, &col);
        row--; // Convert to 0-indexed
        col--; // Convert to 0-indexed

        // Check if the position is valid
        if (row >= 0 && row < 3 && col >= 0 && col < 3 && board[row][col] == ' ') {
            board[row][col] = currentPlayer;
            break;
        } else {
            printf("Invalid move! Try again.\n");
        }
    }
}
