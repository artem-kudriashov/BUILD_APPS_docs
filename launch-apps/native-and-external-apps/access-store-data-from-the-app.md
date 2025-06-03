# Access store data from the app

When users install or open your Native app, Ecwid calls **iframeUrl** with an additional encrypted `payload` query param. As a result, users get to the settings page, and you receive a payload with all the information required to work with a store.

Payload contains store ID, access token, and current store language. **iframe URL** call example:

`https://www.example.com/my-app-iframe-page?payload=353035362c226163636573735f746f6b656e223a22776d6`

Here the `353035362c226163636573735f746f6b656e223a22776d6` is the encrypted payload value with information about the store. Decrypt it to receive _store ID_ and _access token_ required for REST API access.

Your application needs an **access token** for the Ecwid REST API to read and modify Ecwid store orders, products, and other information.

### Decrypt the payload from the Ecwid admin

Ecwid uses _AES-128_ encryption and _base64_ encoding. The encryption key is the first 16 symbols (128 bit) of your app's **client\_secret**.

For correct payload decryption in C#, create additional padding to make the payload a multiple of 4:

`base64 = base64.PadRight(base64.Length + (4 - (base64.Length % 4)), '=');`

Use one of the following examples as a template for your application:

{% tabs %}
{% tab title="PHP" %}
```php
<?php
//
//  Get and decrypt the payload from Ecwid
//

// authenticate user in iframe page
function getEcwidPayload($app_secret_key, $data) {
  // Get the encryption key (16 first bytes of the app's client_secret key)
  $encryption_key = substr($app_secret_key, 0, 16);

  // Decrypt payload
  $json_data = aes_128_decrypt($encryption_key, $data);

  // Decode json
  $json_decoded = json_decode($json_data, true);
  return $json_decoded;
}

function aes_128_decrypt($key, $data) {
  // Ecwid sends data in url-safe base64. Convert the raw data to the original base64 first
  $base64_original = str_replace(array('-', '_'), array('+', '/'), $data);

  // Get binary data
  $decoded = base64_decode($base64_original);

  // Initialization vector is the first 16 bytes of the received data
  $iv = substr($decoded, 0, 16);

  // The payload itself is is the rest of the received data
  $payload = substr($decoded, 16);

  // Decrypt raw binary payload
  $json = openssl_decrypt($payload, "aes-128-cbc", $key, OPENSSL_RAW_DATA, $iv);
  //$json = mcrypt_decrypt(MCRYPT_RIJNDAEL_128, $key, $payload, MCRYPT_MODE_CBC, $iv); // You can use this instead of openssl_decrupt, if mcrypt is enabled in your system

  return $json;
}

// Get payload from the GET and process it
$ecwid_payload = $_GET['payload'];
$client_secret = "secret_0123abcd4567efgh1234567890"; // This is a dummy value. Place your client_secret key here. You received it from Ecwid team in email when registering the app 

$result = getEcwidPayload($client_secret, $ecwid_payload);

// Get store info from the payload
$token = $result['access_token'];
$storeId = $result['store_id'];
$lang = $result['lang'];
$viewMode = $result['view_mode'];

if (isset($result['public_token'])){
  $public_token = $result['public_token'];
}

// URL Encoded App state passed to the app
if (isset($_GET['app_state'])){
  $app_state = $_GET['app_state'];
}

//
//  Get store specific data
//

// Get store specific data from storage endpoint
$key = 'color';

$url = 'https://app.ecwid.com/api/v3/' .$storeId. '/storage/' .$key. '?token=' .$token;

$ch = curl_init();

curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_URL,$url);

$curlResult = curl_exec($ch);
curl_close($ch);

$curlResult = (json_decode($curlResult));
$color = $curlResult -> {'value'};

  if ($color !== null ) {
    // set color from storage
    } else {
    // set default colors
  }


//
//  Start the flow of your application
//  ...
?>
```


{% endtab %}

{% tab title="C#" %}
```csharp
public Dictionary<String, Object> DecodePayload(string payload)
{
    byte[] encryptionKey = System.Text.Encoding.ASCII.GetBytes(Environment.GetEnvironmentVariable("ECWID_CLIENT_SECRET").Substring(0, 16));

    string original = payload.Replace("-", "+").Replace("_", "/");

    byte[] decoded = Convert.FromBase64String(original.PadRight(original.Length + (4 - (original.Length % 4)), '='));

    string decodedData = Encoding.UTF8.GetString(decoded
    );

    Aes aes = new AesManaged
    {
        Key = encryptionKey,
        IV = Encoding.ASCII.GetBytes(decodedData.Substring(0, 16)),
        Mode = CipherMode.CBC
    };

    using (ICryptoTransform cipher = aes.CreateDecryptor())
    {
        string decrypted;

        using (MemoryStream memoryStream = new MemoryStream(decoded))
        {
            using (CryptoStream cryptoStream = new CryptoStream((Stream)memoryStream, cipher, CryptoStreamMode.Read))
            {
                using (StreamReader streamReader = new StreamReader((Stream)cryptoStream))
                {
                    decrypted = streamReader.ReadToEnd();
                }
            }
        }

        return JsonConvert.DeserializeObject<Dictionary<String, Object>>(decrypted.Substring(15));
    }

}
```


{% endtab %}
{% endtabs %}

### Get API access data from the payload&#x20;

After you decrypt and parse the payload, you'll get a JSON with some information about the store:

```json
{
  "store_id": 1234567,
  "lang": "en",
  "access_token":"secret_ab***cd",
  "view_mode":"PAGE",
  "public_token":"public_ASDlkDASmasdaslkdASkndasANJKLsAf"
}
```

Available fields:

| Name          | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| store\_id     | number | Ecwid store ID in which the app is opened                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| lang          | string | Current Ecwid admin language (ISO 639-1). Use it to translate your application UI.                                                                                                                                                                                                                                                                                                                                                                                                      |
| access\_token | string | Access token (**secret\_token**) for REST API requests.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public\_token | string | <p>Public access token (<strong>public_token</strong>) for REST API requests.<br><br>Safe to use on the storefront.</p>                                                                                                                                                                                                                                                                                                                                                                 |
| view\_mode    | string | <p>Mode used to display the application interface.<br><br>One of: </p><p><code>POPUP</code> - App is displayed in a popup on any Ecwid admin page (currently disabled).</p><p><code>PAGE</code> - App is loaded inside the iframe block on a separate page in Ecwid admin (default behavior).</p><p><code>INLINE</code> - app is displayed inside another Ecwid admin page. For example: payment applications can work inside the "Payments" page where the iframe size is smaller.</p> |

### Use REST API to get the data you need

Once you have the _store ID_ and _access token_, make REST API requests to receive all required details for the app to start working. For example:

* Get user data saved in App storage to display personal settings.
* Get customer emails for making a custom newsletter
* If some customers made orders, call REST API _/orders/{orderId}_ to receive order details and use these details to enhance email personalization.
