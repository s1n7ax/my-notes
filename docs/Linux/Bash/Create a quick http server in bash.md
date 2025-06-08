# Create a quick HTTP server in Bash

```bash
#!/bin/bash
# Simple HTTP server with Netcat

while true; do
  # Listen on port 8080 and capture incoming request into a variable
  REQUEST=$(echo -e "HTTP/1.1 200 OK\n\n $(date)" | nc -l -p 8080 -q 1)
  echo "Received request: $REQUEST"
done
```
