#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

void displayWord(char word[], char guessed[], int length);
int checkWin(char word[], char guessed[], int length);

int main() {
    char word[] = "program";  // The word to guess (You can change this)
    int length = strlen(word);
    char guessed[length];  
    int lives = 6, i, found, win;

    // Initialize guessed word with '_'
    for (i = 0; i < length; i++) {
        guessed[i] = '_';
    }
    guessed[length] = '\0';

    printf("==== Welcome to Hangman! ====\n");

    while (lives > 0) {
        char guess;
        found = 0;

        displayWord(word, guessed, length);
        printf("\nLives left: %d", lives);
        printf("\nEnter a letter: ");
        scanf(" %c", &guess);
        guess = tolower(guess); // Convert input to lowercase

        // Check if the letter is in the word
        for (i = 0; i < length; i++) {
            if (word[i] == guess && guessed[i] == '_') {
                guessed[i] = guess;
                found = 1;
            }
        }

        if (!found) {
            lives--; // Reduce life if the guess is incorrect
            printf("Incorrect guess! Lives left: %d\n", lives);
        } else {
            printf("Good guess!\n");
        }

        // Check if player has won
        win = checkWin(word, guessed, length);
        if (win) {
            printf("\nCongratulations! You guessed the word: %s\n", word);
            return 0;
        }
    }

    // If the player loses
    printf("\nGame Over! The correct word was: %s\n", word);
    return 0;
}

// Function to display the word with guessed letters
void displayWord(char word[], char guessed[], int length) {
    printf("\nWord: ");
    for (int i = 0; i < length; i++) {
        printf("%c ", guessed[i]);
    }
    printf("\n");
}

// Function to check if the player has won
int checkWin(char word[], char guessed[], int length) {
    for (int i = 0; i < length; i++) {
        if (guessed[i] == '_') {
            return 0; // Not yet completed
        }
    }
    return 1; // All letters guessed
}
