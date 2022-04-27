# vue-js-communication-box
Demo of the communication box programmed with Vue JS for Docket TMLS application. Code is reactive, organized, and maintainable.

To init, the `index.vue` component makes an HTTP GET request to the backend, retrieving a json of all messages that belong to the selected 'trip'. This data is then set to the `messages` property, defined in the data hook. `this.messages` is then passed to child component `./MessagesSection.vue` which iterates through the array, sending each to `inc/message.vue` sub-component for final processing before display.

```javascript
async getMessages(id) {
  const response = await axios.get(
    `/api/messages?trip_id=${id}`,
    this.$store.getters["config/GET"]
  );
  return response.data;
},
```


When sending, the component makes an Http post request to the backend and then receives a message as an object back. The object is then pushed to the array of messages, reactively displaying the new message to the user.
![Image One](https://lh3.googleusercontent.com/elkfewsCmUQ-9qcJawjtkflv5131cHNfIcEGHoCpdXd_-Etv-hRBRJNPLNOdP72QjyNju5ExerOKkMkNGpotL4kXGLtvYdEHk3ucVx8wE9vc-s0IFTIZB0ppUZEjQ3vRsAtHMVmqiHUCx1dPhL9NNIvkQ5uMpi5XBj4tBakipskHWvqH9bDxkSCyl2j33x15zJZRJem7eUaAhOCsfB1cstrocoDFRx64zF-vLh2629jeRgJmtEi0OIGS8nPtq604Mjm78ehA8oGnIo2WgXsr00G0eNha9vkhcYZ5Zo4h949M1ICC4x3-8iScSyWwGld-JH8dNWNGH3-AIHcNWGT2GcLFpD1C8uYiqhTmQwK84S_JY3fJ040rv8HIyoCAHeVziUb9OVDB5BpTKqbWwM7i6psNKOISRxTCmaY55eYv9fSMq4RQRhBHWlZc8CdI8biAeoNgpIU2z_YqQOA4qg8bQwZUTRmQE4WRogjtAmMMPQcyjKq9tM5d9RRxeZIZuNCibWp2ArE5bbZSPcUKcTWRw1wLwQlDMqZn4MswYcgXebvQ2r51DF03lk7QpFXwPVzMeoskZA1HMeOQZKblxI0b2tkqFJMTt6AZdkjZPVM6qJNEXApcfgdSUM8z5NCbE2JpVR5ZkE0IqWcxJoPARccEpgX3Wv7XuO64DZb0W3QHr9d6_PRNA45llPNr-mlibQKgcCkroenOiTTAz2JO_i5os4M=w427-h809-no?authuser=6)
![Image Two](https://lh3.googleusercontent.com/At8XA4yh-xiht8QHbIKOScsq__BmFGdnhA_tosgqOIIXieDrJMNoxrfF6fv2h-fj3DaAWdOVPRXqib650AHYEI2h9PqRW8n0-R1Sv8j9Y7R4YSYzY2rqlHQd2Gzo3ImNquloaknU5WQgv4W1WZTQMjF019gWJb1kUB7v0NhcuCnYBlTdEo2z_6xkSJj9JCSeOA2SbfzgGB4aIVlQOFbjdAVk7o0_7M7KBB1-0lqzGXIvaLtGazvcBxuJYLKfAhhao16xfFFee6JC0keW57i6v1_oKXrJnf4D7nQF-8bmp9I0wiElEfR_8Q5L-858x2tFLgALKTfROK-LLreCXH2XyNtV7f3CsUrJSkBuwCKlN4iVQugY470lQfLzcU5obvNQh7v864wNldSFkGc2IpgMn25kGj8fT0Nw98W8RSHJOP5_VFcdkOPWP_YqsVqHRdTWp77EpRNRYBow-Ab5movvlu4V11ef7Mplh9lLa6aJ4yPuApvwOAgcsWRKhlVLKLSUef2gtxGKOVqXrCOHPMfqvTjkVkvp0sONv4HX1iXo-mOUNWWUnbOMAMXw7DPKLSimOG5IPXoqLXVB_clj6vsjLHvMgklsMhjW4H3UmiazNyHeuT0fHNdBjMEpA1zktTAQAI47LztTe7GAUtaWtNK-7BUhJvlSNoCnLRBBPPuT9NIl1lb8otuH5ccC6mL1AiOdlRqTUP8usLgJR2cNz2DRu74=w300-h526-no?authuser=6)

