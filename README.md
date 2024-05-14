# Cloud Functions File Forwarding API

This Node.js project is designed to handle `multipart/form-data` upload requests in a Google Cloud Function environment. The code utilizes the `busboy` library to parse multipart requests, processes uploaded files, and forwards them to a specified external API endpoint.

## Prerequisites

- Node.js installed locally for development.
- Google Cloud SDK installed and configured.
- An account on Google Cloud Platform.

## Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/xprilion/cloud-functions-file-forwarding-api.git
   cd cloud-functions-file-forwarding-api
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

## Deployment

Deploy the function to Google Cloud Functions using the following command:

```bash
gcloud functions deploy uploadFile --allow-unauthenticated --trigger-http --runtime=nodejs20 --entry-point=uploadFile
```

### Explanation of Deployment Flags:

- `--allow-unauthenticated`: Allows unauthenticated HTTP requests to access the function. For production, consider securing your function.
- `--trigger-http`: Sets the function to be triggered via HTTP requests.
- `--runtime=nodejs20`: Specifies the runtime environment. Google Cloud Functions supports various Node.js versions; replace `nodejs20` with the desired version.
- `--entry-point=uploadFile`: Specifies the function within your code to execute when the function is triggered.

For more details on deploying to Google Cloud Functions and additional configurations, refer to the [official documentation](https://cloud.google.com/functions/docs/deploying).

## Usage

Once deployed, the function will be accessible via the URL provided by Google Cloud Platform. Send `POST` requests with `multipart/form-data` content to this URL to upload files. The files are processed and forwarded to the specified external API endpoint.

### Example:

#### Curl:

```bash
curl --location 'https://xxxxxxxxxxx.cloudfunctions.net/yourfunctionname' \
--form 'file=@"/Users/username/folder/filename.pdf"'
```

#### Python:
```python
import requests

url = "https://xxxxxxxxxxx.cloudfunctions.net/yourfunctionname"

files=[
  ('file',('Ankana_Chakraborty_Resume.pdf',open('/Users/username/folder/filename.pdf','rb'),'application/pdf'))
]
headers = {}

response = requests.request("POST", url, headers=headers, files=files)

print(response.text)
```

#### JavaScript

```javascript
const formdata = new FormData();
formdata.append("file", fileInput.files[0], "filename.pdf");

const requestOptions = {
  method: "POST",
  body: formdata,
  redirect: "follow"
};

fetch("https://xxxxxxxxxxx.cloudfunctions.net/yourfunctionname", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.error(error));
```

## Contributing

Contributions are welcome. Please open an issue first to discuss what you would like to change or submit a pull request with your suggestions.

## License

This project has an MIT license.
