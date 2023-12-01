# Hedged B2B

APIs to get details of the recommendations the user is subscribed to.

Please visit the <a href="https://api.core.hedged.online/b2b-swagger/"><button style="unset:all; padding: 0.3rem; border-radius: 5px; background-color:#4051b5; color:white; cursor:pointer;">Swagger Page</button></a> for more details.

## APIs

1. ### GET /me:

   Get your profile with your preferences and account details.

2. ### GET /list_b2b_recommendations:

   Lists all recommendations that you are subscribed to.
   You can optionally send a preference for filtering out your recommendations.
   Available filters: - type:
   Either `EQUITY` or `FNO` based on recommendation type. - bias:
   Either `BEARISH`, `BULLISH` or `NEUTRAL` based on recommendation type - target:
   Either `HIGH_RISK_HIGH_REWARD`, `BROKERAGE_INTENSIVE`, `SPECIAL_EVENT`, `HIGH_FREQUENCY_TRADE` or `ALL` based on recommendation target

3. ### GET /get_b2b_recommendation?recommendationId=2:

   Get full details and history of a recommendation that you are subscribed to.
   Please call [/list_b2b_recommendations](#get-list_b2b_recommendations) to get the recommendationId.
   Send the request with the `recommendationId` present in the query parameter

4. ### GET /suggestions/
   A set of APIs for suggestions made through integration with [Green Hedged](), each will send you a JSON response of the prediction.

#### GET /suggestions/get_index_gauge:

Get Green suggestions on Index Gauge
Expected payload:

```jsonc
{
  "Index": "string (one of 'nifty' or 'banknifty')",
  "History": "boolean (true or false); optional"
}
```

If `History` is set to `true`, you would get an array of the suggestions which would look like this:

```jsonc
[
    {
        Time: "number",
        UTM: "number",
        Price: "number"
    },
    ...
]
```

Else you would just get the latest prediction, which would be of this shape:

```jsonc
{
  "Time": "number",
  "UTM": "number",
  "Price": "number"
}
```

#### GET /suggestions/get_index_direction:

Get Green suggestions on Index Direction
Expected payload:

```jsonc
{
  "Index": "string (one of 'nifty' or 'banknifty')",
  "History": "boolean (true or false); optional"
}
```

If `History` is set to `true`, you would get an array of the suggestions which would look like this:

```jsonc
[
    {
        Time: "number",
        UTM: "number",
        AIR: "number",
        Price: "number"
    },
    ...
]
```

Else you would just get the latest prediction, which would be of this shape:

```jsonc
{
  "Time": "number",
  "UTM": "number",
  "AIR": "number",
  "Price": "number"
}
```

#### GET /suggestions/get_OMD:

Get Green suggestions on Options Momentum Driver (OMD)
Expected payload:

```jsonc
{
  "Index": "string (one of 'nifty' or 'banknifty')",
  "Expiry": "string (one of 'cw', 'cm' or 'nm')",
  "Strike": "number"
}
```

The response would be of the following shape:

```jsonc
[
    {
        Time: "number",
        CE.ltp: "number (with decimal places)",
        "Call OI Interpretation": "string",
        Strike: "number",
        "Put OI Interpretation": "string",
        "PE.ltp": ,
        CMP: "number (with decimal places)",
        PCR: "number (with decimal places)",
    },
    ...
]
```

#### GET /suggestions/get_OIO:

Get Green suggestions on Open Interest Outlook (OIO)
Expected payload:

```jsonc
{
  "Index": "string (one of 'nifty' or 'banknifty')",
  "Expiry": "string (one of 'cw', 'cm' or 'nm')"
}
```

The response would be of the following shape:

```jsonc
[
    {
        Time: "number",
        Price: "number (with decimal places)",
        Strike: "number",
        Calls: "number",
        Calls_IV: "number",
        Puts: "number",
        Puts_IV: "number",
    },
    ...
]
```

#### GET /suggestions/get_OPC:

Get Green suggestions on Options Prem Change (OPC)
Expected payload:

```jsonc
{
  "Index": "string (one of 'nifty' or 'banknifty')",
  "Expiry": "string (one of 'cw', 'cm' or 'nm')",
  "Type": "string (one of 'Call' or 'Put')"
}
```

The response would be of the following shape:

```jsonc
[
    {
        Time: "number",
        Expiry: "number (with decimal places)",
        Strike: "number",
        Premium: "number (with decimal places)",
        IV: "number",
        Type: "string (one of 'Call' or 'Put')",
    },
    ...
]
```

#### GET /suggestions/get_OIM:

Get Green suggestions on OI Multistrike (OIM)
Expected payload:

```jsonc
{
  "Index": "string (one of 'nifty' or 'banknifty')",
  "Expiry": "string (one of 'cw', 'cm' or 'nm')",
  "Type": "string (one of 'top3', 'round' or 'nearest')"
}
```

The response would be of the following shape:

```jsonc
[
    {
        Date: "number (with decimal places)",
        Time: "number",
        Expiry: "number (with decimal places)",
        Type: "string (one of 'Call' or 'Put')",
        Strike: "number",
        Call: "number",
        Put: "number",
        Future: "number"
    },
    ...
]
```

#### GET /suggestions/get_EO:

Get Green suggestions on Equity Opportunities (EO)
Expected payload:

```jsonc
{
  "Type": "string (one of 'Daily' or 'Weekly')"
}
```

The response would be of the following shape:

```jsonc
[
    {
        Date: "number (with decimal places)",
        Symbol: "string",
        Buying_Price: "number",
        Stop_Loss: "number"
    },
    ...
]
```

#### GET /suggestions/get_SO:

Get Green suggestions on Stock Outlook (SO)
Expected payload:

```jsonc
{
  "Stock": "string"
}
```

The response would be of the following shape:

```jsonc
[
    {
        Time: "number",
        Symbol: "string",
        Name: "string",
        Description: "string"
    },
    ...
]
```

#### GET /suggestions/get_heatmap:

Get Heatmap from Green
Expected payload:

```jsonc
{
  "Index": "string (one of 'nifty' or 'banknifty')"
}
```

The response would be of the following shape:

```jsonc
[
    {
        TS: "number",
        Symbol: "string",
        LTP: "number (with decimal places)",
        High: "number",
        Low: "number",
        Change: "number (with decimal places)",
        Change_Percentage: "number (with decimal places)"
    },
    ...
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
