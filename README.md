# secure-coding-review
This repo showcases a vulnerable piece of code written by C 

Security Vulnerabilities:

  Buffer Overflow:
      The buffer array in the handle_request function is fixed in size (BUFFER_SIZE). If the received data exceeds BUFFER_SIZE, this can lead to a buffer overflow, potentially allowing an attacker to overwrite memory and execute arbitrary code.

      
