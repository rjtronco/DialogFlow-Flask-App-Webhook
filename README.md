#  DialogFlow ChatBot

Reference: https://www.kommunicate.io/blog/create-chatbot-in-flask-and-python/

## Highlights

🍭 Creating a Chatbot using DialogFlow
- Creating an agent in Dialogflow
- Train the chatbot to for some keywords
- Integrate a Flask app webhook to the chatbot

🍭 Integrating the ChatBot to a [WebApp](http://resty-chatbot.com.s3-website-ap-southeast-1.amazonaws.com/)
- Utilizing `ngrok` in creating a webserver for our Flask app locally
- ChatBot integration in Komunicate
- Integration of the Komunicate chat app to a WebUI


🍭 [Adding PreCommit hooks to your repo](https://github.com/rjtronco/DialogFlow-Flask-App-Webhook/blob/main/pre-commit.md)
- Utilizing `ngrok` in creating a webserver for our Flask app
- ChatBot integration in Komunicate
- Integration of the Komunicate chat app to a WebUI


## How it works

Create an agent using Dialog flow. You can follow the [documentation/reference](https://www.kommunicate.io/blog/create-chatbot-in-flask-and-python/).

Set keywords and/or expression to train your chatbot

Integrating a Flask app webhook for the ChatBot Fulfilment. The endpoint is `/webhook'. 
I have created a sample return message for various keywords that might be used. 

```python
@app.route('/webhook', methods=['POST'])
def webhook():
    query = request.get_json(force=True)
    print("Reached!")
    sample_return_messages = {
        "bye":['bye ka rin!','k bye!'],
        "supot":["supot ka ba?","baka ikaw supot?","kausap ko supot. haha"],
        "mama":["your mom!","mama mo"],
        "ha":["hakdog","hakdog ka"]
    }

    queryText = str(query['queryResult']['queryText'])

    explode_str = queryText.split(" ")

    for i in explode_str:
        if i in sample_return_messages:
            # randomize from list what to return
            rand_index = random.randint(0,len(sample_return_messages[i])-1)
            message = sample_return_messages[i][rand_index]
            return {
                'fulfillmentText': message
            }


    return {
        'fulfillmentText': 'Hello from the bot world supot!'
    }

```


Komunicate Integration
 
You can integrate your DialogFlow chatbot in Kommunicate to make it useable in a WebUI. You can follow this [documentation](https://www.kommunicate.io/blog/integrate-bot-using-dialogflow-in-kommunicate/)


Creating and deploying the webUI. This is just a simple html file with the `<iframe` tag from the Kommunicate integration.
```html
<!DOCTYPE html>
<html>
<head>
<title>Page Title</title>
</head>
<body>

<h1>Resty Chatbot</h1>
<iframe
        style="border: none;"
        height="600px"
        width="400px"
        src="https://widget.kommunicate.io/chat?appId=201b88b52948f69ac0cadb2a8a8b7cbdc"
        allow="microphone; geolocation;"
        >
    </iframe>
</body>
</html>

```

### Testing
  - Access the webUI and try chatting with the bot. Some keywords/phrase are `demo`,`python demo`,`bye` etc


### Kommunicate integration

Webhook flask app url: `https://test-chatbot-rjt.herokuapp.com/webhook` (deployed in heroku) </br>
Komunicate app id: `https://widget.kommunicate.io/chat?appId=201b88b52948f69ac0cadb2a8a8b7cbdc` </br>




Extra Note:

used in ec2
```
ngrok http 8000 > /dev/null &
curl -s localhost:4040/api/tunnels | jq -r .tunnels[0].public_url
gunicorn3 app:app --daemon
