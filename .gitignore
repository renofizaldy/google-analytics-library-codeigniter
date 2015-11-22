<?php if(!defined('BASEPATH')) exit('No direct script access allowed');

class Google_analytics {

	private $library = '/third_party/google-api/src/Google/autoload.php';

	private function getService($email, $key) {
		// Creates and returns the Analytics service object.

		// Load the Google API PHP Client Library.
		require_once APPPATH.$this->library;

		// Use the developers console and replace the values with your
		// service account email, and relative location of your key file.
		$service_account_email = $email;
		$key_file_location = $key;

		// Create and configure a new client object.
		$client = new Google_Client();
		$client->setApplicationName("GoogleAnalytics");
		$analytics = new Google_Service_Analytics($client);

		// Read the generated client_secrets.p12 key.
		$key = file_get_contents($key_file_location);
		$cred = new Google_Auth_AssertionCredentials(
				$service_account_email,
				array(Google_Service_Analytics::ANALYTICS_READONLY),
				$key
		);
		$client->setAssertionCredentials($cred);
		if($client->getAuth()->isAccessTokenExpired()) {
			$client->getAuth()->refreshTokenWithAssertion($cred);
		}

		return $analytics;
	}

	private function getFirstprofileId(&$analytics) {
		// Get the user's first view (profile) ID.

		// Get the list of accounts for the authorized user.
		$accounts = $analytics->management_accounts->listManagementAccounts();

		if (count($accounts->getItems()) > 0) {
			$items = $accounts->getItems();
			$firstAccountId = $items[0]->getId();

			// Get the list of properties for the authorized user.
			$properties = $analytics->management_webproperties
					->listManagementWebproperties($firstAccountId);

			if (count($properties->getItems()) > 0) {
				$items = $properties->getItems();
				$firstPropertyId = $items[0]->getId();

				// Get the list of views (profiles) for the authorized user.
				$profiles = $analytics->management_profiles->listManagementProfiles($firstAccountId, $firstPropertyId);

				if (count($profiles->getItems()) > 0) {
					$items = $profiles->getItems();

					// Return the first view (profile) ID.
					return $items[0]->getId();

				} else {
					throw new Exception('No views (profiles) found for this user.');
				}
			} else {
				throw new Exception('No properties found for this user.');
			}
		} else {
			throw new Exception('No accounts found for this user.');
		}
	}

	public function getResult($account, $time_range, $metric, $dimension=null) {
		/*
			$account = array('email'='YOUR_GA_EMAIL', 'key'=>'YOUR_GA_P12_FILE');

			$time_range = array('start'=>'YYYY-MM-DD', 'end'=>'YYYY-MM-DD');

			$metric = (string) GA_API_PARAMETER;

			$dimension = array();
		*/

		$analytics = $this->getService($account['email'], $account['key']);
		$profile   = $this->getFirstprofileId($analytics);

		if (is_null($dimension) || empty($dimension) || !isset($dimension)) {
			$result= $analytics->data_ga->get(
				'ga:'.$profile,
				$time_range['start'],
				$time_range['end'],
				$metric
			);
		} else {
			$result= $analytics->data_ga->get(
				'ga:'.$profile,
				$time_range['start'],
				$time_range['end'],
				$metric,
				$dimension
			);
		}

		return $result->getRows();
	}

} ?>
