Certificates
===============

Certificates are an essential part of every campaign.

They're used to uniquely identify a certain person or organization, and offer authenthicity reasurance.

Every campaign needs to have a valid certificate associated.

By default, your campaign will use one of our public certificates we've created, but for several security reasons, it's best if you upload your own to Apple's as shown in [this detailed tutorial](http://passworks.io/certificates/how_to) we've built for you, and use it for your campaigns. As mentioned in the tutorial, you need a Apple Developer account in order to create certificates.

Having a unique certificate for your organization's passes make them distinct from all others, as that all the passes you generate will stack in the wallet, and not mix in with other organizations' as they will if you use our default certificate (Every organization wich use our certificates will get their passes stacked, significantly reducing visibility).


Listing the certificates
----------------

```shell
GET /v2/certificates
```

Response:

```json
[
	{
		"id": "f255bb41-ba38-4bfa-9398-3db341859e59",
		"team_identifier": "H2R9WS56F9",
		"pass_type_identifier": "pass.io.passworks.public.generic.1",
		"issued_to": "Passworks, S.A.",
		"expires_at": "2015-03-17T14:21:40Z"
	},
	{
		"id": "09afd258-8cbe-447c-b792-0f975452ecc5",
		"team_identifier": "H2R9WS56F9",
		"pass_type_identifier": "pass.io.passworks.public.storecard.1",
		"issued_to": "Passworks, S.A.",
		"expires_at": "2015-03-17T14:23:50Z"
	},
	{
		"id": "3fdddf1c-0f8e-4e12-9356-7fe985864ef4",
		"team_identifier": "H2R9WS56F9",
		"pass_type_identifier": "pass.io.passworks.public.eventticket.1",
		"issued_to": "Passworks, S.A.",
		"expires_at": "2015-03-17T14:20:10Z"
	}
]
```

Getting a specific certificate
----

```shell
GET /v2/certificates/{certificate_id}
```

Response:

```json
{
	"id": "f255bb41-ba38-4bfa-9398-3db341859e59",
	"team_identifier": "H2R9WS56F9",
	"pass_type_identifier": "pass.io.passworks.public.generic.1",
	"issued_to": "Passworks, S.A.",
	"expires_at": "2015-03-17T14:21:40Z"
}
```


Creating a certificate
----------------

In order to create a certificate, since this process cannot be automated because it requires an Apple Developer account, and is only needed just ocasionally, it makes no sense creating certificates through the API, which would just be complicated.

Instead, log onto our SAAS and upload the certificate in [your certificates page](http://www.passworks.io/certificates).