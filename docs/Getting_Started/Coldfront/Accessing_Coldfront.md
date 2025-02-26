# Access to ColdFront

**ColdFront** is a resource and allocation management system designed to provide a central portal for administration, reporting, and measuring scientific impact of cyberinfrastructure resources.

Using ColdFront we enable self-service for project teams. PI’s or project owners can check the current state of projects and apply for new projects or allocations (storage, compute). 

Project owners can change to role of members or add and remove project and allocation members and therefore grant access to the allocated storage and compute resources.

## Instructions

### Connecting from within the AgResearch network:

1. Open your web browser and navigate to [https://coldfront.eri.agresearch.co.nz/user/login](https://coldfront.eri.agresearch.co.nz/user/login)
2. Accept the certificate and authenticate using Microsoft Entra ID.
3. After the authentication with the proxy, we have to authenticate one more time.
4. Authenticate using the option “Log in via AgResearch Account”
><center>
>
>![alt text](../../assets/images/cf_login.png)
></center>
><center>Log in using Microsoft Entra ID</center>
5. List all your existing projects [https://coldfront.eri.agresearch.co.nz/project/](https://coldfront.eri.agresearch.co.nz/project/) or select “Add a project” to request a new one.

!!! **Note:** 
    only enabled users can log in at this stage! Your username and email address must be available to ColdFront to map to your login session.

### Connecting from outside the AgResearch network:

Utilise the Azure application proxy and authenticate using your AgResearch account in order to be able to load the ColdFront application web interface.

When connecting from the outside, the authentication dialog has to be completed twice. Once for the proxy connection and then again for logging in to the ColdFront application.

!!! **Related Articles:**
    - [How do I request resources?](How_do_I_request_resources.md)

    - [How do I check my allocations?](How_do_I_check_my_allocations.md)
    
    - [How do I add a user?](How_do_I_add_a_user.md)
