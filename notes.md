# DevSecOps

- Integration of security practices into DevOps software delivery model
- Security practices are integrated as early as possible into the software development

## 1. Vulnerabilities

- The average cost of a data breach was $3.86 Million in 2020

### Concepts

- Vulnerability: software code flaw, system misconfiguration that hackers can use to gain unauthorized access to a system or network
- Exploit: the method hackers use to exploit a vulnerability
- Threat: the actual/hypothetical exploit attempt on a vulnerability

### Types of vulnerabilities

- OWASP
- CWE
- Broken Access Control: hacker "hijacks" the system and gains control to portions of the application that it shouldn't have

1. Porous defenses

- One weakness that can be used to bypass or spoof authentication and authorization processes
  - Authentication: verifies identity
  - Authorization: verifies the level of access/permissions

2. Risky Resource Management
3. Insecure interaction between components

- Many applications today send and receive data across a wide range of services, threads, and processes
- The way they interact with each other can introduce vulnerabilities

## 2. DevOps vs. DevSecOps

![alt text](image-1.png)

- Set of practices that combine software development (dev) and IT operations (ops)
- Continuous delivery with high-software availability
- In DevSecOps, security is implemented on the different nodes of the CI/CD pipeline

![alt text](image.png)

- On an average software project, only 10-20% is custom code. We have, under the hood, thousands of libraries written
- Libraries and frameworks that you important can, themselves, import other libraries and frameworks
- Beyond libraries, we have containers, which are written with a bunch of packages inherited from public sources

## 3. Exploiting common vulnerabilities

### Intercepting HTTP Request and Injecting SQL

1. Download Burp Suite: https://portswigger.net/burp/releases/professional-community-2025-4-4
2. Spin up the browser inside Burp Suite
3. Intercept HTTP requests
4. Modify the request:

```json
// change to json -> we will inject SQL here
Content-Type: application/json
Accept: application/json, */*;q=0.5

// injecting sql
{
"username":"admin@snyk.io",
	"password": {"$gt": ""}
 }
```

5. Then forward the request

### Using CURL

- CURL: Command-line utility for transferring data to or from a server
  ![alt text](image-2.png)

- Logging and getting the credentials

```bash
curl -X "POST" --cookie c.txt --cookie-jar c.txt -H 'Content-Type: application/json' --data-binary '{"username":"admin@snyk.io", "password":"SuperSecretPassword"}' 'http://localhost:3001/login'
```
