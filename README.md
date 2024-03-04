# CNLab

## 23/Feb/2024

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

## 4/March/2024

#### Sender

```java
import java.net.*;
public class DSender{
        public static void main(String[] args)throws Exception{
                DatagramSocket ds=new DatagramSocket();
                String str ="Welcome java";
                InetAddress ip = InetAddress.getByName("127.0.0.1");
                DatagramPacket dp=new DatagramPacket(str.getBytes(),str.length(),ip,3000);
                ds.send(dp);
                ds.close();

        }

}

```

#### Reciever

```java
import java.net.*;
public class DReceiver{
        public static void main(String[] args)throws Exception{
                DatagramSocket ds=new DatagramSocket(3000);
                byte[] buf=new byte[1024];

                DatagramPacket dp=new DatagramPacket(buf,1024);
                ds.receive(dp);
                String str=new String(dp.getData(),0,dp.getLength());
                System.out.println(str);
                ds.close();

        }

}

```
