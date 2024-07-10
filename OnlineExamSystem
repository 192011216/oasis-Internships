import java.util.*;

public class OnlineExamSystem {
    private String username;
    private String password;
    private boolean isLoggedIn;
    private int timeRemaining;
    private int questionCount;
    private int[] userAnswers;
    private int[] correctAnswers;

    public OnlineExamSystem(String username, String password) {
        this.username = username;
        this.password = password;
        System.out.println("Successfully registered!");
        System.out.println("Username: " + this.username);
        System.out.println("Password: " + this.password);
        System.out.println("Welcome to the Online Exam System! :)");
        this.isLoggedIn = false;
        this.timeRemaining = 10; // in minutes
        this.questionCount = 10;
        this.userAnswers = new int[questionCount];
        this.correctAnswers = new int[questionCount];
        // initialize correct answers with random values (0 or 1)
        for (int i = 0; i < questionCount; i++) {
            correctAnswers[i] = (int) Math.round(Math.random());
        }
    }

    public void login() {
        System.out.println("Log in to give the Exam");
        Scanner scanner = new Scanner(System.in);
        System.out.print("Username: ");
        String inputUsername = scanner.nextLine();
        System.out.print("Password: ");
        String inputPassword = scanner.nextLine();
        if (inputUsername.equals(username) && inputPassword.equals(password)) {
            isLoggedIn = true;
            System.out.println("Login successful! Best of luck!");
        } else {
            System.out.println("Login failed. Please try again.");
        }
    }

    public void logout() {
        isLoggedIn = false;
        System.out.println("Logout successful.");
    }

    public void updateProfile() {
        if (!isLoggedIn) {
            System.out.println("Please login first.");
            return;
        }
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter new username: ");
        String newUsername = scanner.nextLine();
        System.out.print("Enter new password: ");
        String newPassword = scanner.nextLine();
        this.username = newUsername;
        this.password = newPassword;
        System.out.println("Profile updated successfully!");
    }

    public void startExam() {
        if (!isLoggedIn) {
            System.out.println("Please login first.");
            return;
        }
        Scanner scanner = new Scanner(System.in);
        System.out.println("You have " + timeRemaining + " minutes to complete the exam.");
        long startTime = System.currentTimeMillis();
        long endTime = startTime + timeRemaining * 60 * 1000;
        for (int i = 0; i < questionCount; i++) {
            if (System.currentTimeMillis() > endTime) {
                System.out.println("Time is up! Auto-submitting the exam.");
                submitExam();
                return;
            }
            System.out.println("Question " + (i + 1) + ":");
            System.out.println("1. Option 1");
            System.out.println("2. Option 2");
            System.out.print("Your answer (1 or 2): ");
            int answer = scanner.nextInt();
            userAnswers[i] = answer;
        }
        System.out.println("Would you like to submit?\n1: Yes\n2: No");
        int n = scanner.nextInt();
        if (n == 1) {
            submitExam();
        } else {
            // auto-submit exam when time is up
            try {
                Thread.sleep(timeRemaining * 60 * 1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            submitExam();
        }
    }

    public void submitExam() {
        if (!isLoggedIn) {
            System.out.println("Please login first.");
            return;
        }
        int score = 0;
        for (int i = 0; i < questionCount; i++) {
            if (userAnswers[i] == correctAnswers[i]) {
                score++;
            }
        }
        System.out.println("Your score is " + score + " out of " + questionCount + ".");
        System.out.println("Best of luck! :)");
        logout();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        OnlineExamSystem examSystem = null;
        boolean exit = false;

        while (!exit) {
            System.out.println("Welcome to the Online Exam System!");
            System.out.println("1. Register");
            System.out.println("2. Login");
            System.out.println("3. Update Profile");
            System.out.println("4. Start Exam");
            System.out.println("5. Logout");
            System.out.println("6. Exit");
            System.out.print("Choose an option (1-6): ");
            int choice = sc.nextInt();
            sc.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    System.out.println("Enter your username and password to register");
                    System.out.print("Username: ");
                    String uName = sc.nextLine();
                    System.out.print("Password: ");
                    String pWord = sc.nextLine();
                    examSystem = new OnlineExamSystem(uName, pWord);
                    break;
                case 2:
                    if (examSystem == null) {
                        System.out.println("No registered users. Please register first.");
                    } else {
                        examSystem.login();
                    }
                    break;
                case 3:
                    if (examSystem == null) {
                        System.out.println("No registered users. Please register first.");
                    } else {
                        examSystem.updateProfile();
                    }
                    break;
                case 4:
                    if (examSystem == null) {
                        System.out.println("No registered users. Please register first.");
                    } else if (!examSystem.isLoggedIn) {
                        System.out.println("Please log in to start the exam.");
                    } else {
                        examSystem.startExam();
                    }
                    break;
                case 5:
                    if (examSystem != null && examSystem.isLoggedIn) {
                        examSystem.logout();
                    } else {
                        System.out.println("No active session to logout.");
                    }
                    break;
                case 6:
                    exit = true;
                    System.out.println("Exiting the system.");
                    break;
                default:
                    System.out.println("Invalid choice. Please choose again.");
                    break;
            }
        }
    }
}
