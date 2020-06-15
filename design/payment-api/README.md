# Payment API
This is a generic API for supporting online payment.
The scope of this API is limitted (for the moment to Mobile payment).
The operation supported by the API:
- Transfert: Transfer payment to a customer
- Status: Return the status of a transaction
- Verify: Verify the identify of a customer


## API Operations
## Verify
This command verify the status of a customer. Its can be used to validate a phone number.
```
POST /v1/payment/verify

```
##### Request Body
```json
{
   "customer": {
     "name": "Roger Milla",      // Customer full name
     "number": "+2379999999",    // Mobile number in internation format
     "provider": "mtn"           // MTN, Orange
   }
}
```

##### Successfull Response
Status Code: 200

##### Error
| Status Code | Error Code | Description |
|-------------|------------|-------------|
| 404         | customer_not_found | Customer not found |

## Transfer
This is the command for transfering fund to a given customer.

```
POST /v1/payment/transfer
```

##### Request Body
```json
{
   "meta": {
     "invoiceId": "1234",        // ID associated with this transaction
     "description": "..."        // Description of the transaction
   },
   "customer": {
     "name": "Roger Milla",      // Customer full name
     "number": "+2379999999",    // Mobile number in internation format
     "provider": "mtn"           // MTN, Orange
   },
   "amount":{
     "amount": 130000,           // Transfer amount
     "currency": "XAF"           // ISO currency code
   }
}
```

##### Response Body
```
{
   "transactionId": "1234",       // Transaction unique ID
   "status": "success"            // Status of the transaction: pending|failed
}
```

## Status
```
GET /v1/payment/transfer/<transaction-id>
```

##### Response Body
```
{
   "transactionId": "1234",
   "status": "approved"
}
```

## API Errors