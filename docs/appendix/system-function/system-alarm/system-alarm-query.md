# System.Alarm.query

## Description
Query real-time alarms. 

## Grammar
```typescript
System.Alarm.query(): Promise<any>  
System.Alarm.query(params?:{  
priority?: AlarmPriority | AlarmPriority[],
state?: AlarmState | AlarmState[],
path?: string | string[],
type?:AlarmType | AlarmType[],
asset?: string | string[],
group?: string | string[],
expression?: string}): Promise<any>
- Parameter
  params - The query conditions object, optional parameters
  {
     priority? -  Priority(s), optional values are “Low”,“Medium”,“High”,“Critical”
     state? - State(s), optional values are “Active”,“Unacked”,“Acked”,“Cleared”
     path? - Alarm path(s)
     type? - Type(s), optional values are "H","H2","H3","H4","L","L2","L3","L4","RateOfChange","Equivalent","TrueToFalse","FalseToTrue"
     group? - Alarm group(s)
     asset? - Asset(s)
     expression? - Expression, Example1:priority == "Low", Example2:path.Contains("Device"), Example3:state.HasFlag("Active") && stae.HasFlag("“Unacked")
   } 
- Return
  [
    {
      path: string // Alarm path
      name: string // Alarm name
      type: string // Type
      priority: string // Priority
      eventTime: string // State change time
      state: string // State
      operator: string // Acknowledgment operator
      valueType: string // Value type
      value: string // Alarm value
      ackTime: string  // Acknowledgment time
      ackNotes: string // Acknowledgment notes
      recoveryTime:string // Recovery time  description: string // Description  ackMode: string // Acknowledgment mode
      ruleName: string // Notification Rule  groupNames: string // Alarm group
      activeTime: string // Activation time
    },
      ...
  ] 

```

## Code Example                                                                                                                                                                                                                                                                                                          
Query all real-time alarms.  
```typescript 
const value = await System.Alarm.query();
console.log(value);
```   
Query real-time alarms with an alarm level of High, a type of H or H2, an alarm group of Default, and a status of "Active, Unacked".  
```typescript
const value = await System.Alarm.query({priority:"High",type:["H","H2"],group:'Default',expression:
'state.HasFlag("Active") && state.HasFlag("Unacked")'});
console.log(value);
``` 

