# Codeigniter AWS Library

Helper functions for DynamoDB and SES.

## Installation

[Install the AWS PHP SDK](https://docs.aws.amazon.com/sdk-for-php/v3/developer-guide/getting-started_installation.html)

Copy `application/*` to your CodeIgniter application directory.

## Configuration

Enter your AWS keys and region in `application/config/aws_sdk.php`.

## Usage

Load the DynamoDB and SES libraries as needed.

```php
$this->load->library('aws_dynamodb');
$this->load->library('aws_ses');
```

## DynamoDB Methods

### aws_dynamodb->batchGetItem( str $tableName, array $data, bool $consistentRead=TRUE )

Get items with multiple hash IDs with a single query, returns Responses object or FALSE on failure. The `$consistent_read` parameter is optional, defaults to TRUE.

```php
$this->aws_dynamodb->batchGetItem(
	'MyTableName',
	array(
		array('itemID' => '9e37ce4b-4cf1-46b0-b1f8-8dd4847d8809'),
		array('itemID' => '9e0276ff-2708-47fd-82ac-81b0e9f49aa8'),
		array('itemID' => 'be87a02e-6db3-4012-8046-17372632827b'),
	),
	TRUE
);
```

### aws_dynamodb->getCount( str $tableName )

Count the number of items in a table.

```php
$this->aws_dynamodb->getCount('MyTableName');
```

### aws_dynamodb->getItem( str $tableName, array $data, bool $consistent_read=TRUE )

Get a single item from a table, returns Response object or FALSE on failure. The `$consistent_read` parameter is optional, defaults to TRUE.

```php
$this->aws_dynamodb->getItem(
	'MyTableName',
	array(
		'itemID' => '9e37ce4b-4cf1-46b0-b1f8-8dd4847d8809',
	),
	TRUE
);
```

### aws_dynamodb->putItem( str $tableName, array $data )

Insert a single item into a table, returns Response object or FALSE on failure.

```php
$this->aws_dynamodb->putItem(
	'MyTableName',
	array(
		'itemID' => '9e37ce4b-4cf1-46b0-b1f8-8dd4847d8809',
		'attribute' => 'option',
		'attribute2' => 'option2',
	),
	TRUE
);
```

## SES Methods

### aws_ses->send( str $from, array $to, str $subject, str $message, array $reply_to )

Send an email via SES. The `$to` and `$reply_to` parameters can be an array or string, returns bool on success/failure. The `$reply_to` parameter is optional.

```php
$this->aws_ses->send(
	'from@domain.com',
	array(
		'to@domain1.com,
		'to@domain2.com'
		'to@domain3.com',
	),
	'My Subject',
	'My HTML Message',
	array(
		'from@domain1.com,
		'from@domain2.com'
	),
);
```
