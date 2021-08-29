# sendinAppNotification

To Enable App Notification 

fetch(window.origin + "/api/data/v9.1/SaveSettingValue()",{
 method: "POST", 
   headers: {'Content-Type': 'application/json'},
   body: JSON.stringify({AppUniqueName: "Your app unique name", SettingName:"AllowNotificationsEarlyAccess", Value: "true"})
   });
   
Note: 

Change "Your app unique name" to your Model Driven App Name

For Sample popup

function OnLoad(executionContext) {
    var formContext = executionContext.getFormContext();
    var systemuserid = formContext.context.getUserId().replace("{","").replace("}","");
    var notificationRecord =
    {
        "title": "Welcome",
        "body": "Welcome to the world of app notifications!",
        "ownerid@odata.bind": "/systemusers(" + systemuserid + ")",
        "icontype": 100000000, // info
        "toasttype": 200000000 // timed
    }
    // Create notification record
    Xrm.WebApi.createRecord("appnotification", notificationRecord).
        then(
            function success(result) {
                console.log("notification created with ID: " + result.id);
            },
            function (error) {
                console.log(error.message);
                // handle error conditions
            }
        );
}
