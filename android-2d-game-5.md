# Android 2D Game Development Notes 5

Don't forget to add `<uses-permission android:name="android.permission.INTERNET" />` under `<manifest>` in your `AndroidManifest.xml`.

## TCP Server

```java
import java.net.ServerSocket;
import java.net.Socket;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;

try {
  ServerSocket serverSocket = new ServerSocket(333);
  Socket socket = serverSocket.accept();
  ObjectOutputStream output = new ObjectOutputStream(socket.getOutputStream());
  ObjectInputStream input = new ObjectInputStream(socket.getInputStream());
  System.out.println("[Server] Receive request: " + input.readObject());
  System.out.println("[Server] Send response");
  output.writeObject("Hello too!");
  input.close();
  output.close();
  socket.close();
  serverSocket.close();
} catch (Exception e) {
  e.printStackTrace();
}
```

## TCP Client

```java
import java.net.ServerSocket;
import java.net.Socket;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;

try {
  Socket socket = new Socket("127.0.0.1", 333);
  ObjectOutputStream output = new ObjectOutputStream(socket.getOutputStream());
  ObjectInputStream input = new ObjectInputStream(socket.getInputStream());
  System.out.println("[Client] Send request");
  output.writeObject("Hello server!");
  System.out.println("[Client] Receive response: " + input.readObject());
  input.close();
  output.close();
  socket.close();
} catch (Exception e) {
  e.printStackTrace();
}
```

## UDP Broadcaster

```java
import java.net.DatagramSocket;
import java.net.DatagramPacket;
import java.net.InetAddress;

try {
  DatagramSocket socket = new DatagramSocket();
  socket.setBroadcast(true);
  byte[] buffer = "Hello world!".getBytes();
  InetAddress address = InetAddress.getByName("255.255.255.255");
  DatagramPacket packet = new DatagramPacket(buffer, buffer.length, address, 3333);
  System.out.println("[Server] Send message");
  socket.send(packet);
  socket.close();
} catch (Exception e) {
  e.printStackTrace();
}
```

## UDP Receiver

```java
import java.net.DatagramSocket;
import java.net.DatagramPacket;
import java.net.InetAddress;

try {
  DatagramSocket socket = new DatagramSocket(3333);
  DatagramPacket packet = new DatagramPacket(new byte[256], 256);
  socket.receive(packet);
  String message = new String(packet.getData(), 0, packet.getLength());
  System.out.println("[Client] Receive message: " + message);
  socket.close();
} catch (Exception e) {
  e.printStackTrace();
}
```

Done!
