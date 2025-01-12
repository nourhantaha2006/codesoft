C++
TASK(1)
#include <iostream>
#include <cstdlib>  // For rand() and srand()
#include <ctime>    // For time()

using namespace std;

int main() {
   
    srand(static_cast<unsigned int>(time(0)));

    // Generate a random number between 1 and 100
    int randomNumber = rand() % 100 + 1;
    int guess;
    int count = 0;

    cout << "Welcome to the Number Guessing Game!" << endl;
    cout << "I have selected a random number between 1 and 100." << endl;
    cout << "Can you guess what it is?" << endl;

    
    do {
        cout << "Enter your guess: ";
        cin >> guess;
        count++;

        if (guess < randomNumber) {
            cout << "Your guess is too low. Try again!" << endl;
        }
        else if (guess > randomNumber) {
            cout << "Your guess is too high. Try again!" << endl;
        }
        else {
            cout << "Congratulations! You've guessed the correct number " << randomNumber
                << " in " << count<< " attempts." << endl;
        }
    } while (guess != randomNumber);

    return 0;
}





TASK(2)
#include <iostream>
  
using namespace std;

int main() {
    int number1;
    int number2;
    cout << " plz,enter the two number that you want to calculate there" << endl;
    cout << "enter num1" << endl;
    cin >> number1;
    cout << "enter num2" << endl;
    cin >> number2;
    char operation;
    cout << "plz,enter the operation" << endl;
    cin >> operation;
    switch (operation)
    {
    case('+'):cout << number1 << "+" << number2 << "=" << number1 + number2 << endl;
        break;
    case('-'):cout << number1 << "-" << number2 << "=" << number1 - number2 << endl;
        break;
    case('*'):cout << number1 << "*" << number2 << "=" << number1 * number2 << endl;
        break;
        if (number2 == 0)
           
        
        cout << "invalid" << endl;
        else
    cout << number1 << "/" << number2 << "=" << number1 / number2 << endl;
        
        
   
    }
    
   
    

    return 0;
}
TASK(3)
#include <iostream>
#include <vector>

using namespace std;

// Function to display the game board
void displayBoard(const vector<vector<char>>& board) {
    cout << "Current Board:" << endl;
    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 3; ++j) {
            cout << board[i][j] << " ";
        }
        cout << endl;
    }
}

// Function to check for a win
bool checkWin(const vector<vector<char>>& board, char player) {
    // Check rows and columns
    for (int i = 0; i < 3; ++i) {
        if ((board[i][0] == player && board[i][1] == player && board[i][2] == player) ||
            (board[0][i] == player && board[1][i] == player && board[2][i] == player)) {
            return true;
        }
    }
    // Check diagonals
    if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
        (board[0][2] == player && board[1][1] == player && board[2][0] == player)) {
        return true;
    }
    return false;
}

bool checkDraw(const vector<vector<char>>& board) {
    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 3; ++j) {
            if (board[i][j] == ' ') {
                return false; // If there's an empty space, it's not a draw
            }
        }
    }
    return true; // No empty spaces, it's a draw
}

// Main function
int main() {
    char playAgain;
    do {
        vector<vector<char>> board(3, vector<char>(3, ' ')); // Initialize a 3x3 board
        char currentPlayer = 'X'; // Start with player X
        bool gameWon = false;

        while (!gameWon) {
            displayBoard(board);
            int row, col;

            // Prompt the current player for their move
            cout << "Player " << currentPlayer << ", enter your move (row and column): ";
            cin >> row >> col;

            // Validate input
            if (row < 0 || row > 2 || col < 0 || col > 2 || board[row][col] != ' ') {
                cout << "Invalid move. Try again." << endl;
                continue;
            }

            // Update the board with the player's move
            board[row][col] = currentPlayer;

            // Check for a win
            if (checkWin(board, currentPlayer)) {
                displayBoard(board);
                cout << "Player " << currentPlayer << " wins!" << endl;
                gameWon = true;
            }
            else if (checkDraw(board)) {
                displayBoard(board);
                cout << "It's a draw!" << endl;
                gameWon = true;
            }
            else {
                // Switch players
                currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
            }
        }

        // Ask if players want to play again
        cout << "Do you want to play again? (y/n): ";
        cin >> playAgain;

    } while (playAgain == 'y' || playAgain == 'Y');

    cout << "Thank you for playing!" << endl;
    return 0;
}

TASK(4)
#include <iostream>
#include <vector>
#include <string>

using namespace std;

