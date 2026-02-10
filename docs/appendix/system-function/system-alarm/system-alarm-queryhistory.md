# System.Alarm.queryHistory

## Description
Query the historical alarms of the current historical storage.

## Grammar
```typescript
System.Alarm.queryHistory(historyStorage:string): Promise<any>
System.Alarm.queryHistory(historyStorage:string,params:{
startTime?: Date | string,
endTime?: Date | string,
priority?: AssetAlarmPriority | AssetAlarmPriority[],
state?: AssetAlarmState | AssetAlarmState[],
path?: string | string[],
type?: AssetAlarmType | AssetAlarmType[],
asset?: string | string[],
expression?: string}): Promise<any>
Parameter
      historyStorage - Name of the history storage
      params  - The query conditions object, optional parameters
      {
           startTime? - Start time, default is 8 hours before the current time
           endTime? - End time, default is the current time
           priority? -  Priority(s), optional values are “Low”,“Medium”,“High”,“Critical”
           state? - State(s), optional values are “Active”,“Unacked”,“Acked”,“Cleared”
           path? - Alarm path(s)
           type? - Type(s), optional values are "H","H2","H3","H4","L","L2","L3","L4","RateOfChange","Equivalent","TrueToFalse","FalseToTrue"
           asset? - Asset(s)
           expression? - Expression, Example1:priority == "Low", Example2:path.Contains("Device"), Example3:state.HasFlag("Active") &&       
                                  stae.HasFlag("“Unacked")         
      }
Return
[
         {
            path: string // Alarm path
            name: string // Alarm name
            type: string // Type
            priority: string // Priority
            eventId: string // State change ID
            eventTime: string // State change time
            state: string // State
            operator: string // Acknowledgment operator
            valueType: string // Value type
            value: string // Alarm value
            ackTime: string  // Acknowledgment time
            ackNotes: string // Acknowledgment notes
            ackMode: string // Acknowledgment mode
            nodeName: string // Node name
            storageName: string // History storage name
            description: string // Description
           },
          ...
]

```

## Code Example                                                                                                                                                                                                                                                                                                          
Query the historical alarms from the "Default" historical storage for the past 8 hours. 
```typescript 
const value = await System.Alarm.queryHistory("Default");
console.log(value);
```   
Query the historical alarms from the "Default" historical storage within the time range from 2025-03-10 00:00:00 to 2025-03-11 00:00:00, with an alarm level of High, a type of H or H2, and a status of "Active, Unacked".
```typescript
const value = await System.Alarm.queryHistory("Default",{startTime:'2025-03-10 00:00:00',endTime:'2025-03-11 00:00:00',priority:"High",type:["H","H2"],expression:'state.HasFlag("Active") && state.HasFlag("Unacked")'});
console.log(value);
``` 

