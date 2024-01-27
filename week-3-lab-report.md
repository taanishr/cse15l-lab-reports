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
b) handleRequest took in the webpage's URL. The equals method checked that the webpage was on the add-request path. I also split the query by the & (splitting the message and user) and these resulting message and user arrays by the = (splitting them into a prompt and value). The only relevant field from the class was messages, which was a string that held all the messages added by users (seperated by newlines).
c) The messages field is initially empty. When this request is made, the messages field is updated to "taanish: i like hot dogs\n".

### Screenshot 2
![First screenshot of /add-message](/w3-lr-1.png)
a) I called the handleRequest(), url.getPath(), equals(), getQuery(), split(), and String.format() methods in my code.
b) handleRequest took in the webpage's URL. The equals method checked that the webpage was on the add-request path. I also split the query by the & (splitting the message and user) and these resulting message and user arrays by the = (splitting them into a prompt and value). The only relevant field from the class was messages, which was a string that held all the messages added by users (seperated by newlines).
c) The messages field is initially "taanish: i like hot dogs\n". When this request is made, the messages field is updated to "taanish: i like hot dogs\nsomeone else: the weather is nice today\n".


