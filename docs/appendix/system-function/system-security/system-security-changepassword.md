# System.Security.changePassword


## Description
Change password of the currently logged in user.

## Grammar
System.Security.changePassword(oldPassword:string,newPassword:string): Promise<boolean>

     - Parameter

        oldPassword  Old password 

        newPassword  New password

     - Return

        Whether the password was successfully changed

## Code Example       
Change the password of the currently logged in user from "abc123" to "abc456".
```typescript 
const result = await System.Security.changePassword('abc123','abc456');
console.log(result);

```   
