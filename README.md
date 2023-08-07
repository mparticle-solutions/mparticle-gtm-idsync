## IDSync Template 
This GTM template allows for a customer to be logged in, logged out, or to be modified via your GTM implementation. This tag required the successful loading of the mParticle SDK to have been completed prior to this tag firing. This does require some additional set-up in comparison to other GTM tag templates, an identity callback function and user identities will need to be added to the data layer before the tag is triggered. 

### Steps to enable: 
1. Enable the [data layer](https://developers.google.com/tag-platform/tag-manager/datalayer). 
```
<script>
 
    //configure the data layer
    window.dataLayer = window.dataLayer || [];
    
</script>
```
2. Add an identity callback to the data layer. 
```
 <script>

    //add a custom identity callback to the data layer
    dataLayer.push({
        identityCallback: function(result) { 
            if (result.getUser()) { 
                // Do something once an identity call has been made.
                // For more information, see https://docs.mparticle.com/developers/sdk/web/idsync/#sdk-initialization-and-identify
                console.log(result);
            } 
        },
    });
    
</script>
```
3. Add desired user identities to the data layer. 
```
<script type="text/javascript">

        //this is an example function that runs when the login button is clicked. 
       function processIDSync(eventName){
            let email = document.querySelector('#email').value; 
            dataLayer.push({
                'userIdentities': {
                    'email': email
                }
            })
            
            //this is the example GTM custom event trigger for IDSync, please note that the identities are pushed before the trigger event. 
            dataLayer.push({'event': eventName'})
        }
    </script>
```
4. Select the IDSync Template from the [Google Community Template Gallery](https://tagmanager.google.com/gallery/#/?page=1). 
5. Configure the tag with the desired IDSync event type. 
6. Configure the trigger to coincide with the login event. 
7. Deploy the tag. 
