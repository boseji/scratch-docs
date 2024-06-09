# TCP Socket Server under Linux

## Creating a Simple TCP Socket Server in Bash

<https://www.baeldung.com/linux/bash-tcp-socket-server>

**[PDF version](./Creating-a-Simple-TCP-Socket-Server-in-Bash-on-Linux.pdf)** of the same.

### Using `netcat` in Linux to Create a loop TCP Server and Client

Installation:
```sh
sudo apt install netcat-openbsd
```

```sh
sudo pacman -S netcat
```

Server:
```sh
nc -k -l 8080
```

The `-k` option tells `netcat` to continue listening after the first connection completes rather than exiting the program. The `nc` command processes the incoming connections sequentially, not concurrently. In addition, the `-l` option instructs `netcat` to operate in listening mode.

Client:
```sh
nc localhost 8080
```

## How to Read Data From a Socket in Bash on Linux

<https://www.howtogeek.com/787892/how-to-read-data-from-a-socket-in-bash-on-linux/>

**[PDF Version](How-to-Read-Data-From-a-Socket-in-Bash-on-Linux.pdf)** of the same.

### Sending Data to a File using `netcat`

```sh
nc -l -p 8080 > logfile.txt
```

Here the `-p` specifies the port.

### Accepting Multiple Connections in `netcat`

```sh
nc -k -l -p 6566
```

Here the `-p` specifies the port.

----
<!-- Footer Begins Here -->
## Links

- [Back to Root Document](../README.md)
