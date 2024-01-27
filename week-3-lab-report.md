# ChatServer Code
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler{
    String messages = "";
    @Override
    public String handleRequest(URI url) {
        if (url.getPath().equals("/add-message")) {
            String[] parameters = url.getQuery().split("&");
            String[] message = parameters[0].split("=");
            String[] user = parameters[1].split("=");
            messages += String.format("%s: %s \n", user[1], message[1]);
            return messages;
            
        }
        return "404 Not Found!";
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException{
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```

# Using /add-message
### Screenshot 1
![First screenshot of /add-message](/w3-lr-1.png)
a) I called the handleRequest(), url.getPath(), equals(), getQuery(), split(), and String.format() methods in my code.

b) handleRequest takes in the webpage's URL. The url argument (`"http://localhost:4000/add-message?s=i%like%20hot%20dogs%20&user=taanish"`) is stored in a `URI` variable called `url`. The equals method checks that the webpage is on the `/add-message` path. If not, the handleRequest function returns the string `"404 Not Found!"`. I then split the query by `"&"`, and stored this value (the array `["s=i like hot dogs", "user=taanish"]`) in a local variable called `String[] parameters`. I further split the elements of `String[] parameters` by `"="` into `String[] message` (which holds an array `["message", "i like hot dogs"]`) and `String[] user` (which holds an array `["user", "taanish"]`). The only field from the class is messages, which is a string that holds all the messages added by users (seperated by newlines). It is initialized as an empty string `""`, and becomes `"taanish: i like hot dogs\n"`.

c) The messages field is initially empty (`""`). When this request is made, the messages field is updated to `"taanish: i like hot dogs\n"`.

### Screenshot 2
![First screenshot of /add-message](/w3-lr-1.png)
a) I called the handleRequest(), url.getPath(), equals(), getQuery(), split(), and String.format() methods in my code.

b) handleRequest takes in the webpage's URL. The url argument (`http://localhost:4000/add-message?s=the%20weather%20is%20nice%20today&user=someone%20else`) is stored in a `URI` variable called `url`. The equals method checks that the webpage is on the `/add-message` path. If not, the handleRequest function returns the string `"404 Not Found!"`. I then split the query by `"&"`, and stored this value (the array `["s=the weather is nice today", "user=someone else"]`) in a local variable called `String[] parameters`. I further split the elements of `String[] parameters` by `"="` into `String[] message` (which holds an array `["message", "the weather is nice today"]`) and `String[] user` (which holds an array `["user", "someone else"]`). The only field from the class is messages, which is a string that holds all the messages added by users (seperated by newlines). Its value before this request was `taanish: i like hot dogs\n"`, but became `"taanish: i like hot dogs\nsomeone else: the weather is nice today\n"`.

c) The messages field is initially `"taanish: i like hot dogs\n"`. When this request is made, the messages field is updated to `"taanish: i like hot dogs\nsomeone else: the weather is nice today\n"`.


