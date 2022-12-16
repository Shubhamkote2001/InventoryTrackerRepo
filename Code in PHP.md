<?php
// User Login
if(isset($_POST['login'])) {
	$username = $_POST['username'];
	$password = $_POST['password'];

	if(username == 'admin' && password == 'admin') {
		//Login Successful
		echo "Login Successful";
	} else {
		//Login Failed
		echo "Login Failed";
	}
}

// User Register
if(isset($_POST['register'])) {
	$username = $_POST['username'];
	$password = $_POST['password'];
	$email = $_POST['email'];

	//Check if user already exists
	$query = mysql_query("SELECT * FROM users WHERE username = '$username'");
	$numrows = mysql_num_rows($query);

	if($numrows == 0) {
		//Insert user into database
		$sql = "INSERT INTO users (username,password,email) VALUES ('$username','$password','$email')";
		$result = mysql_query($sql);
		if($result) {
			echo "Registration Successful";
		} else {
			echo "Registration Failed";
		}
	} else {
		echo "Username already taken";
	}
}

// User Update Profile
if(isset($_POST['update_profile'])) {
	$username = $_POST['username'];
	$password = $_POST['password'];
	$email = $_POST['email'];

	//Update user in database
	$sql = "UPDATE users SET username = '$username', password = '$password', email = '$email' WHERE id = '$id'";
	$result = mysql_query($sql);
	if($result) {
		echo "Update Successful";
	} else {
		echo "Update Failed";
	}
}

// User Change Password
if(isset($_POST['change_password'])) {
	$old_password = $_POST['old_password'];
	$new_password = $_POST['new_password'];

	//Check if old password is correct
	$query = mysql_query("SELECT * FROM users WHERE username = '$username' AND password = '$old_password'");
	$numrows = mysql_num_rows($query);

	if($numrows == 1) {
		//Update user's password in database
		$sql = "UPDATE users SET password = '$new_password' WHERE username = '$username'";
		$result = mysql_query($sql);
		if($result) {
			echo "Password Changed Successfully";
		} else {
			echo "Password Change Failed";
		}
	} else {
		echo "Incorrect Password";
	}
}

// User Forgot Password
if(isset($_POST['forgot_password'])) {
	$username = $_POST['username'];

	//Send verification code to user's email 
	$code = rand(1000,9999);
	$message = "Verification Code : ".$code;
	$to = $email;
	$subject = "Forgot Password Verification";
	$headers = "From: admin@example.com \r\n";
	mail($to,$subject,$message,$headers);

	if(mail) {
		//Update user's verification code
		$sql = "UPDATE users SET code = '$code' WHERE username = '$username'";
		$result = mysql_query($sql);
		if($result) {
			echo "Verification code sent successfully";
		} else {
			echo "Verification code sending failed";
		}
	}
}

// Product Create
if(isset($_POST['create_product'])) {
	$name = $_POST['name'];
	$price = $_POST['price'];
	$category = $_POST['category'];
	
	//Insert product into database
	$sql = "INSERT INTO products (name,price,category) VALUES ('$name','$price','$category')";
	$result = mysql_query($sql);
	if($result) {
		echo "Product Created Successfully";
	} else {
		echo "Product Creation Failed";
	}
}

// Product Update
if(isset($_POST['update_product'])) {
	$name = $_POST['name'];
	$price = $_POST['price'];
	$category = $_POST['category'];
	
	//Update product in database
	$sql = "UPDATE products SET name = '$name', price = '$price', category = '$category' WHERE id = '$id'";
	$result = mysql_query($sql);
	if($result) {
		echo "Product Updated Successfully";
	} else {
		echo "Product Updation Failed";
	}
}

// Product Delete
if(isset($_POST['delete_product'])) {
	$id = $_POST['id'];

	//Delete product from database
	$sql = "DELETE FROM products WHERE id = '$id'";
	$result = mysql_query($sql);
	if($result) {
		echo "Product Deleted Successfully";
	} else {
		echo "Product Deletion Failed";
	}
}

// Product List
if(isset($_POST['list_products'])) {
	//Fetch all products
	$sql = "SELECT * FROM products";
	$result = mysql_query($sql);
	if($result) {
		while($row = mysql_fetch_array($result)) {
			echo $row['name']." - ".$row['price']." - ".$row['category']."<br>";
		}
	} else {
		echo "Failed to fetch products";
	}
}

// Category Create
if(isset($_POST['create_category'])) {
	$name = $_POST['name'];
	
	//Insert category into database
	$sql = "INSERT INTO categories (name) VALUES ('$name')";
	$result = mysql_query($sql);
	if($result) {
		echo "Category Created Successfully";
	} else {
		echo "Category Creation Failed";
	}
}

// Category Delete
if(isset($_POST['delete_category'])) {
	$id = $_POST['id'];

	//Delete category from database
	$sql = "DELETE FROM categories WHERE id = '$id'";
	$result = mysql_query($sql);
	if($result) {
		//Delete all products of the deleted category
		$sql = "DELETE FROM products WHERE category = '$id'";
		$result = mysql_query($sql);
		if($result) {
			echo "Category Deleted Successfully";
		} else {
			echo "Category Deletion Failed";
		}
	} else {
		echo "Category Deletion Failed";
	}
}

// Category Update
if(isset($_POST['update_category'])) {
	$name = $_POST['name'];
	
	//Update category in database
	$sql = "UPDATE categories SET name = '$name' WHERE id = '$id'";
	$result = mysql_query($sql);
	if($result) {
		echo "Category Updated Successfully";
	} else {
		echo "Category Updation Failed";
	}
}

// Category Add Item
if(isset($_POST['add_item'])) {
	$name = $_POST['name'];
	$price = $_POST['price'];
	$category = $_POST['category'];
	
	//Insert product into database
	$sql = "INSERT INTO products (name,price,category) VALUES ('$name','$price','$category')";
	$result = mysql_query($sql);
	if($result) {
		echo "Product Added Successfully";
	} else {
		echo "Product Addition Failed";
	}
}

// Category List
if(isset($_POST['list_categories'])) {
	//Fetch all categories
	$sql = "SELECT * FROM categories";
	$result = mysql_query($sql);
	if($result) {
		while($row = mysql_fetch_array($result)) {
			echo $row['name']."<br>";
		}
	} else {
		echo "Failed to fetch categories";
	}
}
?>
