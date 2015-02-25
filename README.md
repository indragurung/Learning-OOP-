# Learning-OOP-
<?php 

require_once 'core/init.php';

if(Input::exists('post')) {
	$validate = new Validate();
	$validation = $validate->check($_POST,array(
		'username'		=> array(
			'required'	=> true,
			'min'		=> 2,
			'max'		=> 32,
			'unique'	=> 'users'
		),

		'password'		=> array(
			'required'	=> true,
			'min'		=> 5,
			'max'		=> 32,
		),

		'password_again'	=> array(
			'required'		=> true,
			'min'			=> 5,
			'max'			=> 32,
			'matches'		=> 'password'
		),

		'name'			=> array(
			'required'	=> true,
			'min'		=> 2,
			'max'		=> 50
		)
	));

	if($validate->passed()) {
		echo "Passed";
	} else {
		foreach($validate->errors() as $errors)
		{
			echo $errors,'<br>';
		}
	}
}


?>


<form action="" method="post">
	<label for="username">Username: </label>
	<input type="text" name="username" value="<?php echo Input::get('username'); ?>">
	<br> <br>

	<label for="password">Password: </label>
	<input type="password" name="password">
	<br> <br>

	<label for="password_again">Password Again: </label>
	<input type="password" name="password_again">
	<br> <br>

	<label for="name">Name: </label>
	<input type="text" name="name" value="<?php echo Input::get('name'); ?>">
	<br> <br>

	<input type="hidden" name="token" value="<?php echo Token::generate(); ?>">

	<button>Submit</button>
</form>
