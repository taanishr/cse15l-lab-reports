# Part 1
## ChatServer Code
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

## Using /add-message
### Screenshot 1
![First screenshot of /add-message](/w3-lr-1.png)
a) I called the `handleRequest()`, `url.getPath()`, `equals()`, `getQuery()`, `split()`, and `String.format()` methods in my code.

b) `handleRequest` takes in the webpage's URL. The url (`http://localhost:4000/add-message?s=i%like%20hot%20dogs%20&user=taanish`) is stored in a `URI` object called `url`. The `equals` method checks that the webpage is on the `/add-message` path. If not, the `handleRequest` function returns the string `"404 Not Found!"`. I then split the query by `"&"`, and stored this value (the array `["s=i like hot dogs", "user=taanish"]`) in a local variable called `String[] parameters`. I further split the elements of `String[] parameters` by `"="` into `String[] message` (which holds an array `["message", "i like hot dogs"]`) and `String[] user` (which holds an array `["user", "taanish"]`). The only field from the class is `messages`, which is a string that holds all the messages added by users (seperated by newlines). It is initialized as an empty string `""`, and becomes `"taanish: i like hot dogs\n"`.

c) The `messages` field is initially empty (`""`). When this request is made, the `messages` field is updated to `"taanish: i like hot dogs\n"`.

### Screenshot 2
![First screenshot of /add-message](/w3-lr-1.png)
a) I called the `handleRequest()`, `url.getPath()`, `equals()`, `getQuery()`, `split()`, and `String.format()` methods in my code.

b) `handleRequest` takes in the webpage's URL. The url (`http://localhost:4000/add-message?s=the%20weather%20is%20nice%20today&user=someone%20else`) is stored in a `URI` object called `url`. The `equals` method checks that the webpage is on the `/add-message` path. If not, the `handleRequest `function returns the string `"404 Not Found!"`. I then split the query by `"&"`, and stored this value (the array `["s=the weather is nice today", "user=someone else"]`) in a local variable called `String[] parameters`. I further split the elements of `String[] parameters` by `"="` into `String[] message` (which holds an array `["message", "the weather is nice today"]`) and `String[] user` (which holds an array `["user", "someone else"]`). The only field from the class is `messages`, which is a string that holds all the messages added by users (seperated by newlines). Its value before this request was `taanish: i like hot dogs\n"`, but became `"taanish: i like hot dogs\nsomeone else: the weather is nice today\n"`.

c) The `messages` field is initially `"taanish: i like hot dogs\n"`. When this request is made, the `messages` field is updated to `"taanish: i like hot dogs\nsomeone else: the weather is nice today\n"`.

# Part 2
**Path to private key:** The path to my private key is `.ssh/id_rsa`. When ls is ran with `.ssh/id_rsa` as the path, the output is:
```
treja@Taanishs-MacBook-Air ~ % ls .ssh/id_rsa
.ssh/id_rsa
```

**Path to public key:** The path to my public key is `.ssh/authorized_keys`. When ls is ran with `.ssh/authorized_keys` as the path, the output is:
```
[treja@ieng6-203]:~:54$ ls .ssh/authorized_keys 
.ssh/authorized_keys
```

**Terminal interaction with ieng6:**
```
treja@Taanishs-MacBook-Air ~ % ssh treja@ieng6.ucsd.edu
Last login: Sat Jan 27 16:03:51 2024 from 100.90.236.54
quota: Cannot resolve mountpoint path /home/linux/ieng6/cs120wi24/public/.snapshot/daily.2023-12-28_0010: Stale file handle
Hello treja, you are currently logged into ieng6-203.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   16:05:01   23  0.31,  0.45,  0.65
ieng6-202   16:05:01   17  0.32,  0.41,  0.43
ieng6-203   16:05:01   23  3.36,  3.11,  2.57

 

To begin work for one of your courses [ cs15lwi24 ], type its name 
at the command prompt.  (For example, "cs15lwi24", without the quotes).

To see all available software packages, type "prep -l" at the command prompt,
or "prep -h" for more options.
[treja@ieng6-203]:~:52$ ls 
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos  perl5  wavelet
[treja@ieng6-203]:~:53$ 
```

# Part 3
One thing I learned from lab this week was setting up ssh. Logging into the server with my password each time was getting tedious, but private/public keys offer a more secure and convienent way to access servers. It also opens up a lot of operations, such as secure file transfers with scp

