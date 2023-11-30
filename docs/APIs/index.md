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

4. ### GET /predictions/
A set of APIs for predictions made through integration with [Green Hedged](), each will send you a JSON response of the prediction.

    4.a. #### GET /predictions/get_index_gauge:
	Get Green predictions on Index Gauge.

	Expected payload:
	```jsonc
	{
	    Index: "string (one of 'nifty' or 'banknifty')",
	    History: "boolean (true or false); optional"
	}
	```

	If `History` is set to `true`, you would get an array of the predictions which would look like this:
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
	    Time: "number",
	    UTM: "number",
	    Price: "number" 
	}
	```

#### GET /predictions/get_index_direction:
Get Green predictions on Index Direction
Expected payload:
```jsonc
{
    Index: "string (one of 'nifty' or 'banknifty')",
    History: "boolean (true or false); optional"
}
```

If `History` is set to `true`, you would get an array of the predictions which would look like this:
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
    Time: "number",
    UTM: "number",
    AIR: "number",
    Price: "number" 
}
```

#### GET /predictions/get_OMD:
Get Green predictions on Options Momentum Driver (OMD)
Expected payload:
```jsonc
{
    Index: "string (one of 'nifty' or 'banknifty')",
    Expiry: "string (one of 'cw', 'cm' or 'nm')",
    Strike: "number"
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

#### GET /predictions/get_OIO:
Get Green predictions on Open Interest Outlook (OIO)
Expected payload:
```jsonc
{
    Index: "string (one of 'nifty' or 'banknifty')",
    Expiry: "string (one of 'cw', 'cm' or 'nm')"
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

#### GET /predictions/get_OPC:
Get Green predictions on Options Prem Change (OPC)
Expected payload:
```jsonc
{
    Index: "string (one of 'nifty' or 'banknifty')",
    Expiry: "string (one of 'cw', 'cm' or 'nm')",
    Type: "string (one of 'Call' or 'Put')"
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

#### GET /predictions/get_OIM:
Get Green predictions on OI Multistrike (OIM)
Expected payload:
```jsonc
{
    Index: "string (one of 'nifty' or 'banknifty')",
    Expiry: "string (one of 'cw', 'cm' or 'nm')",
    Type: "string (one of 'top3', 'round' or 'nearest')"
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

#### GET /predictions/get_EO:
Get Green predictions on Equity Opportunities (EO)
Expected payload:
```jsonc
{
    Type: "string (one of 'Daily' or 'Weekly')"
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

#### GET /predictions/get_SO:
Get Green predictions on Stock Outlook (SO)
Expected payload:
```jsonc
{
    Stock: "string"
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

#### GET /predictions/get_heatmap:
Get Heatmap from Green
Expected payload:
```jsonc
{
    Index: "string (one of 'nifty' or 'banknifty')",
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

#### GET /predictions/get_dayscans:
Get Day Scans based on Green's data look-up
Expected payload:
```jsonc
{
    Index: "string (one of 'nifty' or 'banknifty')",
}
```

The response would be of the following shape:
```jsonc
[
    {
        Time: "number",
        " Day_ATM": "number",
        " Running_ATM": "number",
        " CMP": "number"
    },
    ...
]
```

#### GET /predictions/get_future:
Get Future based on Green's data look-up
Expected payload:
```jsonc
{
    Index: "string (one of 'nifty' or 'banknifty')",
    Chart: "number (min: 1. max: 5)"
}
```

The response would be of the following shape:
```jsonc
[
    {
        time: "number (with decimal places)",
        o: "number (with decimal places)",
        h: "number (with decimal places)",
        l: "number (with decimal places)",
        c: "number",
        v: "number",
        oi: "number"
    },
    ...
]
```

#### GET /predictions/get_options:
Get Options based on Green's data look-up
Expected payload:
```jsonc
{
    Index: "string (one of 'Nifty' or 'BankNifty')",
    Symbol: "string (like NIFTY23051119600CE)"
}
```

The response would be of the following shape:
```jsonc
[
    {
        time: "number (with decimal places)",
        o: "number (with decimal places)",
        h: "number (with decimal places)",
        l: "number (with decimal places)",
        c: "number",
        v: "number",
        oi: "number"
    },
    ...
]
```

#### GET /predictions/get_expiries:
Get Expiries based on Green's data look-up
Expected payload:
```jsonc
{
    Index: "string (one of 'Nifty' or 'BankNifty')"
}
```

The response would be of the following shape:
```jsonc
[
    {
        Directory: "number",
        Type: "CW",
        Expiry: "number (with decimal places)",
        Active: "number",
    },
    ...
]
```

#### GET /predictions/get_stocks:
Get Stocks based on Green's data look-up
Expected payload:
```jsonc
{
    Index: "string (one of 'Nifty' or 'BankNifty')"
}
```

The response would be of the following shape:
```jsonc
[
    {
         "Company Name": "string",
        Industry: "string",
        Symbol: "string",
        Series: "string",
        "ISIN Code": "string"
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
