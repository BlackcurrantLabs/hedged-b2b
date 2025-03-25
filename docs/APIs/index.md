# Hedged B2B

APIs to get details of the recommendations the user is subscribed to.

Please visit the <a href="https://api.core.hedged.in/b2b-swagger/"><button style="unset:all; padding: 0.3rem; border-radius: 5px; background-color:#4051b5; color:white; cursor:pointer;">Swagger Page</button></a> for more details.

To access these APIs you would need api key and api secret which are available on b2b console.

The header should contain two header keys :

api-key

api-secret

## APIs

1. ### GET /me:

   Get your profile with your preferences and account details.
```jsonc
   {
       "id": "number",
       "postbackUrl": "string",
       "type": "string",
       "createdAt": "datetime",
       "updatedAt": "datetime",
       "userId": "number",
       "User": {
           "id": "number",
           "oldUid": "null|string",
           "name": "string",
           "email": "string",
           "emailVerified": "boolean",
           "emailDeliveryActive": "boolean",
           "phone": "string",
           "phoneVerified": "boolean",
           "subscription": "string",
           "subscriptionName": "string",
           "subscriptionStart": "null|datetime",
           "subscriptionExpiry": "null|datetime",
           "lastActiveAt": "datetime",
           "type": "string",
           "isActive": "boolean",
           "isUsingOldPassword": "boolean",
           "tradingExperience": "null|string",
           "city": "null|string",
           "isOnboardingComplete": "boolean",
           "pan": "null|string",
           "isBillingInfoSet": "boolean",
           "lifetimeValue": "number",
           "noOfPurchases": "number",
           "AdminPermission": "object",
           "B2BPermission": {
           },
           "createdAt": "datetime",
           "updatedAt": "datetime",
           "isImpersonationEnabled": "boolean",
           "birthDate": "null|datetime",
           "whatsappPhone": "null|string",
           "isSubscribedToNewsletter": "boolean",
           "gender": "boolean",
           "profilePic": "null|string"
       },
       "B2BRecommendationTargetClasses": [{
               "id": "number",
               "code": "string",
               "name": "string",
               "isDisabled": "boolean",
               "createdAt": "datetime",
               "updatedAt": "datetime",
               "B2BSubscriberPivotTargetClass": {
                   "createdAt": "datetime",
                   "updatedAt": "datetime",
                   "b2BSubscriberId": "number",
                   "b2BRecommendationTargetClassId": "number"
               }
           }
       ]
   }
```

