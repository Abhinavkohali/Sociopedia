BabaSecurity Docs 

Access the BabaSecurity dashboard online: https://baba-frontend.vercel.app/

Running the Backend Locally
Using Docker:
1.	Pull the backend Docker image: 
docker pull praatikzz/babasecurity:backend 
2.	Run the backend on port 3000:
      docker run -p 3000:3000 --name babasecuritybackend praatikzz/babasecurity:backend

From Github :
1.	Clone the backend repository:
git clone https://github.com/pratikanand13/Babasecuritybackend.git
2.	Install the necessary dependencies:  
npm i
3.	Run the backend server:
npm run dev 

Running the Frontend Locally
1.  Clone the frontend repository:
	git clone https://github.com/Ravi022/Baba_Frontend
2.  Install the necessary dependencies:
	npm i
3.  Run the frontend server:
	npm run dev

BabaSecurity Dashboard Routes
POST /user/login


Data : 
   

POST /user/signup}
Data:   
 

GET /apiDisocver
GET /apilinks  
GET /bearer
POST /nuclei
Data :
 

POST /thirdpartySast
Data:
 
API Inventory Management 
Overview 
The API Inventory Management system is designed to automatically discover and inventory all 
APIs within an organization. This system is seamlessly integrated into the Software Development Life Cycle (SDLC), providing continuous updates and real-time monitoring. The security team is alerted immediately whenever new APIs are added to the SDLC. 
 
Features: 
•	Automatic API Discovery: Continuously scans for new APIs using server logs and web crawlers. 
•	Real-Time Monitoring: Provides instant alerts for any newly discovered APIs. 
•	Integration into SDLC: Ensures that the API inventory is up-to-date at every stage of the development process. 
Tools and Components 
1. Server Log Analysis 
To discover new API endpoints, our system leverages access to enterprise server logs. A Python script is utilized to analyze these logs, extracting relevant data about new endpoints and other critical metrics. 
How it works: 
•	The script continuously monitors the server logs. 
•	It identifies new API endpoints based on patterns and records them in the inventory. 
•	It provides detailed metrics, including response times and error rates. 
Note: Ensure the necessary permissions are in place to access and analyze server logs. 
2. Web Crawler - 404 Crawler 
In addition to log analysis, we employ the 404 Crawler to identify APIs by crawling the web application and recording any endpoints that return a 404 error. This helps in discovering hidden or undocumented APIs. 
Installation: 
To install the 404 Crawler, follow these steps: 
1.	Ensure that Node.js and npm are installed on your machine. 
	o 	To install Node.js and npm, visit the official documentation. 
 
2.	Open a terminal and run the following command to install the 404 Crawler globally: 
       npm install -g @algolia/404-crawler 
For more information on how to use the 404 Crawler, visit the official GitHub repository. 
 
OWASP Top 10 API Attacks Coverage 
Overview 
The OWASP Top 10 API Attacks Coverage section of our dashboard focuses on implementing protections against the OWASP Top 10 API security risks. This includes both continuous and ondemand scanning options to ensure the security of APIs. To achieve this, we use a combination of Static Application Security Testing (SAST) and Dynamic Application Security Testing (DAST). 
Additionally, automated regression suites with security objectives are integrated to streamline and enhance security testing. 
SAST and DAST Explained 
•	SAST (Static Application Security Testing): 
o	SAST is a white-box testing method that involves scanning the source code for vulnerabilities without executing the application. It allows developers to identify security flaws early in the development process by analyzing data flows and control structures. 
•	DAST (Dynamic Application Security Testing): 
o	DAST is a black-box testing method that involves analyzing an application in its running state. It simulates attacks on the application to identify vulnerabilities such as SQL injection, cross-site scripting, and other security risks. DAST does not require access to the source code. 
Tools and Components 
1. SAST Scanner - Bearer CLI 
For static application security testing, we utilize the Bearer CLI tool. Bearer CLI scans your source code, analyzing data flows to discover, filter, and prioritize security and privacy risks. This helps in identifying vulnerabilities early in the SDLC. 
Installation: 
To install Bearer CLI, follow these steps: 
Quick Install: 
	• 	Run the following command in your terminal to use the install script: 
  curl -sfL https://raw.githubusercontent.com/Bearer/bearer/main/contrib/install.sh | sh 
This will auto-select the best build for your architecture and install the latest version in the ./bin directory. 
For more information on Bearer CLI, visit the official GitHub repository 
 
