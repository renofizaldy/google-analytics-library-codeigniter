## Google Analytics Library for CodeIgniter 3

### Requirements:

Google API PHP Client : https://github.com/google/google-api-php-client

### Installation:

1. Copy `Google_analytics.php` file into your `/application/libraries/` directory

2. Rename directory from Google-PHP-API-Client as `google-api` and copy into `/application/third_party/`

### Usage:

```html
$this->load->library('google_analytics');

$account = array('email'='YOUR_GA_EMAIL', 'key'=>'YOUR_GA_P12_FILE'); // Required

$time_range = array('start'=>'YYYY-MM-DD', 'end'=>'YYYY-MM-DD'); // Required

$metric = "GA_API_PARAMETER"; // Required -- See parameter and usage on Google Analytics API

$dimension = array(); // Optional -- See parameter and usage on Google Analytics API

$this->google_analytics->getResult($account, $time_range, $metric);
```
