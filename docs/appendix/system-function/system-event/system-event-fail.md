
# System.Event.fail


## Description
Add a failed operation event to the system event, which can be queried in the real-time event control or historical event control.

## Grammar

System.Event.fail(message:string,...args: any): Promise<void> 

     - Parameter 

        message - Description of the failed event 

        args - Details of the failed event 

     - Return 

Nothing

## Code Example   

Add a failed operation event.
```typescript 

// Add operation event description.
await System.Event.success('Failed to turn off the lights on schedule.');

// Add operation event description and details.
await System.Event.success('Failed to turn off the lights on schedule.', ['Meeting Room', 'Office Area', 'Reception']);

```  
