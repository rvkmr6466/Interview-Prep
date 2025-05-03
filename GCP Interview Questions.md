## GCP Interview Questions

## Q. 
To save a secret key in Google Cloud KMS, you'll first need to create a key ring and a key within that key ring. Then, you can use the key to encrypt your secret and store it in a secure location like Google Cloud Storage or Secret Manager.

Here's a breakdown of the process: 

### 1. Create a Key Ring and Key:  

#### Key Ring: 
A key ring is a container for your encryption keys. It helps organize and manage your keys within your project. You can create a key ring using the Google Cloud Console or the Google Cloud CLI. 
- **Google Cloud Console:** Navigate to the Key Management section, select "Key Rings", and click "Create Key Ring". 
- **Google Cloud CLI:** Use the command `gcloud kms keyrings create <KEY_RING_NAME> --location <LOCATION>`. 

#### Key: 
Once you have a key ring, create a key within it. This key will be used to encrypt your secret. 
- Google Cloud Console: In the Key Management section, select your key ring and click "Add Key". 
- Google Cloud CLI: Use the command `gcloud kms keys create <KEY_NAME> --location <LOCATION> --keyring <KEY_RING> --purpose encryption`.

### 2. Encrypt the Secret:

#### Data Encryption: Use the Cloud KMS key to encrypt your secret data. This can be done using the Google Cloud CLI or the Cloud KMS API.
	- **Google Cloud CLI:** Use the command `gcloud kms encrypt --ciphertext-file <OUTPUT_FILE> --plaintext-file <INPUT_FILE> --keyring <KEY_RING> --key <KEY_NAME> --location <LOCATION>;`.  

#### Store the Encrypted Secret: 
Store the encrypted secret data in a secure location like Google Cloud Storage or Secret Manager.

### 3. Accessing the Secret:

- To access the secret, you'll need to decrypt the encrypted data using the same Cloud KMS key. 
- **Google Cloud Console:** You can access the decrypted secret from Secret Manager or download the encrypted data from Cloud Storage and decrypt it using the CLI.  
- **Google Cloud CLI:** Use the command `gcloud kms decrypt --ciphertext-file <INPUT_FILE> --output-file <OUTPUT_FILE> --keyring <KEY_RING> --key <KEY_NAME> --location <LOCATION>`.

### Important Considerations:
- **Permissions:** Ensure that the service account or user accessing the key has the necessary permissions to encrypt and decrypt data using the Cloud KMS key.
- **Security:** Store the encrypted secret in a secure location like Secret Manager or encrypt it before storing it in Cloud Storage.
- **Key Rotation:** Regularly rotate your Cloud KMS keys to minimize the risk of compromise.

---
## Q. GCP ( cloud run, cloud function)

### **Google Cloud Run**

**Overview**:  
Cloud Run lets you deploy and run containerized applications that scale automatically. It's a serverless compute platform based on containers.

**Key Features**:
- Supports **any language**, framework, or binary as long as it can be containerized.
- Full **HTTP request handling**.
- Scales from zero to thousands of instances.
- Can run **longer processes** (up to 60 minutes).
- More **control over the runtime**, memory, CPU, and concurrency.
- Easily connect to **Cloud SQL**, VPC, or use custom domains.

**Use Cases**:
- Microservices with REST APIs.
- Web applications or backend services.
- Background workers or batch jobs.

---

### ⚡️ **Google Cloud Functions**

**Overview**:  
Cloud Functions is a lightweight, event-driven serverless platform. You deploy small units of code that respond to events.

**Key Features**:
- **No need for containerization**—just write the function code and deploy.
- Triggers from **HTTP, Pub/Sub, Cloud Storage, Firestore**, etc.
- **Auto-scales** instantly depending on load.
- Shorter execution time (max **9 minutes**).
- **Stateless** and ideal for event-driven architecture.

**Use Cases**:
- Real-time file processing (e.g., image resize on upload).
- Responding to Pub/Sub messages.
- Webhooks or lightweight HTTP APIs.
- Automation scripts.

---

### **Comparison Table**

| Feature                | Cloud Run                        | Cloud Functions                  |
|------------------------|----------------------------------|----------------------------------|
| Runtime                | Container-based (any language)   | Code-based (Node.js, Python, etc)|
| Trigger                | HTTP, Pub/Sub, Scheduler, etc.   | HTTP, Pub/Sub, Cloud Events      |
| Concurrency            | Supports concurrent requests     | One request per instance         |
| Max Execution Time     | 60 minutes                       | 9 minutes                        |
| Deployment Model       | Container image                  | Function source code             |
| Use Case               | REST APIs, web apps, workers     | Event-driven, lightweight tasks  |
| VPC & Networking       | Full control available           | Limited                          |
| Custom Domains         | Supported                        | Supported (via HTTP trigger)     |

---

### When to Use What?

- Use **Cloud Run** when:
  - You need full control over the runtime (e.g., custom dependencies, multi-threading).
  - Your app is already containerized.
  - Your tasks need more than 9 minutes.
  - You need concurrency or large-scale APIs.

- Use **Cloud Functions** when:
  - You want to run code quickly in response to an event.
  - Simplicity and quick setup matter.
  - You’re handling lightweight, short-lived logic.

---
## Q. Explain BigQuery.
BigQuery is a service that can be found on the Google Cloud Platform. This service acts as a storage facility for major companies and organizations. This reasonably priced and highly scalable software analyses data in memory and makes use of machine learning to improve the quality of the results.

