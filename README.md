# ST10522363Part2POE

QuickChat is a Java console application. The user registers an account, logs in, and can then send messages through a simple numeric menu. The program was built in two parts:

- **Part 1 – Registration and login:** the user registers with a username, password and cell phone number, and then logs in with the same details.
- **Part 2 – Sending messages:** once logged in, the user can send, disregard or store messages.

All of the code is in one class, `Main`, in `src/main/java/com/mycompany/main/Main.java`.

## Features

### Registration and login
- The user enters their first name, last name, username, password and cell phone number.
- **Username:** must contain an underscore (`_`) and be no more than five characters long.
- **Password:** must be at least eight characters long and contain a capital letter, a number and a special character.
- **Cell phone number:** must start with `+` and an international code, followed by a number of no more than ten digits (for example `+27838968976`).
- The program keeps asking until each detail is correct.
- The user then logs in with the same username and password. A successful login shows: `Welcome <first name>, <last name> it is great to see you again.`

### QuickChat menu
After logging in the program shows `Welcome to QuickChat.` and asks how many messages the user wants to enter. The user can only enter that many messages. The menu then runs until the user chooses to quit:

1. **Send Messages** – write a message and choose to send, disregard or store it.
2. **Show recently sent messages** – shows `Coming Soon.` (still in development).
3. **Quit** – shows the total number of messages sent and exits.

### Each message contains
| Field | Description |
|---|---|
| Message ID | A random, unique ten-digit number |
| Message number | Starts at 0 and goes up as messages are sent |
| Recipient | A cell number with an international code |
| Message | No more than 250 characters |
| Message hash | First two digits of the ID, the message number, and the first and last words of the message, in capitals (for example `00:0:HITONIGHT`) |

After a message is written the user chooses one of:
- **Send Message** – `Message successfully sent.` The message ID, hash, recipient and message are then displayed.
- **Disregard Message** – `Press 0 to delete the message.`
- **Store Message to send later** – `Message successfully stored.` The message is saved in `storedMessages.json`.

The total number of messages sent is displayed once all the messages have been entered, and when the user quits.

## Requirements
- Java 17 or newer
- Maven (included with NetBeans)

## How to run

**In NetBeans:** open the project folder (File → Open Project) and run `Main.java`.

**From the command line:**
```
mvn compile exec:java -Dexec.mainClass=com.mycompany.main.Main
```
(The `exec:java` goal needs internet access the first time so Maven can download the exec plugin.)

## How to run the unit tests
```
mvn test
```
The tests are in `src/test/java/com/mycompany/main/MainTest.java` and use JUnit 5. They cover:
- the username, password and cell phone checks, and the login messages (Part 1)
- the message length, recipient number, message hash, message ID, send/disregard/store messages, total messages sent and JSON storage (Part 2)

## Project structure
```
quickchat-project/
├── pom.xml
├── README.md
├── .gitignore
├── .github/workflows/maven.yml     (runs the tests on GitHub)
└── src/
    ├── main/java/com/mycompany/main/Main.java
    └── test/java/com/mycompany/main/MainTest.java
```

## Continuous integration
A GitHub Actions workflow (`.github/workflows/maven.yml`) runs `mvn test` every time code is pushed to the `main` or `KhanbanTasks` branch, or a pull request is opened against `main`. This checks that the tests pass before changes are merged.

## Stored messages
Messages that the user chooses to store are written to `storedMessages.json` in the folder where the program is run. Each stored message looks like this:
```json
{
  "messageID": "0012345678",
  "messageHash": "00:0:HITONIGHT",
  "recipient": "+27718693002",
  "message": "Hi Mike, can you join us for dinner tonight?"
}
```

## References
- Oracle (n.d.) *java.util.regex.Pattern*. Available at: https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html (used for the cell phone number check).
- Ecma International (2017) *ECMA-404 The JSON data interchange syntax*. Available at: https://www.json.org/json-en.html (used for storing messages in JSON).

## Author
[Silindokuhle Mngwengwe] – [ST10522363]
