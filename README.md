
# Chatbot


### DialogFlow Setup
  - Create agent in DialogFlow
  - Create Custom intent for that agent
  - Add keywords to the training
  - Enable webhook for the custom intent
  - Create Flask App for the Fulfillment of the custom intent
  - Install ngrok in your local
  - run your flask app and ngrok
  - attach the ngrok url to the webhook url then save
  - Test the agent

### Kommunicate integration

Frontend for chat app: `http://resty-chatbot.com.s3-website-ap-southeast-1.amazonaws.com/`

Webhook flask app url: `https://test-chatbot-rjt.herokuapp.com/webhook` (deployed in heroku) 

Komunicate app id: `https://widget.kommunicate.io/chat?appId=201b88b52948f69ac0cadb2a8a8b7cbdc`


Note:
```
ngrok http 8000 > /dev/null &
curl -s localhost:4040/api/tunnels | jq -r .tunnels[0].public_url
gunicorn3 app:app --daemon
