# abc
KESHAV MEMORIAL INSTITUTE OF TECHNOLOGY
(AN AUTONOMOUS INSTITUTE)
Accredited by NBA & NAAC, Approved by AICTE, Affiliated to JNTUH, Hyderabad
A.Y 2025-2026
Department of Computer Science & Engineering (DS)

Lab Internal I - Software Engineering
Subject Code: 23CC501PC
Year/Sem: III/I
Branch/Section: CSD-B
Faculty: Y Deepthi
Lab Internal: 10/09/2025

SET-1

---

Part I – Software Requirement Specification (SRS) \[10 Marks]

1. Purpose / Abstract:
   Question: Write a detailed purpose and abstract for an Online Food Ordering System (OFOS) that explains why the system is needed, what problems it solves, and the benefits to customers and restaurant staff.
   Answer: The purpose of the Online Food Ordering System (OFOS) is to automate and streamline the process of browsing menus, placing food orders, making payments, and tracking deliveries in a restaurant environment. It addresses common problems like manual order errors, delayed deliveries, lack of payment options, and inefficient order management. The system benefits customers by providing convenience, faster ordering, multiple payment options, and real-time order status updates. For restaurant staff, it simplifies order handling, reduces errors, and improves delivery management.

2. Functional Requirements:
   Question: List and explain the key functional features the OFOS should include to solve common restaurant and customer problems.
   Answer:

* Menu browsing: Customers can view detailed menu items with images, descriptions, and prices.
* Food ordering: Users can add items to a cart, modify quantities, and place orders.
* Online payments: Secure integration with payment gateways for credit/debit cards and wallets.
* Order status tracking: Real-time updates on order preparation, dispatch, and delivery.
* User account management: Profile management, order history, and favorite items.

3. Non-Functional Requirements:
   Question: Describe how the system should behave in terms of performance, security, usability, scalability, and availability.
   Answer:

* Usability: Intuitive and user-friendly interface for all users.
* Performance: Fast response times even with hundreds of concurrent users.
* Security: Secure login, encrypted payments, role-based access for staff and admins.
* Scalability: Capable of handling increasing number of users and orders.
* Availability: High uptime to ensure system accessibility 24/7.

4. Users and Interaction:
   Question: Identify all types of users and explain their interaction with the system.
   Answer:

* Customer: Browses menu, places orders, makes payments, and tracks delivery.
* Restaurant Staff: Updates menu items, manages incoming orders, and tracks delivery.
* Admin: Oversees system configuration, user management, and monitors performance.

5. Modules:
   Question: Break the OFOS into logical modules and explain each module's function.
   Answer:

* Menu Module: Handles creation, update, and display of menu items.
* Order Module: Manages order placement, cart functionality, and order tracking.
* Payment Module: Processes payments securely through integrated gateways.
* Delivery Tracking Module: Monitors the status and location of orders.
* User Management Module: Manages customer and staff accounts and permissions.

---

Part II – Maven Web Application Development \[25 Marks]

1. Fix pom.xml dependency errors:
   Question: The project fails to build due to missing or incorrect dependencies. How would you fix the pom.xml?
   Answer: Ensure all required <dependencies> are listed correctly, <packaging> is set to war, and Maven compiler plugin is configured for Java 17.

2. Update Maven configuration for Java 17:
   Question: How do you update a Maven project that runs on Java 8 to Java 17?
   Answer: In pom.xml, set:
   \<maven.compiler.source>17\</maven.compiler.source>
   \<maven.compiler.target>17\</maven.compiler.target>

3. Force Maven to update dependencies:
   Question: Your local Maven cache has old versions. How do you force Maven to update dependencies?
   Answer: Run command: mvn clean install -U

4. Skip tests during Maven build:
   Question: Tests take too long. How can you skip them?
   Answer: Command: mvn clean package -DskipTests
   Or set in pom.xml: <skipTests>true</skipTests>

5. Resolve dependency conflict:
   Question: Maven shows conflicting versions. How do you resolve it?
   Answer: Use <dependencyManagement> to specify versions or exclude duplicates using <exclusions>.

6. Add JSTL support for JSP pages:
   Question: Which Maven dependency adds JSTL support?
   Answer:

   <dependency>

<groupId>javax.servlet</groupId> <artifactId>jstl</artifactId> <version>1.2</version> </dependency>

---

Part III – Git & GitHub Integration \[15 Marks]

1. Initialize Git repo and push to GitHub:
   Question: The project is not under version control. How do you start using Git and push to GitHub?
   Answer:

* git init
* git add .
* git commit -m "Initial commit"
* git remote add origin <repo-URL>
* git push -u origin main

2. Fix incorrect commit message:
   Question: You wrote “Added Payement Module” instead of “Added Payment Module”. How to correct it?
   Answer:

* git commit --amend -m "Added Payment Module"

3. Check modified files:
   Question: How to see uncommitted changes?
   Answer: git status

4. View commit history compactly:
   Question: How to quickly see a compact log?
   Answer: git log --oneline

5. Recover deleted file before commit:
   Question: You deleted menu.jsp by mistake. How to restore?
   Answer: git checkout -- menu.jsp

6. Clone and switch branch:
   Question: How to clone a teammate’s repo and switch to a branch?
   Answer:

* git clone <repo-url>
* cd <repo-folder>
* git checkout feature-payment

---

Part IV – Git Collaboration, Patch & Merge Conflict \[20 Marks]

1. Create and switch branch:
   Question: You are assigned to add a delivery tracking feature without affecting main code. How?
   Answer: git checkout -b feature/delivery

2. List all branches:
   Question: How to see all local and remote branches?
   Answer: git branch -a

3. Delete local branch safely:
   Question: Wrong branch created. How to delete it?
   Answer: git branch -d feature/delivery

4. Create a patch file:
   Question: Bug in OrderServlet.java. How to create patch?
   Answer: git diff > bugfix.patch

5. Apply a patch:
   Question: Teammate sent a patch. How to apply?
   Answer: git apply bugfix.patch

6. Combine multiple commits:
   Question: How to squash commits before pushing?
   Answer: git rebase -i HEAD\~n (replace n with number of commits)

7. Clone repository:
   Question: How to make a local copy of remote repository?
   Answer: git clone <repo-url>

---

Part V – Dockerization \[15 Marks]

1. Dockerfile to build OFOS:


FROM maven:3.8.7-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

FROM tomcat:9.0
COPY --from=build /app/target/OFOS.war /usr/local/tomcat/webapps/OFOS.war
EXPOSE 8080
CMD ["catalina.sh", "run"]


2. Build and run container:

* docker build -t ofos-app .
* docker run -p 8080:8080 ofos-app
* Access: [http://localhost:8080/OFOS](http://localhost:8080/OFOS)

3. Push image to Docker Hub:

* docker tag ofos-app username/ofos-app\:v1
* docker push username/ofos-app\:v1

---

Part VI – Docker Compose Multi-Container Setup \[15 Marks]

1. docker-compose.yml:


version: '3.8'
services:
  ofos-app:
    image: username/ofos-app:v1
    ports:
      - "8080:8080"
    depends_on:
      - db

  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: ofos_db
      MYSQL_USER: ofos_user
      MYSQL_PASSWORD: ofos_pass
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:


2. Run containers:

* docker-compose up --build

3. Rebuild service after changes:

* docker-compose up --build --force-recreate

4. Verify data persistence:

* Insert orders → restart containers → check data remains in database

5. Stop containers but keep data:

* docker-compose down
