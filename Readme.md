


# Suggested Flow:


1. Embed in an angular component:
```html
<!-- Start of Meetings Embed Script -->
    <div class="meetings-iframe-container" data-src="https://meetings.hubspot.com/hassan-magdy?embed=true"></div>
    <script type="text/javascript" src="https://static.hsappstatic.net/MeetingsEmbed/ex/MeetingsEmbedCode.js"></script>
  <!-- End of Meetings Embed Script -->
```

2. As Hubspot SDK posts a `message` to the parent window, we will listen to the `message` event fired from the SDK.
```js
  window.addEventListener("message", (event) => {
            console.log(event)
            if(event.data && event.data.meetingBookSucceeded){
                console.log('booking succeeded, unlock app-web for PK/IN users')
                // Unlock web-app experience
            }
        });
```

Returned data:
```json
{
    "meetingBookSucceeded": true,
    "meetingsPayload": {
        "linkType": "PERSONAL_LINK",
        "offline": false,
        "userSlug": "hassan-magdy",
        "formGuid": "317b5707-bcb4-4220-9139-efc900d98814",
        "bookingResponse": {
            "event": {
                "duration": 900000,
                "formFields": [],
                "dateString": "2023-08-21",
                "dateTime": 1692638100000
            },
            "postResponse": {
                "timerange": {
                    "start": 1692638100000,
                    "end": 1692639000000
                },
                "organizer": {
                    "firstName": "Hassan",
                    "lastName": "Magdy",
                    "email": "",
                    "fullName": "",
                    "name": "Hassan Magdy",
                    "userId": null
                },
                "bookedOffline": false,
                "contact": {
                    "firstName": "test",
                    "lastName": "test",
                    "email": "hassan+21Aug2023@timedoctor.com",
                    "fullName": "",
                    "name": "testing schedule flow",
                    "userId": null
                }
            }
        },
        "isPaidMeeting": false
    }
}
```

3. Once we get a message event with `meetingBookSucceeded`, we will unlock the web-app experience.