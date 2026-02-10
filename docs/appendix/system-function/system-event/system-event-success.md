# System.Event.success


## Description
Add a successful operation event to the system event, which can be queried in real-time event control or historical event control.

## Grammar
System.Event.success(message:string,...args: any): Promise<void> 

     - Parameter 

        message - Description of the successful event 

        args - Detail of the successful event 

     - Return 

        Nothing

## Code Example                                                                                                                                                                                                                                                                                                          
Add a successful operation event.
```typescript 
// Add operation event description.
await System.Event.success('Lights turned off on schedule successfully.');

// Add operation event description and details.
await System.Event.success('Lights turned off on schedule successfully.', ['Meeting Room', 'Office Area', 'Reception']);


```   
