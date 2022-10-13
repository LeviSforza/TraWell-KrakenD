
# KrakenD config info

For the time being every enpoint in krakend.json demands authentication. If it turns out that endpoint that you are working on should be accessible for guest users, you should delete "extra_config" attribute from that endpoint in krakend.json.

Right now, every endopoint also assumes that response data will be in JSON format. If you need to return data in response to request in different format, you should change "output_encoding" and "encoding" for your endpoint accordingly -> [KrakenD documentation for content types](https://www.krakend.io/docs/endpoints/content-types/) 