3. ### GET /list_b2b_recommendations:

   Lists all recommendations that you are subscribed to.
   You can optionally send a preference for filtering out your recommendations.
   Available filters: - type:
   Either `EQUITY`,`FNO` and `SIMPLY_HEDGED` based on recommendation type. - bias:
   Either `BEARISH`, `BULLISH` , `NEUTRAL` and `BIDIRECTIONAL` based on recommendation type
   #### Query Parameters
   - **fundType** (optional)
     _Type_: `string`
     _Allowed values_: `EQUITY`, `FNO`, `SIMPLY_HEDGED`
   - **bias** (optional)
     _Type_: `string`
     _Allowed values_: `BEARISH`, `BULLISH`, `NEUTRAL`, `BIDIRECTIONAL`
   - **targetClassCode** (optional)
     _Type_: `string`
     _Description_: Target class code



   ```jsonc
      [
        {
          "id": 7,
          "capitalDeployed": 80,
          "expectedDurationInDays": 9,
          "target": "GROUP",
          "uuid": "da8cb392-ab4a-4fa8-ac0a-de407a21f835",
          "name": "Long Put",
          "tradeLogic": "<p>    </p>",
          "status": "CLOSED",
          "canEnter": true,
          "bookedPnL": 92.95,
          "mtm": 0,
          "finalPnL": 92.95,
          "bias": "NEUTRAL",
          "equityCaptitalRequired": 0,
          "hedgeCapitalRequired": 0,
          "capitalRequired": 1000,
          "maxProfit": 100,
          "maxLoss": 10,
          "fundType": "FNO",
          "publishedAt": "2025-03-13T06:43:19.000Z",
          "closedAt": "2025-03-17T12:01:58.000Z",
          "version": 18,
          "payoffChartImg": null,
          "tradeLogicImg": null,
          "createdBy": 18736,
          "instrumentId": "NSE:NIFTY 50",
          "createdAt": "2025-03-13T05:36:18.092Z",
          "updatedAt": "2025-03-17T12:02:08.823Z",
          "Instrument": {
            "id": "NSE:NIFTY 50",
            "instrument_token": 256265,
            "exchange_token": 1001,
            "tradingsymbol": "NIFTY 50",
            "name": "NIFTY 50",
            "last_price": 22067.35,
            "expiry": "1899-11-30",
            "strike": 0,
            "tick_size": 0,
            "lot_size": 75,
            "instrument_type": "EQ",
            "segment": "INDICES",
            "exchange": "NSE",
            "ISIN": null,
            "truedataSymbolId": "200000001",
            "truedataSymbol": "NIFTY 50",
            "freezeQuantity": 225,
            "createdAt": "2024-10-04T11:28:22.534Z",
            "updatedAt": "2025-03-04T05:16:42.726Z"
          },
          "B2BRecommendationLegs": [
            {
              "id": 10,
              "uuid": "6127b9ca-07f4-4b83-9a3d-61aff310fe8e",
              "status": "EXIT",
              "action": "BUY",
              "quantity": 1,
              "canEnter": true,
              "entryThreshold": 1,
              "entryPrice": 50,
              "averageEntryPrice": 50,
              "exitPrice": 100,
              "averageExitPrice": 100,
              "entryAt": "2025-03-13T05:36:18.000Z",
              "exitAt": "2025-03-17T11:41:38.000Z",
              "mtm": 50,
              "finalPnL": 50,
              "sequenceInParent": 1,
              "entryParentVersion": 1,
              "exitParentVersion": 3,
              "b2BRecommendationId": 7,
              "instrumentId": "NSE:IREDA",
              "createdAt": "2025-03-13T05:36:18.353Z",
              "updatedAt": "2025-03-13T05:36:18.353Z",
              "Instrument": {
              
                "id": "NSE:IREDA",
                "instrument_token": 5186817,
                "exchange_token": 20261,
                "tradingsymbol": "IREDA",
                "name": "INDIAN RENEWABLE ENERGY",
                "last_price": 0,
                "expiry": "1899-11-30",
                "strike": 0,
                "tick_size": 0.05,
                "lot_size": 1,
                "instrument_type": "EQ",
                "segment": "NSE",
                "exchange": "NSE",
                "ISIN": "INE202E01016",
                "truedataSymbolId": "100007530",
                "truedataSymbol": "IREDA",
                "freezeQuantity": null,
                "createdAt": "2024-10-04T11:28:18.922Z",
                "updatedAt": "2024-10-04T11:28:18.922Z"
              }
            }
          ]
        }
      ]
   }
   ```