2. DAST Scanner - VulnAPI 
For dynamic application security testing, we use VulnAPI, an open-source tool designed to scan your APIs for common security vulnerabilities and weaknesses. VulnAPI helps you detect and mitigate vulnerabilities before attackers can exploit them. 
Installation: 
To install VulnAPI on Linux using Snap, run the following command: 
sudo snap install vulnapi 
 
For more details on VulnAPI, visit the official GitHub repository. 
 
3. Automated Regression Suites - Nuclei 
To automate regression suites with security objectives, we use Nuclei. Nuclei sends requests across targets based on templates, leading to zero false positives and providing fast scanning on many hosts. It supports scanning for a wide range of protocols and can be customized to model various security checks. 
Installation: 
To install Nuclei using Docker, run the following command: 
Docker pull projectdiscovery/nuclei:latest 
For more information on Nuclei, visit the official GitHub repository. 
 
Architecture and Design Decisions 
1. Introduction 
This documentation provides a detailed overview of the architectural design and key design decisions behind the Baba Security Dashboard. Built using MongoDB, Express.js, and Node.js, this tool is intended to help manage and monitor security vulnerabilities within an enterprise. It encompasses functionality for storing security scan results, managing user authentication, and offering a comprehensive dashboard for API security. 
2. Schema Design 
2.1 Record Schema 
•	Purpose: To store essential details about security vulnerabilities identified in APIs. 
•	Fields: 
o	apiName: The name of the API where the vulnerability was detected. o 	name: The title or description of the vulnerability. o 	tag: An optional field for additional categorization. 
o	severity: The severity level of the identified vulnerability. 
2.2 Scan Result Schema 
•	Purpose: To record detailed scan results associated with a specific organization. 
•	Fields: 
o	organisationId: A reference to the Dashboard schema to maintain relational integrity. o 	githubOrgName: The name of the GitHub organization associated with the scan. o 	githubLink: The URL to the relevant GitHub repository. 
o	Severity Arrays (CRITICAL, HIGH, MEDIUM, LOW): Arrays to classify and list vulnerabilities based on their severity. 
2.3 Dashboard Schema 
•	Purpose: To manage user authentication and store user-related information for dashboard access. 
•	Fields: 
o	Personal and Organization Information: Includes fields such as name, email, password, organization name, etc. 
o	tokens: An array of authentication tokens to maintain secure sessions. 
•	Security Features: 
o	Password Hashing: Passwords are hashed using bcryptjs to enhance security. o 	JWT Tokens: JSON Web Tokens (JWT) are used for secure session management. 
 
2.4 API Store Schema 
•	Purpose: To serve as a central repository for storing and retrieving API details linked with identified vulnerabilities. 
•	Fields: 
o	apiName: A list of APIs associated with the stored records. o 	records: An embedded document structure to store related vulnerabilities. 
o	organisationId: A link to the Dashboard schema to maintain relational integrity. 
 
 
3. Architectural Design 
3.1 Middleware Integration 
•	Middleware Components: 
o	auth: Handles user authentication to secure API endpoints. 
o	vulnapi, modifyTxt, webCrawling: Perform specific tasks such as vulnerability assessments, text modifications, and data collection via web crawling. 
o	logRequest: Logs all incoming requests to monitor API usage and identify potential security breaches. 
•	Utility Functions: 
o	clearDir: Cleans up directories after analysis to prevent the retention of data that could be exploited. 
o	extract: Utility for extracting specific data points from larger datasets. 
3.2 Routing and API Endpoints 
•	User Management: 
o	Endpoints are provided for user registration, login, update, deletion, and session management, ensuring a secure and seamless user experience. 
•	Security Scan Management: 
o	Endpoints like testapi, apiDiscovery, apilinks, bearer, nuclei, and thirdpartySast are used to manage different aspects of security testing and result management. 
•	Data Processing: 
o	The tool captures standard output from security tools, parses it, and stores it effectively within MongoDB. 
4. Security Measures 
The tool implements several security measures to ensure data integrity and confidentiality: 
•	Authentication and Password Security: The use of JWT for authentication and bcrypt for password hashing ensures that user data remains secure. 
•	Regular Updates: Middleware and dependencies are regularly updated to mitigate vulnerabilities arising from third-party libraries. 
5. Conclusion 
The Baba security dashboard integrates various technologies to deliver a robust solution for managing and assessing security vulnerabilities. Its modular architecture supports scalability and adaptability to emerging security challenges. The use of MongoDB allows for a flexible schema design, making it well-suited for handling the dynamic nature of security data. This documentation covers the critical components and design decisions, ensuring that the tool remains maintainable and extensible. 
 
