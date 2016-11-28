# Organizations

Organizations are the atom of the Passworks platform.

The usage of this endpoint is limited and special permissions need to be added
to your account, if need this permission please contact support@passworks.io
and ask for the "Create and manage organizations API permission" please include: **API username of your current account** and **reason for requesting this permission**.

> There is a initial limit of `10` children organizations per organization.
> This limit can be increase by contacting support@passworks.io

## Creating a new organization

To create a organization simply call the endpoint and provide the organization name.

You can have multiple organizations with the same name.

```
POST /v2/organizations
```

POST Body:
```
{
  "name": "Organization name"
}
```

API example response:

```
{
  "id": "0b09cb7b-8fc2-4eb2-ac11-81c4424261a1",
  "name": "Acme Corporation",
  "api_username": "...",
  "api_password": "...",
  "webhook_url": null,
  "users_count": 0,
  "locked_at": null,
  "updated_at": "2016-11-28T18:06:54.749Z",
  "created_at": "2016-11-28T18:06:54.716Z"
}
```


NOTE: For security reasons organizations created via API are considered automated accounts and don't have assigned users so there is no way to login to the web interface.

## Listing organizations

Lists all organizations under the current account, please note that is output is paginated.

You can use the "api_username" and "api_password" as the credentials to manage that organizations resources under the Passworks platform.

```
GET /v2/organizations
```

API example response:

```
[
  {
    "id": "0b09cb7b-8fc2-4eb2-ac11-81c4424261a1",
    "name": "Acme Corporation",
    "api_username": "...",
    "api_password": "...",
    "webhook_url": null,
    "users_count": 0,
    "locked_at": null,
    "updated_at": "2016-11-28T18:06:54.749Z",
    "created_at": "2016-11-28T18:06:54.716Z"
  }
]
```

## Reseting API Password

For security reasons you can refresh (re-issue) a new password for a given organization.

```
POST /v2/organizations/<organization_id>/refresh_api_password
```

API example response:

```
{
  "id": "0b09cb7b-8fc2-4eb2-ac11-81c4424261a1",
  "name": "Acme Corporation",
  "api_username": "...",
  "api_password": "...",
  "webhook_url": null,
  "users_count": 0,
  "locked_at": null,
  "updated_at": "2016-11-28T18:31:00.750Z",
  "created_at": "2016-11-28T18:06:54.716Z"
}
```

NOTE: To reset the API password of your main account you will need to login to the web interface and reset it there.
