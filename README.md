# Bruh

public class ComputerPlayer {
    private Random generator;
    private Scanner scan;
    private int generatedNumber;

    public ComputerPlayer() {
        generator = new Random();
        scan = new Scanner(System.in);
    }

    public void start() {
        boolean wantToPlay = false;
        do {
            System.out.print("Do you want to play a two-player game? Yes / No: ");
            wantToPlay = prompt();
            if (wantToPlay) {
                playTwoPlayerGame();
            } else {
                generatedNumber = super.randGenNum();
                playGame();
            }
        } while (!wantToPlay);
    }

    private void playGame() {
        // Existing code for single-player game...
    }

    private void playTwoPlayerGame() {
        int min = 1;
        int max = 100;
        int count = 0;
        String ans = "";

        System.out.print("Player 1, enter the number to guess (between 1 and 100): ");
        generatedNumber = scan.nextInt();
        scan.nextLine(); // Consume the newline character

        boolean done = false;
        while (!done) {
            int guess = min + (int)(Math.random() * (max - min + 1));
            count++;
            
            System.out.println("Player 2, guess the number: ");
            int playerGuess = scan.nextInt();
            scan.nextLine(); // Consume the newline character
            
            if (playerGuess > guess) {
                System.out.println("Too high! Player 2 needs to guess lower.");
                max = playerGuess - 1;
            } else if (playerGuess < guess) {
                System.out.println("Too low! Player 2 needs to guess higher.");
                min = playerGuess + 1;
            } else {
                System.out.println("Player 2 guessed the right number in " + count + " guesses!\n\n");
                done = true;
            }
        }
    }

    private boolean prompt() {
        while (true) {
            String input = scan.nextLine();
            if (input.equalsIgnoreCase("y") || input.equalsIgnoreCase("yes")) {
                return true;
            } else if (input.equalsIgnoreCase("n") || input.equalsIgnoreCase("no")) {
                return false;
            } else {
                System.out.print("Please enter 'Yes' or 'No': ");
            }
        }
    }
}
