# secure-coding-review
**This repo showcases a vulnerable server written by C**

## Security Vulnerabilities:

### 1-Buffer Overflow:

  - The buffer array in the handle_request function is fixed in size (BUFFER_SIZE). If the received data exceeds BUFFER_SIZE, this can lead to a buffer overflow, potentially allowing an attacker to overwrite memory and execute arbitrary code.
  
  - Recommendation: Always ensure that you read only as much data as can fit in the buffer. Use safer functions like recv() with explicit size checks or strncpy() instead of strcpy().

### 2-Lack of Input Validation:

  - The server does not validate the HTTP request properly. For example, it doesn’t check for potentially malicious payloads or malformed requests that could lead to attacks such as SQL Injection, Command Injection, or Path Traversal.
  
  - Recommendation: Always sanitize and validate inputs. For HTTP requests, ensure only valid HTTP methods (e.g., GET, POST) and headers are allowed. Reject requests with suspicious headers or malformed input.

### 3-Improper Error Handling:

  - Errors like failed recv() or send() calls are reported with perror(), but the system continues without closing the socket properly or handling potential resource leaks.
  
  - Recommendation: Implement proper error handling by checking return codes and freeing any allocated resources. Close sockets and handle memory allocation issues gracefully.

### 4-No Authentication or Authorization:

  - The server doesn’t have any form of authentication or authorization. This means anyone can access the server without any restrictions.
  
  - Recommendation: Implement authentication mechanisms (e.g., basic HTTP authentication or token-based authentication) and ensure that only authorized users can access sensitive endpoints.

### 5-Unencrypted Communication:

  - The application uses plain HTTP without encryption. This makes the server vulnerable to Man-in-the-Middle (MITM) attacks, where an attacker can intercept and manipulate traffic.
  
  - Recommendation: Implement HTTPS (using SSL/TLS) to encrypt communication between clients and the server. You can use libraries like OpenSSL for this.

### 6-Hardcoded Configuration:

  - The server listens on a hardcoded port (PORT 8080), which can be a security concern, especially if it's known to be an open port on the server.
  
  - Recommendation: Store configuration values such as ports in a configuration file or environment variables, so they can be easily changed without modifying the code.
