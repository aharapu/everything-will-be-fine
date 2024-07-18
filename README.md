# everything-will-be-fine
Transactions, but for promises, not databases.

### why?
because often times in backend endpoints, operations need to be made in sequence. if one of these operations fails, the previous ones would ideally be rolled back.<br>

Most often i see `await` calls to services within the same project (notifications, event logging etc.), calls to microservices or calls to 3rd party integrations. A failure at any point might require some level of rollback on some of those operations.

### the dream
**iPromise*" is a function that takes a callback where or the "transactional style" promises are executed.
<br>

if a promise fails, the previous ones should get their rollback called in reverse order.

some strange example:
```javascript
const recordEvent = new DoOrDie({
  makePromise: async (some, args) => {
    // do some ops
    await someDbOperation()
    // do more stuff
    return {
      successResult: thisGetReturnedByCallingRecordEvent,
      rollback: async () => {
        // make use of closure
        // and use whatever data you need from the initial operation
        // to do your rollback
      }
```

### bonus
this should be fully typed


