# Explore Refersion GraphQL using Voyager

Voyager is a great tool to visualize Refersion GraphQL. Follow the steps below to explore the full set of data available through the API.

 1. Prepare a POST request:
 
        
        "https://graphql.refersion.com" \
        -H "X-Refersion-Key: <YOUR_ACCESS_TOKEN>" \
        -H "Content-Type: application/graphql" \
        
 
 2. Go to [https://apis.guru/graphql-voyager/](https://apis.guru/graphql-voyager/) and click “Custom Schema”

 3. Click “Copy Introspection Query” and paste it as the body of your POST request, keep your Voyager window open

 4. Send the POST request, copy the response and paste it back in Voyager (see below)
 
    <div style="text-align: center;">
    <img src="/assets/images/voyager.png" alt="What you request is what you get" />
    </div>
 
 5. Press "CHANGE SCHEMA" 
