# CNLab

## 23/March/2024

### Part 1
#### Client

```java
import java.io.*;
import java.net.*;

public class MyClient{
        public static void main(String[] args){
                try{
                        Socket s=new Socket("localhost",6666);
                        DataOutputStream dout =new DataOutputStream(s.getOutputStream());
                        dout.writeUTF("Hello Server");
                        dout.flush();
                        dout.close();
                        s.close();
                }
                catch(Exception e){
                        System.out.println(e);

                }
        }

}


```

#### Server

```java
import java.io.*;
import java.net.*;

public class MyServer{
        public static void main(String[] args){
                try{
                        ServerSocket ss=new ServerSocket(6666);
                        Socket s=ss.accept();
                        DataInputStream dis =new DataInputStream(s.getInputStream());
                        String str = (String)dis.readUTF();
                        System.out.println("message = "+str);
                        ss.close();
                }
                catch(Exception e){
                        System.out.println(e);
                }
        }

}
```

## Part 2

 
#### Client

```java
import java.io.*;
import java.net.*;

public class MyClient2{
        public static void main(String[] args)throws Exception{
                        Socket s=new Socket("localhost",3333);
                        DataInputStream din =new DataInputStream(s.getInputStream());
                        DataOutputStream dout =new DataOutputStream(s.getOutputStream());
                        BufferedReader br =new BufferedReader(new InputStreamReader(System.in));


                        String str1 = "" ,str2="";
                        while(!str1.equals("stop")){
                                str1=br.readLine();
                                dout.writeUTF(str1);
                                dout.flush();
                                str2=din.readUTF();
                                System.out.println("server says : " + str2);

                        }

                        dout.close();
                        s.close();
        }


}

```


#### Server

```java
public class MyServer2{
        public static void main(String[] args)throws Exception{
                        ServerSocket ss=new ServerSocket(3333);
                        Socket s=ss.accept();
                        DataInputStream din =new DataInputStream(s.getInputStream());
                        DataOutputStream dout =new DataOutputStream(s.getOutputStream());

                        BufferedReader br =new BufferedReader(new InputStreamReader(System.in));

                        String str1 = "" ,str2="";
                        while(!str1.equals("stop")){
                                str1=din.readUTF();
                                System.out.println("client says = "+str1);
                                str2=br.readLine();
                                dout.writeUTF(str2);
                                dout.flush();
                        }

                        din.close();
                        s.close();
                        ss.close();
        }


}
```
