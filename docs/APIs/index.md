# Hedged B2B
APIs to get details of the recommendations the user is subscribed to.

Please visit the <a href="https://api.core.hedged.online/b2b-swagger/"><button style="unset:all; padding: 0.3rem; border-radius: 5px; background-color:#4051b5; color:white; cursor:pointer;">Swagger Page</button></a> for more details.

## APIs
1. ### GET /me:
Get your profile with your preferences and account details.

2. ### GET /list_b2b_recommendations:
Lists all recommendations that you are subscribed to. 
You can optionally send a preference for filtering out your recommendations.
Available filters:
      - type:
          Either `EQUITY` or `FNO` based on recommendation type.
      - bias:
          Either `BEARISH`, `BULLISH` or `NEUTRAL` based on recommendation type
      - target:
          Either `HIGH_RISK_HIGH_REWARD`, `BROKERAGE_INTENSIVE`, `SPECIAL_EVENT`, `HIGH_FREQUENCY_TRADE` or `ALL` based on recommendation target
  
3. ### GET /get_b2b_recommendation?recommendationId=2:
Get full details and history of a recommendation that you are subscribed to.
Please call [/list_b2b_recommendations](#get-list_b2b_recommendations) to get the recommendationId.
Send the request with the `recommendationId` present in the query parameter
  
## Responses:
- 200 Success:
    When the API produces intended result

- 401 Unauthorized:
    When you are missing the `api-key` or `api-token` in the header

- 403 Forbidden:
    When you are not sending valid headers (API key or secret) or you are trying to access a recommendation you are not subscribed.

- 404 Not Found:
    When the resource(s) you are requesting are not available
