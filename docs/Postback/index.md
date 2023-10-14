# Post Back

A postback url would allow you to recieve updates on recommendations that you have subscribed to.

To use Postback, please add your postback url through the [console](https://core.hedged.online/b2b/account). After this, have a server at this postback url to recieve events on the recommendations.

## Events

There are 3 types of events:

1. Published Event (PUBLISHED): 
    When the recommendation actually gets published.
2. Update Event (MODIFIED): 
    Whenever there are updates to one of the published recommendation.
3. Closed Event (CLOSED): 
    When the recommendation finally gets closed.

## Expected body according to event

1.  PUBLISHED:

        When a recommendation is published, expect the following response:

    | Object Property    |      Value   | Remarks    |
    |--------------------|:------------:|-----------:|
    | eventType          |  "PUBLISHED" | This tells you the type of event among the 3 types |
    | b2BRecommendation  |  [Recommendation Object](#recommendation-object)  | This will give you the full details of the corresponding recommendation object with it's legs and history |

2.  MODIFIED:

        When a recommendation is updated after being published, expect the following response:

    | Object Property    |      Value   | Remarks    |
    |--------------------|:------------:|-----------:|
    | eventType          |  "PUBLISHED" | This tells you the type of event among the 3 types |
    | b2BRecommendation  |  [Recommendation Object](#recommendation-object)  | This will give you the full details of the corresponding recommendation object with it's legs and history |
    | legsAdded | B2B Recommendation Leg (Object) | The legs that were added as part of this update. |
    | legsModified | B2B Recommendation Leg (Object) | The legs that were updated/modified as part of this update. |
    | legsExited | B2B Recommendation Leg (Object) | The legs that were exited as part of this update. |
    
    Please refer to the Recommendation object's `B2BRecommendationLegs`` property for further details of the BB Recommendation Leg object

3.  CLOSED:

        When a recommendation is closed, expect the following response:

    | Object Property    |      Value   | Remarks    |
    |--------------------|:------------:|-----------:|
    | eventType          |  "CLOSED" | This tells you the type of event among the 3 types |
    | b2BRecommendation  |  [Recommendation Object](#recommendation-object)  | This will give you the full details of the corresponding recommendation object with it's legs and history |

## Recommendation Object
The recommendation object has the following components:

- B2B Recommendation
    - Instrument (of recommendation)
    - Legs
        - Instrument (of recommendation leg)
        - Legs History
    - History


These components are arranged to make up the full Recommendation object:
```jsonc
{
    "B2BRecommendation": {
        "id": "integer",
        "uuid": "string (uuid)",
        "tradeLogic": "string", // The why of this recommendaton
        "status": "string (one of 'PUBLISHED' or 'CLOSED')",
        "bookedPnL": "number", //  Profits or losses from exited legs
        "mtm": "number", // Profits or losses from the publish date bookedPnL + mtm of ENTERED legs
        "finalPnL": "number", // Final profit or loss
        "bias": "string (one of 'BEARISH', 'BULLISH' or 'NEUTRAL')",
        "author": "string",
        "capitalRequired": "number",
        "capitalDeployed": "number",
        "maxProfit": "number",
        "expectedProfit": "number",
        "maxLoss": "number",
        "type": "string (one of 'EQUITY' or 'FNO')",
        "target": "string (one of 'HIGH_RISK_HIGH_REWARD', 'BROKERAGE_INTENSIVE', ,'SPECIAL_EVENT', 'HIGH_FREQUENCY_TRADE' or 'ALL')",
        "expectedDurationInDays": "integer",
        "publishedAt": "datetime",
        "closedAt": "datetime",
        "version": "integer", //     To be incremented whenever the strategy is updated after publishing, default: 1
        "payoffChartImg": "string",
        "tradeLogicImg": "string",
        "instrumentId": "string (references the Instrument)",

        "Instrument": {
            "id": "string",
            "instrument_token": "number",
            "exchange_token": "number",
            "tradingsymbol": "string",
            "name": "string",
            "last_price": "number",
            "expiry": "string",
            "strike": "number",
            "tick_size": "number",
            "lot_size": "number",
            "instrument_type": "string (one of 'CE', 'PE', 'FUT' or 'EQ')",
            "segment": "string (one of 'NFO-FUT', 'NFO-OPT', 'NSE' or 'INDICES')",
            "exchange": "string (one of 'MCX', 'NFO' or 'NSE')",
            "createdAt": "datetime",
            "updatedAt": "datetime",
        },
        
        "B2BRecommendationLegs": [
            {
                "id": "integer",
                "uuid": "string",
                "status": "string (one of 'ENTER' or 'EXIT')",
                "action": "string (one of 'BUY' or 'SELL')",
                "quantity": "number",
                "entryPrice": "number (manually added)",
                "exitPrice": "number (manually added)",
                "entryAt": "datetime",
                "exitAt": "datetime",
                "mtm": "number",
                "finalPnL": "number",
                "sequenceInParent": "integer",
                "entryParentVersion": "integer",
                "exitParentVersion": "integer",
                "instrumentId": "string (references the Instrument)",
                
                "Instrument": {
                    "id": "string",
                    "instrument_token": "number",
                    "exchange_token": "number",
                    "tradingsymbol": "string",
                    "name": "string",
                    "last_price": "number",
                    "expiry": "string",
                    "strike": "number",
                    "tick_size": "number",
                    "lot_size": "number",
                    "instrument_type": "string (one of 'CE', 'PE', 'FUT' or 'EQ')",
                    "segment": "string (one of 'NFO-FUT', 'NFO-OPT', 'NSE' or 'INDICES')",
                    "exchange": "string (one of 'MCX', 'NFO' or 'NSE')",
                    "createdAt": "datetime",
                    "updatedAt": "datetime",
                },
      
                "B2BRecommendationLegHistories": [{
                    "id": "integer",
                    "uuid": "string",
                    "oldStatus": "string",
                    "newStatus": "string",
                    "comment": "string",
                    "b2BRecommendationLegId": "integer (references the B2B Recommendation Leg)",
                }]
            }
        ],

        "B2BRecommendationHistories": [
            {
                "id": "integer",
                "oldStatus": "string",
                "newStatus": "string",
                "comment": "string",
                "b2BRecommendationId": "integer (references the B2B Recommendation)",
            }
        ],
    }
}
```

The object properties are named in a self-explanatory manner. However, we have added references to the data-type of the property and further description in the comments to provide you with more context.

This is the data you would recieve on the `b2BRecommendation` field of your post back call.