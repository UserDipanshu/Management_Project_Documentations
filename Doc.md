# Project Title: IoT Devices Manager

## 1. Introduction

- **Overview**:
  The IoT Devices Manager is a web-based application designed to manage and monitor IoT devices manufactured and sold by the firm. It serves as an administrative panel for maintaining records and permissions associated with dispatched devices. The primary functionalities include device management, user authorization, and remote interaction with IoT devices.

- **Key Features**:
  1. **Device Inventory Management**:
     - View and track all dispatched IoT devices, including device details (e.g., serial number, firmware version, location), without the direct involvement of the Firm.

  2. **User Authorization and Permissions**:
     - Assign specific authorities and permissions to end users based on their roles and responsibilities.
     - Control access levels for device interactions and settings based on user permissions.

  3. **Remote Device Interaction**:
     - Retrieve real-time parameters and data from IoT devices.
     - Monitor device statuses and health remotely.

  4. **Device Lifecycle Management**:
     - Track the lifecycle of devices from dispatch to decommissioning.
     - Manage device statuses (e.g., active, inactive, under maintenance).

  5. **Customizable Dashboard**:
     - Provide a customizable dashboard for users to monitor key device metrics and statuses.
     - Support visualization of device data through charts, graphs, and tables.


## 2. Architecture

- **System Components**:
  - Frontend (UI)
  - Backend (API server)
  - Database
  - IoT Device Communication Layer

- **Communication Protocols**:
  - MQTT for device communication

- **Technology Stack**:
  - Frontend: React.js
  - Backend: Node.js with Express
  - Database: MongoDB

### 3. Project Workflow

- **User Flows**:
  - Details the different user workflows, such as Registration and Login, Device Management, and Data Visualization. (yet to document)

- **Device Distribution Workflow**:
  1. **Device Storage and Dispatch**:
     - Devices are stored in the firm's store without specific device-to-customer tracking.
     - Upon receiving an order, devices are randomly dispatched from the store to customers or middlemen.

  2. **Device Registration and Ownership**:
     - When a user (customer or middleman) opens and logs into the management app, they register the device they possess.
     - Registration in the app assigns device ownership, reflecting in the firm's database.

  3. **Device Distribution Scenarios**:
     a. **Direct Sale to End User**:
        - The end customer interacts with the device using a separate user application.
        - Initially, the user has read-only access to device parameters and information.
        - To gain control or modify settings, the user contacts the device's admin (first middle vendor) for access.
     
     b. **Sale to Another Middleman**:
        - If a middleman sells to another middleman (e.g., Middleman 1 to Middleman 2), Middleman 2 must register the device.
        - The original admin (Middleman 1) retains control over the device.
        - Middleman 2 requests privileges from Middleman 1 to gain administrative access.

  4. **Authentication and Authorization**:
     - **Device Identification (DeviceId)**:
       - Each device has a unique DeviceId crucial for registration and device interaction.
       - End customers require this DeviceId to connect to and interact with the device via the IoT interface web app.

     - **End Customer Authentication Process**:
       - End customers register on the IoT interface web app.
       - To access a device, customers enter the DeviceId associated with that device.
       - Before gaining access, customers must request registration approval from the device's admin.
       - The admin (device owner) approves or denies access requests to maintain device privacy.
       - Admins can revoke access to users as needed to protect device information.

     - **Enhancing Authentication**:
       - **Adding Verification Layer**:
         - To prevent unauthorized access, a verification layer is implemented.
         - Users' registration requests must be approved by the device's admin before accessing the IoT interface.
         - This ensures that only authorized users can view and interact with specific devices, maintaining privacy and security.


- **Detailed Workflow**:
  The workflow of device distribution within our IoT Devices Manager application begins with the firm storing devices in their store without specific device-to-customer tracking. When an order is received, devices are randomly dispatched from the store to customers or middlemen. This random distribution ensures flexibility and avoids the need for meticulous tracking at the point of dispatch.

  To manage device ownership and tracking effectively, we utilize a unique analogy. When a user receives a device and logs into our management app to register it, they become the designated admin for that device. This registration process not only establishes ownership but also informs us as the firm (super admin) through a shared database and tables. However, there's a potential flaw in this approach: any individual who gains access to a device could potentially register it and assume admin privileges. We recognize the need to refine this logic to ensure more controlled device ownership and registration.

  Now, let's consider what happens when a device reaches the first middleman. Upon receiving the device, the first middleman registers it in our portal, effectively assuming ownership of the device within our system. Since our devices are IoT-enabled with built-in SIM cards, we perform KYC (Know Your Customer) on the SIM during registration to associate the device with the middleman. Despite the registration process, we acknowledge the aforementioned flaw and plan to implement measures to mitigate unauthorized registrations.

  After registration, there are two primary scenarios for the device's journey with the first middleman:

  Direct Sale to End User:
  If the first middleman sells the device directly to an end user, the end user can access our separate user application to interact with the IoT device. Initially, the user has read-only access, enabling them to view device parameters and data. To gain control or modify settings, the user must contact the device's admin (first middleman) for necessary access permissions.
  Sale to Another Middleman:
  Alternatively, if the first middleman sells the device to another middleman (Middleman 2), Middleman 2 also needs to register the device in our portal. However, the original admin (Middleman 1) retains control over the device. Middleman 2 must request administrative privileges from Middleman 1 to access and manage the device further.
  Moving on to authentication and authorization at the end-user level, we employ a unique approach to secure device interactions. Each device is identified by a DeviceId, prominently displayed as a QR code and sticker on the device itself. To interact with a device via our IoT interface web app, end customers register on the platform and provide the DeviceId associated with their device.

  However, to prevent unauthorized access and ensure device privacy, we've implemented a verification layer. When a customer requests device access, their registration request goes to the device's admin for approval. Only after the admin approves the request can the customer log in to the IoT interface web app and interact with the specific device. Admins also have the ability to revoke access to maintain privacy and security over device interactions.





















<!-- 







- **API Documentation**:
  - `/api/devices`: Endpoint to manage devices
  - `/api/data`: Endpoint to retrieve device data

## 4. Project Setup

- **Prerequisites**:
  - Node.js
  - MongoDB

- **Installation Guide**:
  1. Clone the repository
  2. Install dependencies: `npm install`
  3. Set up environment variables

## 5. Codebase Structure

- **Directory Structure**:
  - `/client`: Frontend code
  - `/server`: Backend code
  - `/docs`: Documentation files

- **Important Files**:
  - `server.js`: Main server file
  - `App.js`: Main frontend component

## 6. Development Guidelines

- **Coding Standards**:
  - Follow ES6 syntax
  - Use meaningful variable names

- **Git Workflow**:
  - Branch naming convention: `feature/feature-name`

## 7. Testing

- **Unit Testing**:
  - Use Jest for frontend testing
  - Use Mocha/Chai for backend testing

- **Integration Testing**:
  - Test API endpoints using Supertest

## 8. Security

- **Authentication**:
  - JWT-based authentication

- **Data Protection**:
  - Use HTTPS for data transmission
  - Encrypt sensitive data in the database

## 9. Deployment

- **Deployment Pipeline**:
  - Automated deployment using CI/CD (e.g., GitHub Actions)

- **Environment Variables**:
  - Store sensitive data in environment variables

## 10. Maintenance

- **Logging and Monitoring**:
  - Use Winston for logging
  - Monitor server health using Prometheus/Grafana

- **Routine Maintenance**:
  - Regular backups of the database
  - Scheduled maintenance for updates

## 11. Future Enhancements

- **Feature Roadmap**:
  - Implement real-tim -->
