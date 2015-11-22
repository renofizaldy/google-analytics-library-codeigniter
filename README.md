# google-analytics-library-codeigniter
Simple google analytics library to use in CodeIgniter 3

Usage: 

$this->load->library('google_analytics');

$account = array('email'='YOUR_GA_EMAIL', 'key'=>'YOUR_GA_P12_FILE');

$time_range = array('start'=>'YYYY-MM-DD', 'end'=>'YYYY-MM-DD');

$metric = (string) GA_API_PARAMETER;

$dimension = array(); // Optional

$this->google_analytics->getResult($account, $time_range, $metric);
