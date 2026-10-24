# **🚀 Dayflow — Daily Task & Progress Tracker Application**
Full-stack Node.js & Express task planner with JWT authentication, bcrypt security, and Azure Cosmos DB cloud integration.

## **💻About the Project**
Dayflow is a responsive, full-stack task planning application built with Node.js, Express.js, Vanilla JavaScript, and MongoDB. It features secure user authentication with bcrypt password hashing and stateless JSON Web Token (JWT) session protection. The application includes server-side pagination, real-time daily completion analytics, streak tracking, and an offline-capable architecture that works seamlessly across desktop, tablet, and mobile devices. It is engineered for production deployment on Microsoft Azure App Service (Linux) with seamless data persistence backed by Azure Cosmos DB for MongoDB.
## **✨ Key Features**

### **🔒 Authentication & Data Isolation**

* **Secure Registration & Sign-In:** User passwords are encrypted and salted using bcrypt hashing.  
* **Stateless Session Protection:** All task and analytics API routes are protected via JSON Web Tokens (JWT).  
* **Multi-Tenant Privacy:** Strict account isolation ensures each user only views and manages their own tasks.

### **📋 Smart Task Management**

* **Full CRUD Operations:** Create, edit, complete, and delete tasks seamlessly.  
* **Date, Category & Priority Planning:** Schedule tasks by target date, assign custom categories, and filter by priority level.  
* **Server-Side Pagination & Search:** Paginated task lists (8 tasks per page) with server-side paging, instant search, and status filters.  
* **Productivity Shortcuts:** Includes a Quick Add bar, keyboard shortcuts (n for new task, / for search), and a one-click "Move overdue to today" action.

### **📊 Progress Analytics & Gamification**

* **Daily Completion Ring:** Live animated SVG progress ring displaying daily completion percentage alongside completed/remaining task counters.  
* **Weekly Overview & All-Time History:** Dedicated progress page featuring 7-day activity bars, daily streaks, and all-time completion metrics.  
* **Micro-Animations:** Tasks slide in smoothly, check off with a pop \+ strike-through \+ confetti burst, glide when reordered, and trigger a full celebration when clearing the day (fully respects prefers-reduced-motion).

## **🔐 Environment Variables**

* **PORT**  
  * **Default / Example:** 5000 (Local) / 8080 (Azure)  
  * **Description:** Port the Express server listens on (process.env.PORT \|\| 5000\)  
* **MONGODB\_URI**  
  * **Default / Example:** mongodb+srv://user:pass@cluster...  
  * **Description:** Full connection string for Azure Cosmos DB or MongoDB Atlas  
* **JWT\_SECRET**  
  * **Default / Example:** 64-char-random-hex-string  
  * **Description:** Secret key used to sign and verify session JWT tokens  
* **NODE\_ENV**  
  * **Default / Example:** development or production  
  * **Description:** Set to production when deployed to Azure App Service

## **🛠️ Tech Stack Layers**

* **Frontend:** HTML5, CSS3, Vanilla JavaScript (ES6+), PWA (Service Worker, Web Manifest)  
* **Backend:** Node.js (v18+ / v20 LTS), Express.js, RESTful API Architecture  
* **Database:** Azure Cosmos DB for MongoDB (vCore / MongoDB 8.0 compatibility), MongoDB Atlas  
* **Authentication:** JSON Web Tokens (jsonwebtoken), bcrypt Password Hashing  
* **Cloud & DevOps:** Microsoft Azure App Service (Linux), Azure Application Insights, Azure Log Stream, VS Code Azure Tools

## **☁️ Step-by-Step Deployment Guide**

### **Step 1: Create the Azure Web App (Cloud Server)**

> 1. **Open App Services in Azure Portal:**  
   * Log in to the Azure Portal and type web app in the top search bar.  
   * Under the **Services** section, click on **App Services**.  
   * Click the **\+ Create** button at the top left and select **Web App**.  
> 2. **Fill the Basics Tab Details:**  
   * **Subscription:** Select Azure for Students.  
   * **Resource Group:** Select your existing dayflow-app-rg (or click **Create new** to make one).  
   * **Name:** Enter a unique name like dayflow-app.  
   * **Publish:** Select Code.  
   * **Runtime stack:** Select Node 20 LTS.  
   * **Operating System:** Select Linux.  
   * **Region:** Select East Asia (this region is allowed by your student subscription policy).  
   * **Pricing plan:** Select the Free or Basic tier.  
> 3. **Review and Create:**  
   * Click the **Review \+ create** tab at the top.  
   * Wait for validation to pass, then click **Create**.  
   * Wait 1–2 minutes until the deployment finishes, then open your **App Services** list to see dayflow-app with Status Running.

![Project Screenshot](/images/AppServices.png)

### **Step 2: Create Azure Cosmos DB (Database)**

> 1. **Create the Database Resource:**  
   * In the top Azure search bar, search for Azure Cosmos DB (or Azure DocumentDB) and click **\+ Create**.  
   * Select **Azure Cosmos DB for MongoDB** (vCore / Native DocumentDB cluster).  
