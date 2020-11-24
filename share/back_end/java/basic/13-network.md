#### 网络编程

- 概要：
    - 简介：
        - 网络通信的要素：
            - 通信双方的地址：
                - ip：
                    - InetAddress类
                - 端口号：
                    - InetScoketAddress
            - 规则：网络通信的协议
                - TCP/IP四层概念模型
                - OSI七层网络模型
- 语法：
- 案例：
```java
    //TCP
        //client
            package com.tsing.network;

            import java.io.IOException;
            import java.io.OutputStream;
            import java.net.InetAddress;
            import java.net.Socket;
            import java.net.UnknownHostException;

            public class Client {
                public static void main(String[] args) {
                    Socket socket = null;
                    OutputStream outputStream = null;
                    try {
                        InetAddress serverIp = InetAddress.getByName("127.0.0.1");
                        int port = 9999;

                        socket = new Socket(serverIp, port);

                        outputStream = socket.getOutputStream();

                        outputStream.write("你好，青衣".getBytes());

                    } catch (Exception e) {
                        e.printStackTrace();
                    }finally {
                        try {
                            socket.close();
                            outputStream.close();
                        } catch (IOException e) {
                            e.printStackTrace();
                        }
                    }
                }
            }
        
        //server
            package com.tsing.network;

            import com.sun.xml.internal.bind.v2.util.ByteArrayOutputStreamEx;

            import java.io.ByteArrayOutputStream;
            import java.io.IOException;
            import java.io.InputStream;
            import java.net.ServerSocket;
            import java.net.Socket;

            public class Server {

                public static void main(String[] args) {

                    ServerSocket serverSocket = null;
                    Socket socket = null;
                    InputStream inputStream = null;
                    ByteArrayOutputStream outputStream = null;

                    try {
                        serverSocket = new ServerSocket(9999);
                        socket = serverSocket.accept();
                        inputStream = socket.getInputStream();

                        outputStream = new ByteArrayOutputStream();

                        byte[] buffer = new byte[1024];
                        int len;
                        while ((len = inputStream.read(buffer)) != -1){
                            outputStream.write(buffer, 0, len);
                        }
                        System.out.println(outputStream);
                    } catch (IOException e) {
                        e.printStackTrace();
                    }finally {
                        try {
                            outputStream.close();
                            inputStream.close();
                            socket.close();
                            serverSocket.close();
                        } catch (IOException e) {
                            e.printStackTrace();
                        }
                    }
                }
            }

    //UDP
        //client
            package com.tsing.network;

            import java.net.DatagramPacket;
            import java.net.DatagramSocket;
            import java.net.InetAddress;
            import java.net.SocketException;

            public class UdpClient {
                public static void main(String[] args) {
                    try {
                        DatagramSocket socket = new DatagramSocket();
                        String msg = "你好青衣";
                        InetAddress inetAddress = InetAddress.getByName("127.0.0.1");
                        int port = 9090;

                        DatagramPacket packet = new DatagramPacket(msg.getBytes(), 0, msg.getBytes().length, inetAddress, port);

                        socket.send(packet);
                        socket.close();
                    } catch (Exception e) {
                        e.printStackTrace();
                    }
                }
            }
        //server
            package com.tsing.network;

            import java.net.DatagramPacket;
            import java.net.DatagramSocket;
            import java.net.SocketException;

            public class UdpServer {

                public static void main(String[] args) {
                    try {
                        DatagramSocket socket = new DatagramSocket(9090);
                        byte[] buffer = new byte[1024];
                        DatagramPacket packet = new DatagramPacket(buffer, 0, buffer.length);

                        socket.receive(packet);

                        System.out.println(new String(packet.getData(), 0, packet.getLength()));
                        socket.close();
                    } catch (Exception e) {
                        e.printStackTrace();
                    }
                }

            }

```
