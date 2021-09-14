# vue-js-communication-box
Demo of the communication box programmed with Vue JS for Docket TMLS application. Code is fully reactive, organized, and maintainable.

To init, the `index.vue` component makes an Http get request to the backend, retrieving a json of all messages that belong to the selected 'trip'. This data is then set to the `messages` property, defined in the data hook. `this.messages` is then passed to child component `./MessagesSection.vue` which iterates through the array, sending each to `inc/message.vue` sub-component for final processing before display.

![Image One](https://user-images.githubusercontent.com/74021878/133347499-731ac386-852f-4eb2-adee-ed827023c213.png)


When sending, the component makes an Http post request to the backend and then receives a message as an object back. The object is then pushed to the array of messages, reactively displaying the new message to the user.

![Image Two](https://lh3.googleusercontent.com/At8XA4yh-xiht8QHbIKOScsq__BmFGdnhA_tosgqOIIXieDrJMNoxrfF6fv2h-fj3DaAWdOVPRXqib650AHYEI2h9PqRW8n0-R1Sv8j9Y7R4YSYzY2rqlHQd2Gzo3ImNquloaknU5WQgv4W1WZTQMjF019gWJb1kUB7v0NhcuCnYBlTdEo2z_6xkSJj9JCSeOA2SbfzgGB4aIVlQOFbjdAVk7o0_7M7KBB1-0lqzGXIvaLtGazvcBxuJYLKfAhhao16xfFFee6JC0keW57i6v1_oKXrJnf4D7nQF-8bmp9I0wiElEfR_8Q5L-858x2tFLgALKTfROK-LLreCXH2XyNtV7f3CsUrJSkBuwCKlN4iVQugY470lQfLzcU5obvNQh7v864wNldSFkGc2IpgMn25kGj8fT0Nw98W8RSHJOP5_VFcdkOPWP_YqsVqHRdTWp77EpRNRYBow-Ab5movvlu4V11ef7Mplh9lLa6aJ4yPuApvwOAgcsWRKhlVLKLSUef2gtxGKOVqXrCOHPMfqvTjkVkvp0sONv4HX1iXo-mOUNWWUnbOMAMXw7DPKLSimOG5IPXoqLXVB_clj6vsjLHvMgklsMhjW4H3UmiazNyHeuT0fHNdBjMEpA1zktTAQAI47LztTe7GAUtaWtNK-7BUhJvlSNoCnLRBBPPuT9NIl1lb8otuH5ccC6mL1AiOdlRqTUP8usLgJR2cNz2DRu74=w300-h526-no?authuser=6)