> 2. **Configure Database Basics:**  
   * **Subscription:** Azure for Students.  
   * **Resource Group:** Select the same dayflow-app-rg.  
   * **Cluster Name:** Enter a name (e.g., docdb-cluster-20261017-0042).  
   * **Location:** Select East Asia (keep it in the exact same region as your Web App).  
   * **Cluster Tier:** Select Free tier (32 GiB disk).  
   * **Admin Username:** Enter your admin username (e.g., dbuser6fxh2v).  
   * **Password:** Create a clean password using only letters and numbers (e.g., RahulDayflow2026) so special symbols like @ do not break the URL.  
> 3. **Configure Networking (Firewall):**  
   * Go to the **Networking** tab during setup (or after creation on the left menu).  
   * Enable Public access and check the box to **Allow public access from Azure services and resources within Azure to this cluster** (and add your current client IP).  
   * Click **Review \+ create** and then **Create**. Wait until the database status shows Ready.

![Project Screenshot](/images/CosmosDB.png)

### **Step 3: Get the Database Link & Configure Settings**

> 1. **Copy the Connection String:**  
   * Inside your database Overview page, click the button **List connection strings for this Azure DocumentDB** (or go to Settings \-\> Connection strings on the left menu).  
   * Copy the connection string:mongodb+srv://dbuser6fxh2v:\<password\>@\[docdb-cluster-20261017-0042.global.mongocluster.cosmos.azure.com/?tls=true\&authMechanism=SCRAM-SHA-256\&retrywrites=false\&maxIdleTimeMS=120000\](https\://docdb-cluster-20261017-0042.global.mongocluster.cosmos.azure.com/?tls=true\&authMechanism=SCRAM-SHA-256\&retrywrites=false\&maxIdleTimeMS=120000)  
   * Replace \<password\> (removing the \< and \> brackets) with your clean password:mongodb+srv://dbuser6fxh2v:RahulDayflow2026@docdb-cluster-20261017-0042.global.mongocluster.cosmos.azure.com/?tls=true\&authMechanism=SCRAM-SHA-256\&retrywrites=false\&maxIdleTimeMS=120000  
> 2. **Add the Link to Local Code (.env) & Verify Packages:**  
   * Open your project folder in VS Code.  
   * Open your .env file and paste the modified link into MONGODB\_URI= so your local code matches:  
     Code snippet  
     PORT=5000  
     MONGODB\_URI=mongodb+srv://dbuser6fxh2v:RahulDayflow2026@docdb-cluster-20261017-0042.global.mongocluster.cosmos.azure.com/?tls=true\&authMechanism=SCRAM-SHA-256\&retrywrites=false\&maxIdleTimeMS=120000  
     JWT\_SECRET=your\_long\_random\_secret\_secrete\_is\_here\_do\_what\_you\_want\_with\_it

   * Open the VS Code terminal and run npm install dotenv so dotenv is saved in your package.json.  
> 3. **Add the Link to Azure App Service Environment Variables:**  
   * *(Note: Azure ignores your local .env file for security, so you must also paste the link inside Azure).*  
   * Go to your dayflow-app in the Azure Portal.  
   * On the left menu under **Settings**, click **Environment variables**.  
   * Under the **App settings** tab, click **\+ Add**:  
     * **Name:** MONGODB\_URI  
     * **Value:** Paste your full connection string with the password included.  
     * Click **Apply**.  
   * Click **\+ Add** again:  
     * **Name:** JWT\_SECRET  
     * **Value:** your\_long\_random\_secret\_secrete\_is\_here\_do\_what\_you\_want\_with\_it  
     * Click **Apply**.  
   * Click the blue **Apply** button at the bottom of the page and click **Confirm**.

![Project Screenshot](/images/MONGODB_URI_JWT_SECRET.png)

### **Step 4: Deploy via VS Code & Verify Live App**

> 1. **Connect VS Code to Azure:**  
   * Install the **Azure App Service** extension in VS Code.  
   * Click the Azure icon in the left sidebar of VS Code and sign in with your college email (lengare.rahul-imed@bvp.edu.in).  
> 2. **Deploy the Project:**  
   * Under your Azure for Students subscription, expand **App Services**.  
   * Right-click on dayflow-app and click **Deploy to Web App...**.  
   * Select your Dayflow project folder at the top prompt and click **Deploy**.  
   * Wait 1–2 minutes while VS Code packages your code, uploads it, and installs node\_modules.

![Project Screenshot](/images/VSCodeDeploy.png)

> 3. **Restart and Open Your Live Website:**  
   * Go back to dayflow-app in the Azure Portal, click **Overview**, and click **Restart**.  
   * Open the live URL (\[https\://dayflow-app.azurewebsites.net\](https\://dayflow-app.azurewebsites.net)), log in, and add a sample task on the dashboard.

![Project Screenshot](/images/Website.png)
![Project Screenshot](/images/DeploySecurely.png)

