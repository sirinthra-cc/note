# Secure Code Curriculum
- - - -
## Injection
### SQL Injection
**via**: 
**when**: 
**solution**: 

### XXE Injection
**via**: 
**when**: 
**solution**: 

### Command Injection
**via**: url path
**when**: program execute a command using query params
**solution**: validate input 

- - - -
## Broken Authentication And Session Management
### Session Fixation
**via**: login
**when**: เราพยายาม login -> ได้ session id -> ส่ง url นั้นให้คนอื่น login -> เรา refresh -> เรา login ได้แล้ว
**solution**: gen session id ใหม่ทุกครั้ง (session id ก่อนพยายาม login กะหลัง login ต้องเป็นคนละอันกัน)

### Use of Insufficiently Random Values
**via**:  login
**when**: session id could be predicted 
เช่น session_id = old_session_id + 1, time <- random ไม่พอ
**solution**: use secure random (ทำไงก็ได้ให้เดาไม่ได้อ่า)

- - - -
## Cross Site Scripting
### Reflected Xss
**via**: making request
**when**: เรา reveal url เช่น เค้ากด search ละ url กลายเป็น ?search=test -> hacker ลองยิงอย่างอื่นไปที่ url นั้น
**solution**: encode output

### Persistent (Stored) Xss
**via**: display data
**when**: user store xss in data field such as name -> display name -> execute xss
**solution**: escape when display

### DOM Cross Site Scripting
**via**: request
**when**: การ process query param มีช่องโหว่ -> ส่งเมลหลอก user ให้เข้า link แต่ redirect ไปที่อื่น e.g. document.write("Hello " + name + "! Please login or signup to access news stories");
**solution**: defense-in-depth ทำทุกอย่างตั้งแต่ validate input บลาๆ
- Stored XSS and Reflected XSS injection takes place server side
- DOM XSS, the attack is injected into the Browser DOM, this adds additional complexity and makes it very difficult to prevent and highly context specific, because an attacker can inject HTML, HTML Attributes, CSS as well as URLs.

- - - -
## Insecure Direct Object References
### Directory (Path) Traversal
**via**: display content in file using file name as param
**when**: user traverse to outer directory e.g. ?file=../../etc/pwd
**solution**: กันไม่ให้ traverse to outer directory

- - - -
## Security Misconfiguration
### Privileged Interface Exposure
**via**: login
**when**: expose url -> hacker เข้าหน้า login admin ได้
**solution**: *

### Left Over Debug Code
**via**: login
**when**: debug code reveal how to access to the system
**solution**: remove it

- - - -
## Sensitive Data Exposure
### Authentication Credentials In URL
**via**: login
**when**: expose authentication data in url, the URL is saved in multiple locations during request transmission thus the credentials can be stolen
**solution**: Ensure that Session Identifiers are not transmitted to the application via GET request, only via POST requests

### Session Exposure within URL
**via**: login
**when**: expose session in url -> โพสลงเฟส -> มีคนมากด login -> เข้าได้
**solution**: Session ID shouldn't be sent in the URL as the URL may be disclosed in multiple locations. Also, it shouldn't be sent in POST parameter with every request because it may be stolen via XSS. The secure way to send a session ID is a cookie with HttpOnly and Secure flags.

### User Enumeration
**via**: password reset form
**when**: ใส่เมล์มั่วๆละระบบบอกว่าเมล์นี้ไม่มี -> hacker สุ่มจนกว่าจะเจอ user 
**solution**: หลอกว่าส่งเมล์ไปแล้ว

- - - -
## Missing Function Level Access Control
### Horizontal Privilege Escalation
**via**: get user data
**when**: จะ get user data แต่ดันไม่ authorize อีกรอบ -> พอเปลี่ยน id ใน query param ก็เข้าไปดู data คนอื่นได้
**solution**: authorize อีกรอบ -> level of authorization and group

### Vertical Privilege escalation
**via**: get user data
**when**: จะ get user data แต่เข้าผ่าน admin path
**solution**: เช็ค user ไม่พอ ต้องเช็ค role ด้วย

- - - -
## Cross Site Request Forgery
### Cross Site Request Forgery (POST)
**via**: post
**when**: access web อื่น แต่เว็บนั้น post มาเว็บเรา -> พอเราเปิดเว็บนั้น เรา authorized -> เค้า post เว็บเราสำเร็จ
**solution**: Synchronizer Token Pattern - To be effective, each response from the web server requires a Random Token to be generated. This token is then inserted by the application, as a hidden parameter, into sensitive form fields. 

### Cross Site Request Forgery (GET)
**via**: get
**when**: access web อื่น แต่เว็บนั้น post มาเว็บเรา -> พอเราเปิดเว็บนั้น เรา authorized -> เค้า post เว็บเราสำเร็จ (misuse of get)
**solution**: ใช้ get, post, put, delete ให้ถูก

### Click Jacking
**via**: click
**when**: เราเขียนเว็บเราขึ้นมา แต่ content ด้านใน(opa 0)เป็นของเว็บอื่น พอ user กดปุ่มอะไร action จะไปตกที่เว็บนั้น
![](Secure%20Code%20Curriculum/9F7FC6FA-5E3E-401C-A11D-6621384C5C21.png)
**solution**: use X-Frame-Options Headers

- - - -
## Unvalidated Redirects And Forwards
### Insecure URL Redirect
**via**: redirect
**when**: เค้าสร้างหน้าปลอมให้ login ละ redirect จากเว็บเค้ามาเว็บเรา
**solution**: check address before redirect

- - - -
## Extra Modules
### Components With Known Vulnerabilities
**via**: command line
**when**: using old web server -> hacker รู้ช่องโหว่ -> เจาะเข้า server
**solution**: update server bash