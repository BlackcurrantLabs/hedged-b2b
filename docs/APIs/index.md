# Hedged B2B
APIs to get details of the recommendations the user is subscribed to.
Please visit the [Swagger Page](https://api.core.hedged.online/b2b-swagger/) for more details.

## APIs
1. ### GET /me:
    Get your profile with your preferences and account detai;s

2. ### GET /list_b2b_recommendations:
    Lists all recommendations that you are subscribed to. 
You can optionally send a preference for filtering out your recommendations.
Available filters:
      - type:
          Either `EQUITY` or `FNO` based on recommedation type.
      - bias:
          Either `BEARISH`, `BULLISH` or `NEUTRAL` based on recommendation type
      - target:
          Either `HIGH_RISK_HIGH_REWARD`, `BROKERAGE_INTENSIVE`, `SPECIAL_EVENT`, `HIGH_FREQUENCY_TRADE` or `ALL` based on recommendation target
  
3. ### GET /get_b2b_recommendation:
    Get full details and history of a recommendation that you are subscribed to. Please call /list_b2b_recommendations to get the recommendationId
  
## Responses:
- 200 Success:
    When the API produces intended result

- 401 Unauthorized:
    When you are missing the `api-key` or `api-token` in the header

- 403 Forbidden:
    When you are not sending valid headers (API key or secret) or you are trying to access a recommendation you are not subscribed.

- 404 Not Found:
    When the resource(s) you are requesting are not available
