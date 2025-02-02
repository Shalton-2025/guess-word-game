#include <iostream>
#include <cstdlib>
#include <ctime>
#include <string>

using namespace std;

int main() {
    srand(time(0)); 				// Seed for random number generation

   						 // List of words to guess
    string words[] = {"apple", "banana", "cherry", "date", "elderberry"};
    int numWords = sizeof(words) / sizeof(words[0]);

   						 // Choose a random word
    string chosenWord = words[rand() % numWords];		

   						// Initialize the guessed word with at least two correct letters
    string guessedWord(chosenWord.size(), '_');
    int numCorrectLetters = 0;
    while (numCorrectLetters < 2) {
        int index = rand() % chosenWord.size();
        if (guessedWord[index] == '_') {
            guessedWord[index] = chosenWord[index];
            numCorrectLetters++;
        }
    }

   						// Initialize the number of tries
    int tries = 6;	

    cout << "Welcome to Word Guess!" << endl;
    cout << "You have 6 tries to guess the word." << endl;

    while (tries > 0) {
        cout << "\n" << guessedWord << endl;

      						  // Ask the user for a guess
        char guess;	
        cout << "Enter your guess: ";
        cin >> guess;

        // Check if the guess is in the chosen word
        bool correctGuess = false;
        for (int i = 0; i < chosenWord.size(); i++) {
            if (chosenWord[i] == guess && guessedWord[i] == '_') {
                guessedWord[i] = guess;
                correctGuess = true;
            }
        }

      						  // If the guess is incorrect, decrement the number of tries
        if (!correctGuess) {
            tries--;
            cout << "Incorrect guess. You have " << tries << " tries left." << endl;
        }

        					// Check if the user has won
        if (guessedWord == chosenWord) {
            cout << "\nCongratulations! You guessed the word: " << chosenWord << endl;
            return 0;
        }
    }

    						// If the user has run out of tries, they lose
    cout << "\nSorry, you ran out of tries. The word was: " << chosenWord << endl;
    return 0;
}
