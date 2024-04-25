# ChatServer
---
Code of my ChatServer
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    ArrayList<String> chat = new ArrayList<>();

    public static String concatenateArrayList(ArrayList<String> list) {
        StringBuilder sb = new StringBuilder();
        
        // Append each element to the StringBuilder
        for (String element : list) {
            sb.append(element);
        }
        
        // Remove the trailing space
        if (sb.length() > 0) {
            sb.deleteCharAt(sb.length() - 1);
        }
        
        return sb.toString();
    }

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return "Put in your message and your name to chat with me!";
        } else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("&");
                String[] parsedName = parameters[1].split("=");
                String[] parsedMessage = parameters[0].split("=");
                String name = parsedName[1];
                String message = parsedMessage[1];
                chat.add(name);
                chat.add(": ");
                chat.add(message);
                chat.add("\n");
                String result = concatenateArrayList(chat);
                return result;
            }
            return "404 Not Found!";
        }
    }
}

class NumberServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

```

Screenshots of using `/add-message`:
![image](https://github.com/Fro0t/cse15l-lab-reports/assets/165719298/1191aabd-0dde-435d-87fd-3fe669916ea3)
![image](https://github.com/Fro0t/cse15l-lab-reports/assets/165719298/47200974-9cac-4c21-978a-1bb3ff31532b)
![image](https://github.com/Fro0t/cse15l-lab-reports/assets/165719298/20296f7b-8038-4e88-a01f-1f47c8530049)
![image](https://github.com/Fro0t/cse15l-lab-reports/assets/165719298/0b65f6f4-a3fc-439c-b8e2-bbca8bc1174e)

For both screenshots, method `concatenateArrayList`, which I created to convert the `String[]` into an easily printable `String`, and method
`handleRequest` are called.

For method `concatenateArrayList`, it's a static method that converts the input `String[]` into a `String`. It doesn't use any fields of the class `Handler`. The argument it takes, a `String[]`, would be the cumulative messages we stored in our method `handleRequest`. 
Method `handleRequest` takes in an URL and basically reads its composition. If it matches the specific request, then it takes the input message and the name, and adds it to the cumulative `String[]` "message box" called `chat`. `parameter` is the parsed URL separated by the `&`, because we need name and message, with name in front of message. `parsedName` and `parsedMessage` are the `String[]` after splitting `=` signs. They are further converted into `name` and `message` for actual names and message contents by choosing the last element out of both of them. Then, they are both added to `chat`, the cumulative name and message storage list. New line symbol and colon are added to fit the formatting. Finally, calling the static method `concatenateArraylist` to convert this list into a formatted String as an output.

The only field in the class `Handler` that changes is the `ArrayList<String> chat`. It's being updated everytime a new URL is entered with name and message. They will be added to `chat` from successful URL called requests. This is so that the program always prints all the messages and names that it has taken.


# Part 2
<img width="576" alt="image" src="https://github.com/Fro0t/cse15l-lab-reports/assets/165719298/f8b4c0e2-01aa-42e8-8284-c4974753d359">
<img width="615" alt="image" src="https://github.com/Fro0t/cse15l-lab-reports/assets/165719298/b153ea68-ee4d-4a01-b37b-65d274d55db3">
<img width="557" alt="image" src="https://github.com/Fro0t/cse15l-lab-reports/assets/165719298/03657221-1d54-4d1d-87ea-157d6c8a197e">


# Part 3
I learnt that `String[]` is problematic if we want to print it out, because when we use `toString()` method on it, it automatically adds the brackets and commas to the output string as well. I also learnt that a frame for a web server is highly universal. I just made a few changes to turn the server into another one that takes in some more complicated arguments. However, it's also not desirable to have the fields in the server class to cumulate everything that we have inputed. This way, even if you go back, the values are still added and the changes are still being made. It's also interesting to get to know what the web servers are looking for (the keys) when we try to log in.
