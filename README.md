# PHP Router in 140 Characters

This is a dimple(damn simple) URL routing script for PHP which is written in just 140 characters of code, so it fits within a tweet.

Its NOT a good router at all, **don't use it on a real application**, its not exception handled either. I did it just for fun and to demonstrate the simplicity

So here's the router code, and that's all (seriously).
```PHP
class R{
function a($r,callable $c){$this->r[$r]=$c;}
function e(){$s=$_SERVER;$i='PATH_INFO';$p=isset($s[$i])?$s[$i]:'/';$this->r[$p]();}
}
```

## Usage
Create a file index.php in your server root and try this code
```PHP
<?php
// The router code
class R{
function a($r,callable $c){$this->r[$r]=$c;}
function e(){$s=$_SERVER;$i='PATH_INFO';$p=isset($s[$i])?$s[$i]:'/';$this->r[$p]();}
}
//


// Create 
$router = new R();

// Add a route with a callback function
$router->a('/a', 'callbackFunction');

// Add a route with a closure
$router->a('/b', function(){
    echo 'Hello B';
});

// Add homepage route
$router->a('/', function(){
	echo 'Hello World';
});

// Add route with class method
$router->a('/c', [new Foo, 'bar']);
// Add multiple slashed route with class method
$router->a('/c/d', [new Foo, 'bar']);

// Execute the route
$router->e();

// Callback handlers
function callbackFunction(){
	echo 'Hello A';
}

class Foo{
	function bar(){
		echo 'Hello Bar';
	}
}
```

Now visit your server root `http://localhost/index.php`, `http://localhost/index.php/a`, `http://localhost/index.php/b`, `http://localhost/index.php/c` and `http://localhost/index.php/c/d`.

Or you may run built-in PHP server from the command line (in the same dir)
```
php -S localhost:8081
```
and visit `http://localhost:8081/index.php`.

Runs on 5.4+. 140 chars idea is inspired by Fabien Potencier's [Twittee](http://twittee.org/).
