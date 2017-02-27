# NV:MP.com API
NV:MP.com has an official OAuth2 API which gives developers access to client permissions for automated tasks or data retrieval. We also have a character API which can poll character data, and current server/faction data.

## Usage Agreement
Usage of the API assumes you will follow our code of conduct, which is designed to prevent misuse of user data and to prevent abuse of the NV:MP image.

* As a developer using the API, you must not handle, request or suggest input of user credentials. These include usernames and passwords of users. All authentication should be done on our website, with the returning authentication being your applications only form of account authentication. The only exception to this rule is development accounts, ie. accounts that you maintain (as the single user of the program) for authorising via headless software.
* As a developer using the API, you must not represent, claim or suggest your program (outside of the nv-mp.com hostname) is affiliated with NV:MP. You must not claim to be related to NV:MP, and any forms of web authentication should retain the notice: `This website is not associated with NV:MP.com`
* As a developer using the API, you must not scrape large amounts of public user or website data. User tokens that scrape more than 5,000 requests per hour to "read" scopes will have their application flagged for review. This gives roughly 1.3 requests per second to each user token. 
* As a developer using the API, you must not mis-represent your applications permissions. The permissions you request from users should be what the user expects. If you are representing to only read data, you should not have a write permission request on the users request without explicitly notifying them beforehand. 
* Site administrators on NV:MP.com can revoke your application at any point without given notice.
* As a developer using the API, you agree not to create malicious clients which may cause server disruption or change user data without the users attention.
* As a developer using the API, you agree to periodically review the usage agreement for changes.

This agreement may change, and will be updated on this repository noting dates of changes. 

## API
### Website
We use bdApi, which is a well documented OAuth2.0 implementation for XenForo. The full API write up can be found [in the API's repository docs folder](https://github.com/xfrocks/bdApi/blob/master/docs/api.markdown). We have extended some of the public API to include active team (faction) ribbon IDs, and current gender for local user queries (users/me)

Our current API root is:
`https://nv-mp.com/api/v2/`

The API can support the HTTP protocol, but we really recommend doing all sensitive token authorisation using HTTPS. As per the API spec, all requests must follow the XenForo routing style. 
`https://nv-mp.com/api/v2/index.php?users/`

Everything after the `index.php?` is regarded as the URL route.
Version 1 of the API is not active, documented or functional. It should not be used. Please stick to v2. 

### Game
The game API is actively evolving, right now the documented routes are the faction list and the active server list. Our current game server URL is:
`http://nlan.org:8088/`

HTTPS protocol is not supported currently for this API.

### GET `/static/getServers`
Returns a list of online servers in JSON format. 
[
    {
        "last_update_time": 1488207854,
        "display_name": "NV:MP Official - Free Roam",
        "ip": "euw.game.nv-mp.com",
        "port": 27015,
        "perm": true,
        "details": {
            "forum_account_only": true,
            "players": 0,
            "max_players": 32
        }
    }
}

### GET `/static/getFactions`
Returns a list of active factions in use in NV:MP's freeroam gamemode.
{
    "1": {
        "title": "White Glove Society",
        "tag_line": "We have nothing to hide here.",
        "banner": "White Glove Society",
        "banner_class": "bannerBlue"
    },
    "2": {
        "title": "Caesar's Legion",
        "tag_line": "Render Unto Caesar",
        "banner": "Caesar's Legion",
        "banner_class": "bannerOrange"
    }
}