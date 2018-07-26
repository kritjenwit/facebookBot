
# FacebookBot
Facebook bot is created by using PHP. And this is a simple and also sample to build a bot from facebook messenger.

# How to make it work
#### What all you need is https server and curl skill

### code for verify token
create a file named as what you want in my case i will write webhook.php. And then write this code

```
if(isset($_GET['hub_mode']) && isset($_GET['hub_challenge']) &&  isset($_GET['hub_verify_token'])){

        if($_GET['hub_verify_token'] == 'pokemon'){

            echo $_GET['hub_challenge'];

        }
  }
  
  http_response_code(200);
```
### Next step
First move http_response_code(200); to the end of the line
```
define('ACCESS_TOKEN',<YOUR ACCESS TOKEN>',true);
$input = json_decode(file_get_contents('php://input'), true);
$senderId = $input['entry'][0]['messaging'][0]['sender']['id'];
$message = trim(strtolower($input['entry'][0]['messaging'][0]['message']['text']));
$answer = '...';
if($message == 'hello'){
  $response = [
        'recipient' => array(
            'id' => $senderId
        ),
        'message' => array(
            'text' => $answer
        )
    ];
}
$ch = curl_init('https://graph.facebook.com/v3.0/me/messages?access_token=' . ACCESS_TOKEN);
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($response));
curl_setopt($ch, CURLOPT_HTTPHEADER, ['Content-Type: application/json']);
curl_exec($ch);
curl_close($ch);
http_response_code(200);
```
and test the bot
