# 🌐 Webserv

### 42 Project - HTTP Server in C++

---

## 🧠 Overview

**Webserv** is a project from **42 School** that aims to implement a fully functional **HTTP server** in **C++98**, capable of serving static and dynamic web content.

The goal is to reproduce the behavior of a real web server like **nginx** or **Apache**, while deepening understanding of **sockets**, **HTTP protocols**, **CGI**, and **I/O multiplexing** (using `poll()`).

---

## 🚀 Features

- Fully compliant with **HTTP/1.1** specifications.  
- Supports multiple **server blocks** and **virtual hosts**.  
- **Non-blocking I/O** using `poll()` for efficient handling of multiple clients.  
- Handles:
  - `GET`, `POST`, and `DELETE` requests.
  - **Static file serving**.
  - **Directory listing (autoindex)**.
  - **CGI scripts** (e.g., PHP or Python).
- Custom **error pages** per server configuration.
- **Configuration file** parser (`.conf` format, nginx-like syntax).
- Robust **request/response parsing** and **chunked transfer encoding**.

---

## 🧩 Technologies Used

| Component | Description |
|------------|-------------|
| **Language** | C++98 |
| **Networking** | POSIX sockets |
| **I/O Multiplexing** | `poll()` |
| **Configuration** | Custom parser for `.conf` files |
| **CGI Handling** | Environment setup + process fork/exec |
| **Testing** | Using web browsers, `curl`, and `ab` (Apache Benchmark) |

---

## ⚙️ Usage

### 🧱 Compilation
```bash
make
```
## ▶️ Run the Server
```bash
./webserv conf/beast.conf
```
###Then open your browser and go to :
```bash
http://localhost:8090/
```
### 🧾 Example Configuration
```bash $cat config.conf
server {
    listen 8080;
    server_name localhost;

    root ./www;

    location / {
        index index.html;
        autoindex on;
    }

    location /cgi-bin/ {
        cgi_pass ./cgi-bin/;
    }

    error_page 404 /errors/404.html;
}
```

##🌍Test Website Preview
##![🌍Test Website Preview](site/resources/images/webserv.png)

##🧪 Testing

You can test your webserver with:
```bash
curl -v http://localhost:8080/
curl -X POST -d "data=test" http://localhost:8080/cgi-bin/form.py
ab -n 1000 -c 50 http://localhost:8080/
```
