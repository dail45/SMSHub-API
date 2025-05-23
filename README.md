from main import api_key

# SMSHub API

## Usage showcase:

```python
from SMSHubAPI import SMSHubAPI

api_key = "YOUR_API_KEY"
api = SMSHubAPI(
    api_key,  # required
    retries=5,  # optional[default] (retries count for requests)
    delay=1,  # optional[default] (delay between retries)
    raise_for_status=False,  # optional[default] (if True raise Exceptions else return PendingResponse with exception)
    proxy=None  # optional[default] (proxy must look like for requests lib)
)

phone = api.get_number(
    "SERVICE_NAME",  # required
    operator=None,  # optional[default] operator name
    country=None,  # optional[default] country ID
    max_price=None,  # optional[default] max price for phone number
    currency=None  # optional[default] currency for max_price
)

...  # do something for send sms

rsp = api.sms_sent()  # optional
if not rsp:
    api.sms_cancel()

code = api.wait_for_sms(
    interval=1,  # interval for requests to get sms
    timeout=60  # timeout of waiting for sms
)

if not code:
    api.sms_cancel()

...  # do something with sms

api.sms_finish()  # use this if all right or after api.sms_retry()


# api.sms_retry()  # use next if you need to get new sms (free)
```