5. ### GET /get_b2b_recommendation?recommendationId=2:

   Get full details and history of a recommendation that you are subscribed to.
   Please call [/list_b2b_recommendations](#get-list_b2b_recommendations) to get the recommendationId.
   Send the request with the `recommendationId` present in the query parameter
      #### Query Parameters
      - **recommendationId** (required)
      _Type_: `number`
     
   ```jsonc
         {
        "id": 7,
        "capitalDeployed": 80,
        "expectedDurationInDays": 9,
        "target": "GROUP",
        "uuid": "da8cb392-ab4a-4fa8-ac0a-de407a21f835",
        "name": "Long Put",
        "tradeLogic": "<p>    </p>",
        "status": "CLOSED",
        "canEnter": true,
        "bookedPnL": 92.95,
        "mtm": 0,
        "finalPnL": 92.95,
        "bias": "NEUTRAL",
        "equityCaptitalRequired": 0,
        "hedgeCapitalRequired": 0,
        "capitalRequired": 1000,
        "maxProfit": 100,
        "maxLoss": 10,
        "fundType": "FNO",
        "publishedAt": "2025-03-13T06:43:19.000Z",
        "closedAt": "2025-03-17T12:01:58.000Z",
        "version": 18,
        "payoffChartImg": null,
        "tradeLogicImg": null,
        "createdBy": 18736,
        "instrumentId": "NSE:NIFTY 50",
        "createdAt": "2025-03-13T05:36:18.092Z",
        "updatedAt": "2025-03-17T12:02:08.823Z",
        "Instrument": {
          "id": "NSE:NIFTY 50",
          "instrument_token": 256265,
          "exchange_token": 1001,
          "tradingsymbol": "NIFTY 50",
          "name": "NIFTY 50",
          "last_price": 22067.35,
          "expiry": "1899-11-30",
          "strike": 0,
          "tick_size": 0,
          "lot_size": 75,
          "instrument_type": "EQ",
          "segment": "INDICES",
          "exchange": "NSE",
          "ISIN": null,
          "truedataSymbolId": "200000001",
          "truedataSymbol": "NIFTY 50",
          "freezeQuantity": 225,
          "createdAt": "2024-10-04T11:28:22.534Z",
          "updatedAt": "2025-03-04T05:16:42.726Z"
        },
        "B2BRecommendationHistories": [
        
          {
            "id": 29,
            "oldStatus": "DRAFT",
            "newStatus": "PUBLISHED",
            "comment": "Initial publish",
            "showData": true,
            "createdAt": "2025-03-13T06:43:19.000Z",
            "b2BRecommendationId": 7,
            "updatedAt": "2025-03-13T06:43:19.851Z"
          }
        ],
        "B2BRecommendationLegs": [
        
          {
            "id": 10,
            "uuid": "6127b9ca-07f4-4b83-9a3d-61aff310fe8e",
            "status": "EXIT",
            "action": "BUY",
            "quantity": 1,
            "canEnter": true,
            "entryThreshold": 1,
            "entryPrice": 50,
            "averageEntryPrice": 50,
            "exitPrice": 100,
            "averageExitPrice": 100,
            "entryAt": "2025-03-13T05:36:18.000Z",
            "exitAt": "2025-03-17T11:41:38.000Z",
            "mtm": 50,
            "finalPnL": 50,
            "sequenceInParent": 1,
            "entryParentVersion": 1,
            "exitParentVersion": 3,
            "b2BRecommendationId": 7,
            "instrumentId": "NSE:IREDA",
            "createdAt": "2025-03-13T05:36:18.353Z",
            "updatedAt": "2025-03-13T05:36:18.353Z",
            "Instrument": {
              "id": "NSE:IREDA",
              "instrument_token": 5186817,
              "exchange_token": 20261,
              "tradingsymbol": "IREDA",
              "name": "INDIAN RENEWABLE ENERGY",
              "last_price": 0,
              "expiry": "1899-11-30",
              "strike": 0,
              "tick_size": 0.05,
              "lot_size": 1,
              "instrument_type": "EQ",
              "segment": "NSE",
              "exchange": "NSE",
              "ISIN": "INE202E01016",
              "truedataSymbolId": "100007530",
              "truedataSymbol": "IREDA",
              "freezeQuantity": null,
              "createdAt": "2024-10-04T11:28:18.922Z",
              "updatedAt": "2024-10-04T11:28:18.922Z"
            }
          }
        ]
   ```

## Responses:

- 200 Success:
  When the API produces intended result

- 401 Unauthorized:
  When you are missing the `api-key` or `api-token` in the header

- 403 Forbidden:
  When you are not sending valid headers (API key or secret) or you are trying to access a recommendation you are not subscribed.

- 404 Not Found:
  When the resource(s) you are requesting are not available
