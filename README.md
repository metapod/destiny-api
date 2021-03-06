# destiny-api

An API to interface with Bungie.net for Destiny stats using Node.js / [Express 4](http://expressjs.com/).

## Usage

### Routes

Use the destiny-api by hosting it as a node.js application then query with the following routes.

| Code | Description |
| ------------- | ------------- |
| `/Group/:groupId/MembersV3/:page`  | Search for the provided clan.  |
| `/SearchDestinyPlayer/:membershipType/:displayName` | Search for the provided player's display name based on membership type (1 = XBL, 2 = PSN). |
| `/:platform/Account/:membershipId` |Get all characters for the provided player (membership ID). |
| `/:platform/Account/:membershipId/Character/:characterId/Progression/` | Get progressions for the provided character. |
| `/:platform/Account/:membershipId/Character/:characterId/Activities/` | Get activities for the provided character. |
| `/Stats/ActivityHistory/:platform/:membershipId/:characterId/:mode` | Get activity history for the provided character on the given type (Raid, Strike, etc). |

### Handling JSON

Handle the JSON from the destiny-api using code similar to the following:

```javascript
function getJson(routeUrl, success, failure) {	
	var searchUrl = 'yourAppBaseURLHere' + routeUrl + '?callback=?';
	return $.ajax({
		url: searchUrl,
		dataType: "jsonp",
		data: "data=yeah",
		jsonp: 'callback',
		success: function (data) {
			success(JSON.parse(data));
		},
		error: function (result) {
			failure(result);
		}
	});
}
```
