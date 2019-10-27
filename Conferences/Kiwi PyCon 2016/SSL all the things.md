---
videos:
- https://youtu.be/0J7NuKjBL7Y
---

# SSL all the things

## General

SSL 2 and 3 are broken. TLS 1.0 and 1.1 are outdated, don't use it unless you need to support older clients.

There are only a few root CA (certificate authority) trusted by the browsers (hardcoded). Certificates aren't issued by these root CAs but by some intermediates CAs. This is known as the **trust chain**.

## Let's Encrypt

Let's Encrypt is only an intermediate certificate but will be added to the list of root certificates in Firefox 50.

Certificates issued by Let's Encrypt are only valid for 3 months.

Let's Encrypt process:

1. Create an account
2. Request a `certificate key` with the `account key` from step 1
3. Copy the challenges to a HTTP accessible endpoint
4. Request challenge verification
5. Pull until completed
6. You have a certificate

Use `acme-tiny` for automation.

It is important to know ahead of time how to revoke a certificate or an account key. You don't want to have to figure this out in a rush.

## Python

As client, wrap your socket with the SSL context but don't forget to pass the hostname as you do so. Otherwise you could verify the valid certificate but navigate on a completely different website. Or use `requests` which probably does that for you.

```python
import socket, ssl

HOST, PORT = 'example.com', 443

def handle(conn):
	conn.write(b'GET / HTTP/1,1\n')
	print(con.recv().decode())
	
def main():
	sock = socket.socket(socket.AF_INET)
	context = ssl.create_default_context(ssl.Purpose.SERVER_AUTH)
	context.options |= ssl.OP_NO_TLSv1 | ssl.OP_NO_TLSv1_1  # Optional
	conn = context.wrap_socket(sock, server_name=HOST)
	try:
		conn.connect((HOST, PORT))
		handle(con)
	finally:
		conn.close()
		
if __name__ == '__main__':
	main()
```

As a server, same kind of stuff apply but you also need to set the `Ciphers` and to keep them up to date? Or just use `Django` which probably does that for you.

## Go further

[Test you website](https://www.ssllabs.com/ssltest/) and investigate `HSTS` and `HPKP`:

- HSTS is HTTP Strict Transport Security. It forces HTTPS at browser level so even the very first transaction is HTTPS, instead of having an insecure call redirected to HTTPS.
- HPKP is HTTP Public Key Pinning. It is a security mechanism which allows HTTPS websites to resist impersonation by attackers using mis-issued or otherwise fraudulent certificates.