// Task structure to hold task details
struct Task {
    string description;
    bool completed;

    Task(string desc) : description(desc), completed(false) {}
};

// Function to display the list of tasks
void displayTasks(const vector<Task>& tasks) {
    cout << "\nTo-Do List:\n";
    for (size_t i = 0; i < tasks.size(); ++i) {
        cout << i + 1 << ". " << tasks[i].description
            << " [" << (tasks[i].completed ? "Completed" : "Pending") << "]\n";
    }
    cout << endl;
}

// Function to add a task
void addTask(vector<Task>& tasks) {
    string taskDescription;
    cout << "Enter the task description: ";
    cin.ignore(); // Clear the input buffer
    getline(cin, taskDescription);
    tasks.emplace_back(taskDescription);
    cout << "Task added successfully!\n";
}

// Function to mark a task as completed
void markTaskAsCompleted(vector<Task>& tasks) {
    int taskNumber;
    cout << "Enter the task number to mark as completed: ";
    cin >> taskNumber;

    if (taskNumber > 0 && taskNumber <= tasks.size()) {
        tasks[taskNumber - 1].completed = true;
        cout << "Task marked as completed!\n";
    }
    else {
        cout << "Invalid task number!\n";
    }
}

void removeTask(vector<Task>& tasks) {
    int taskNumber;
    cout << "Enter the task number to remove: ";
    cin >> taskNumber;

    if (taskNumber > 0 && taskNumber <= tasks.size()) {
        tasks.erase(tasks.begin() + taskNumber - 1);
        cout << "Task removed successfully!\n";
    }
    else {
        cout << "Invalid task number!\n";
    }
}
int main() {
    vector<Task> tasks;
    int choice;

    do {
        cout << "\nTo-Do List Manager\n";
        cout << "1. Add Task\n";
        cout << "2. View Tasks\n";
        cout << "3. Mark Task as Completed\n";
        cout << "4. Remove Task\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            addTask(tasks);
            break;
        case 2:
            displayTasks(tasks);
            break;
        case 3:
            markTaskAsCompleted(tasks);
            break;
        case 4:
            removeTask(tasks);
            break;
        case 5:
            cout << "Exiting the program. Goodbye!\n";
            break;
        default:
            cout << "Invalid choice! Please try again.\n"
        }
    } while (choice != 5);

    return 0;
}        
                         
                               PYTHON TASKS


                               task(2)

print("Enter the first number, please")
num1 = float(input())  # Convert to float to handle decimal numbers
print("Enter the second number, please")
num2 = float(input())  # Convert to float to handle decimal numbers
print("Enter the operator (+, -, /, *):")
op = input()

if op == "+":
    print(num1 + num2)
elif op == "-":
    print(num1 - num2)
elif op == "/":
    if num2 == 0:
        print("Invalid: Division by zero")
    else:
        print(num1 / num2)
elif op == "*":
    print(num1 * num2)
else:
    print("Invalid operator")
    
                           task(3)
import random
import string

print("Enter the length of the password you want:")
length = int(input())  # Convert input to an integer

# Create a string containing uppercase letters, lowercase letters, digits, and special characters
characters = string.ascii_letters + string.digits + string.punctuation

# Generate a random password of the specified length
strongpassword = ''.join(random.choice(characters) for i in range(length))

print("Your strong password is:")
print(strongpassword)

                         task(4)
import random

def play_game():
    print("We are in a game\nPlease, enter your choice from (rock, paper, scissors):")
    choices = ["rock", "paper", "scissors"]
    choice = input().lower()  # Ensure user input is case-insensitive

    # Randomly choose for the computer
    computerchoice = random.choice(choices)

    # Determine the result
    if computerchoice == "rock" and choice == "scissors":
        result = "You are the loser!"
    elif computerchoice == "scissors" and choice == "paper":
        result = "You are the loser!"
    elif computerchoice == "paper" and choice == "rock":
        result = "You are the loser!"
    elif computerchoice == choice:
        result = "It's a tie!"
    else:
        result = "You are the winner!"

    # Print the result
    print(f"Your choice: {choice}")
    print(f"Computer's choice: {computerchoice}")
    print(result)
    print("With my best wishes!")

# Run the game in a loop
while True:
    play_game()  # Play the game

    print("Do you want to play again? (yes/no)")
    answer = input().lower()

    if answer != "yes":
        print("Thanks for playing!")
        break  # Exit the loop if the user doesn't want to play again


        


                                                           
                            
                            
                            
