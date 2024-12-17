# **Binder Service Interaction Flow Documentation**

## **Overview**

This documentation describes the interactions between the **Client Application** and the **Veno Application** through the **Binder Service** for three distinct actions: **Biometric Creation**, **Biometric Update**, and **Authentication**. The client app communicates with the Veno app through the Binder Service, which processes requests, validates data, and returns appropriate responses. Each action involves opening different activities and navigating through various screens.

---

## **1\. User Creation (Button Press 1\)**

### **Step 1: Client Interaction**

* The user presses the **"Create Biometry"** button in the client application.  
* This triggers a request to the Binder Service to create a new pseudonym if not provided.

### **Step 2: Request to Veno**

* The client sends a request to the Binder Service with necessary input parameters for creating a new pseudonym(e.g., user information and application version and some metadata fields).  
* The Binder Service generates a **pseudonym** for the new user.

### **Step 3: Response Handling**

* The Binder Service invokes a **callback** to send the generated pseudonym back to the client application.  
* The client app receives the pseudonym and prepares to process the next step.

### **Step 4: Opening Veno Activity**

* The client launches an activity in the Veno application, passing the **pseudonym** to it.  
* The Veno app uses the pseudonym to process the **create biometric data** workflow.

### **Step 5: Completion of Creation Process**

* After the biometric creation process is completed successfully, the Veno app sends a **response** to the client (success or failure) along with any additional necessary data.

### **Step 6: Client Activity Update**

* The client app displays the response in a new activity, showing the success or failure message along with any relevant data.

  ---

## **2\. Biometric Update (Button Press 2\)**

### **Step 1: Client Interaction**

* The user presses the **"Update Biometry"** button in the client application.  
* The client app collects the **pseudonym** and sends a request to the Binder Service to update the biometric data for the specified user.

### **Step 2: Request to Veno**

* The Binder Service method receives the **pseudonym** and checks if the pseudonym corresponds to an existing user in the Veno database.  
  * If no user is found associated with the pseudonym, the Binder Service responds with a **"User Not Found"** message (false).  
  * If the pseudonym is valid, the Binder Service responds with a **"User Found"** message (true).

### **Step 3: Response Handling**

* The client receives the response:  
  * If the pseudonym is valid (true), the client app proceeds to open the **update biometric data** activity in the Veno application.  
  * If the pseudonym is not valid (false), the client app shows a message indicating that the user was not found.

### **Step 4: Opening Veno Activity**

* The Veno app opens its activity for **updating biometric data**, where the user can provide new biometric details.

### **Step 5: Completion of Update Process**

* Once the update is complete, the Veno app sends a **response** back to the client, indicating whether the biometric update was successful or failed, along with any relevant information.

### **Step 6: Client Activity Update**

* The client app receives the response and opens a new activity to display the success or failure message from the Veno, along with any additional data.

  ---

## **3\. Authentication (Button Press 3\)**

### **Step 1: Client Interaction**

* The user presses the **"Authenticate User"** button in the client application.  
* The client app sends a request to the Binder Service to authenticate the user, providing the **pseudonym** and any additional required information (e.g., biometric data).

### **Step 2: Request to Veno**

* The Binder Service method receives the **pseudonym** and validates the authenticity of the user by matching the pseudonym and biometric data (or other required authentication information) against the stored records in the Veno.

### **Step 3: Response Handling**

* The Binder Service checks if the **pseudonym** and provided biometric data match the stored data:  
  * If the authentication is successful (true), the Binder Service sends a **"Authentication Successful"** response.  
  * If the authentication fails (false), the Binder Service sends a **"Authentication Failed"** response.

### **Step 4: Opening Veno Activity (Authentication Process)**

* If the authentication is successful, the Veno app opens an activity to process any follow-up actions for an authenticated user (e.g., granting access, displaying user information).  
* If the authentication fails, the Veno app may prompt the user to retry or provide an error message.

### **Step 5: Client Activity Update**

* Once the authentication response is received, the client app opens a new activity to display:  
  * **Success**: A message indicating successful authentication, along with any relevant data.  
  * **Failure**: A message indicating failure, with an error explanation.  
    ---

## **Architecture**

### **1\. Key Components**

* **Binder Service**:  
  * Acts as the communication bridge between the client and Veno.  
  * Processes requests and calls the associated callback methods to provide responses back to the client.  
* **Client Application**:  
  * Initiates service requests and displays the responses in activity depending on the action (user creation, biometric update, or authentication).  
* **Veno Application**:  
  * Handles the logic for generating pseudonyms, processing biometric data, validating authentication requests, and returning responses to the client app.  
    

