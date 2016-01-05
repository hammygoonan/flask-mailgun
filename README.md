# Flask-Mailgun

[Flask-Mailgun](https://github.com/sleekslush/flask-mailgun) Adds [Mailgun](https://mailgun.com/) support to Flask applications.

## Quick start

For the common case of having one Flask application all you have to do is to create your Flask application, load the configuration of choice and then create the Mailgun object by passing it the application:

```
from flask import Flask
from flask_mailgun import Mailgun

app = Flask(__name__)
app.config['MAILGUN_DOMAIN'] = 'http://example.com'
app.config['MAILGUN_API_KEY'] = 'yourmailgunapikey'
mailgun = Mailgun(app)
```

You can then go ahead an send email using Mailgun anywhere in your app.

```
from yourapplication import mailgun

response = mailgun.send_email(
    data={
        "from": "Excited User <mailgun@YOUR_DOMAIN_NAME>",
        "to": ["bar@example.com", "YOU@YOUR_DOMAIN_NAME"],
        "subject": "Hello",
        "text": "Testing some Mailgun awesomness!"
    },
    files=[
        ("attachment", open("files/test.jpg")),
        ("inline", open("files/inline_test.jpg"))
    ]
)

print(response)
# {
#    "message": "Queued. Thank you.",
#    "id": "<20111114174239.25659.5817@samples.mailgun.org>"
# }
```

## Configuration

Two variables are required for the module to work:
* **MAILGUN_DOMAIN:** The domain you're sending emails from (configured in Mailgun)
* **MAILGUN_API_KEY:** API key provided by Mailgun
