# **Configuring Network File Shares and Permissions**

## **Objective**
This lab focuses on setting up file shares with specific permissions and testing user access levels based on security group membership in an Active Directory environment.

---

## **Environments and Technologies Used**
- **Microsoft Azure**: Hosting virtual machines for the lab environment.
- **Active Directory**: Managing users, groups, and folder permissions.
- **Windows Server 2022**: Domain Controller.
- **Windows 10**: Client machine for testing file share access.

---

## **Steps and Details**

### **1. Setting Up File Shares**
1. **Initial Setup**
   - Turn on the **DC-1** and **Client-1** virtual machines in the Azure portal.
   - Log into **DC-1** as `mydomain.com\jane_admin` (Domain Admin).
   - Log into **Client-1** as `<someuser>` (Normal User, which in this case is 'fogiw.cemu').

2. **Creating Folders**
   - On **DC-1**, create the following folders on the `C:\` drive:
     - `read-access`
     - `write-access`
     - `no-access`
     - `accounting`
       ![image](https://github.com/user-attachments/assets/78bdf081-cdcc-433b-928b-abd7500d079b)


3. **Configuring Permissions**
   - **read-access**: Assign `Domain Users` group with `Read` permissions.
     ![image](https://github.com/user-attachments/assets/8828bb51-2a3e-47be-a342-65248d5a8ec9)

   - **write-access**: Assign `Domain Users` group with `Read/Write` permissions.
     ![image](https://github.com/user-attachments/assets/04fa2a0a-1c31-48c0-9dca-acdc21b6b4e8)

   - **no-access**: Assign `Domain Admins` group with `Read/Write` permissions.
     ![image](https://github.com/user-attachments/assets/bd898112-4a20-444d-bed1-0b3959731957)

   - Leave the `accounting` folder for a later step.

4. **Testing Access**
   - From **Client-1**, navigate to the shared folder path (`\\dc-1`) and attempt to access each folder.
      ![image](https://github.com/user-attachments/assets/59ef28c9-bde1-4573-a853-7239acce3780)
   - Document which folders are accessible and whether files can be created in each folder.
     ![image](https://github.com/user-attachments/assets/7ff768ba-2969-48c8-a53e-6e0fee2a8f5a)
     ![image](https://github.com/user-attachments/assets/5a22e971-2722-4221-8e26-2cf4ceaa72fe)
     ![image](https://github.com/user-attachments/assets/65fb824e-7634-422e-b7c0-447f3088e151)
 


---

### **2. Configuring Security Groups and Testing Permissions**
1. **Creating a Security Group**
   - On **DC-1**, open Active Directory and create a new security group named `ACCOUNTANTS`.
     ![image](https://github.com/user-attachments/assets/f31e2b8a-4b49-4cc9-ab53-72331c0d7b84)


2. **Assigning Folder Permissions**
   - Assign `ACCOUNTANTS` group with `Read/Write` permissions for the `accounting` folder.
     ![image](https://github.com/user-attachments/assets/c14df886-63ec-4c36-9f54-1ae18f7c3913)

     

3. **Testing Access for Non-Members**
   - On **Client-1**, log in as `<someuser>` and attempt to access the `accounting` folder.
     _Expected Outcome:_ Access should be denied.
     ![image](https://github.com/user-attachments/assets/874a5cf4-d874-4e1e-b49c-2f896cf04097)


4. **Adding User to Security Group**
   - On **DC-1**, add `<someuser>` to the `ACCOUNTANTS` security group.
     ![image](https://github.com/user-attachments/assets/1ce9d752-9907-41a9-b6ef-c7adaba3afb2)


5. **Testing Access for Group Members**
   - Log back into **Client-1** as `<someuser>` and attempt to access the `accounting` folder again.
     _Expected Outcome:_ Access should now be granted.
     ![image](https://github.com/user-attachments/assets/f0182ee5-8cf0-4ee0-a3f5-03c9ba575f29)


---

### **3. Cleanup**
- Once all steps are complete, you can choose to delete or retain the virtual machines for further practice.

---

## **Conclusion**
In this lab, you learned how to:
- Configure shared folders with specific permissions for user groups.
- Test access levels for users based on their group membership.
- Manage security groups in Active Directory to dynamically assign permissions.

This exercise is critical for managing network file shares and enforcing security policies in an enterprise environment.
