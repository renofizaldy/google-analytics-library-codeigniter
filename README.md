# google-analytics-library-codeigniter
Simple google analytics library to use in CodeIgniter 3

Copy 'Google_analytics.php' file to your '/application/libraries' directory

Set Google-API-PHP-Client directory location inside 'Google_analytics.php'

Usage on Controller: 

$this->load->library('google_analytics');

$account = array('email'='YOUR_GA_EMAIL', 'key'=>'YOUR_GA_P12_FILE'); // Required

$time_range = array('start'=>'YYYY-MM-DD', 'end'=>'YYYY-MM-DD'); // Required

$metric = "GA_API_PARAMETER"; // Required -- See parameter and usage on Google Analytics API

$dimension = array(); // Optional -- See parameter and usage on Google Analytics API

$this->google_analytics->getResult($account, $time_range, $metric);
