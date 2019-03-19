---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='http://localhost/signup'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the FeedLab API! You can use our API to access FeedLab API endpoints, which can get information on subscriptions.

We have language bindings in Shell! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.


# Authentication

> To authorize, use this code:
  
```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: $TOKEN"
```

> Make sure to replace `$TOKEN` with your Token.

FeedLab uses Tokens to allow access to the API. You can register a new FeedLab Tokens at our [developer portal](http://localhost).

FeedLab expects for the Token to be included in all API requests to the server in a header that looks like the following:

`Authorization: $TOKEN`

<aside class="notice">
You must replace <code>$TOKEN</code> with your personal Token. Use export <code>TOKEN=xxxxxx</code>
</aside>

# Subscriptions

## Subscribe to Feed

```shell
curl "http://api.localhost/v1/subscriptions/" \
  -H "Authorization: $TOKEN"
  -H "Content-Type: application/json" 
  -d '{
    "url": "https://webrazzi.com/feed/"
    "callback": "https://webhook.site/cb0b8f90-d313-436f-b829-dc259428f4f9"
  }'
```

> The above command returns JSON structured like this:

```json
{
  "status": "successfully added subscription"
}
```

This endpoint **subscribes** user to provided ```url``` and server will POST new feed items to provided ```callback```

### HTTP Request

```POST  http://api.localhost/v1/subscriptions/```

### JSON Data

Key | Description
--- | ---
url | Feed URL to be subscribed
callback | Callback URL for feed updates


## Get All Subscriptions

```shell
curl "http://api.localhost/v1/subscriptions/"
  -H "Authorization: $TOKEN"
```

> The above command returns JSON structured like this:

```json
[
    {
        "feed": {
            "url": "https://shiftdelete.net/feed/",
            "last_item_urls": [
                "https://shiftdelete.net/?p=236498",
                "https://shiftdelete.net/?p=236536",
                "https://shiftdelete.net/?p=236549",
                "https://shiftdelete.net/?p=236550",
                "https://shiftdelete.net/?p=236560",
                "https://shiftdelete.net/?p=236572",
                "https://shiftdelete.net/?p=236598",
                "https://shiftdelete.net/?p=236602",
                "https://shiftdelete.net/?p=236623",
                "https://shiftdelete.net/?p=236627"
            ],
            "last_fetch": "2019-03-19T12:03:06.967646Z",
            "next_fetch": "2019-03-19T12:33:06.967646Z"
        },
        "callback": "https://webhook.site/cb0b8f90-d313-436f-b829-dc259428f4f9"
    },
    {
        "feed": {
            "url": "https://webrazzi.com/feed/",
            "last_item_urls": [
                "https://webrazzi.com/2019/03/18/typorama-ve-videorama-abd-merkezli-appholdings-tarafindan-satin-alindi/",
                "https://webrazzi.com/2019/03/18/fidelity-national-information-worldpayi-34-milyar-dolara-satin-alacak/",
                "https://webrazzi.com/2019/03/18/ipad-mini-ve-ipad-air-turkiye-ozellikler-ve-fiyati/",
                "https://webrazzi.com/2019/03/19/interaktif-diziden-yerellesmeye-netflixin-2019-ajandasi/",
                "https://webrazzi.com/2019/03/19/interaktif-you-vs-wild/",
                "https://webrazzi.com/2019/03/19/yemeksepeti-turkiyenin-borek-trendini-paylasti/",
                "https://webrazzi.com/2019/03/19/teknoloji-karsitligi-new-jerseyde-kendini-gosterdi-nakitsiz-calisan-market-ve-restoranlar-kapanacak/",
                "https://webrazzi.com/2019/03/19/reed-hastings-odagimiz-kullanicilar-ve-basarili-icerik-apple-ve-amazon-degil/",
                "https://webrazzi.com/2019/03/19/reedsy-discovery-bagimsiz-kitaplar-ve-yazarlarla-tanismanizi-sagliyor/",
                "https://webrazzi.com/2019/03/19/stok-videolari-ucretsiz-olarak-sunan-platform-pexels-videos/"
            ],
            "last_fetch": "2019-03-19T12:03:05.805741Z",
            "next_fetch": "2019-03-19T12:33:05.805741Z"
        },
        "callback": "https://webhook.site/cb0b8f90-d313-436f-b829-dc259428f4f9"
    }
]
```

This endpoint **retrieves** all subscriptions.

### HTTP Request

`GET http://api.localhost/v1/subscriptions/`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
page | 1 | Set this for pagination

## Delete a Specific Subscription

```shell
curl "http://api.localhost/v1/subscriptions/" \
  -X DELETE \
  -H "Content-Type: application/json" \
  -H "Authorization: $TOKEN" \
  -d '{
  "url":"https://shiftdelete.net/feed/",
  "callback": "https://webhook.site/cb0b8f90-d313-436f-b829-dc259428f4f9"
}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "successfully deleted subscription"
}
```

This endpoint **deletes** a specific subscription.

### HTTP Request

`DELETE http://api.localhost/subscriptions/`

### JSON Data

Key | Description
--------- | -----------
url | The feed URL to be deleted
callback | Callback URL provided on subscription

