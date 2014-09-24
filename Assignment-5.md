## File Cleansing and Loading

This is a small walk through that prepares us to use php to load json data into a `Redis` key value store. As of now, it's really an assignment to remove the "bad" characters that are plaguing our json data. After we get over that hurdle, then we can load the data into `Redis`.

### What you need to accomplish

- On your server add a user called `redis`

```
$ useradd redis
```

- In `/home/redis` create a folder called `data` and copy `nutrition.json` into that folder (http://107.170.214.232/nutrition.json)
- You can split `nutrition.json` if you like, or leave it at `65mb`.
- Create a script called `process_json.???` replacing the `???` with whatever scripting language you use (php, py, etc.) and place it in `/home/redis`.
- When I run your script, it should process `nutrition.json` (or the smaller split files) and do the following:
    - Remove any characters that are not ascii (subset of UTF-8).
    - Display the illegal characters with the line number where it was found.
    - Display how many lines processed in total.
    - Display how many characters removed.
    - Display the list of unique characters removed (I think it's one).

Below are some helpful resources:

### Installing Redis

- Here is a Digital Ocean tutorial on installing Redis:

https://www.digitalocean.com/community/tutorials/how-to-install-and-use-redis

- In addition, you need to install php5-dev on your server 

```bash
sudo apt-get update

sudo apt-get updgrade

apt-get install php5-dev
```

- Clone the following repository onto your server:

https://github.com/nicolasff/phpredis.git

Then `cd phpredis` (change into the directory you just cloned).

```
sudo phpize5

sudo ./configure

sudo make 

sudo make test

sudo make install
```

### Some helpful links

- Json Decode
    - http://de2.php.net/manual/en/function.json-decode.php
- Check Character Encoding
    - http://php.net/manual/en/function.mb-detect-encoding.php
- Split file into so many lines
    - split -l 500 myfile segment
- Json validator web site
    - http://jsonlint.com/

```php
<?php
//Turn on errors
ini_set('display_errors',1);
ini_set('display_startup_errors',1);
error_reporting(-1);

//Create a new Redis object
//Not used YET
$redis = new Redis();

//Scan the directory with our data placing each filename into an array
$dir = scandir('./data');

//Remove the '.' and the '..'
array_shift($dir);
array_shift($dir);

//Loop through the directory array and process each file
foreach($dir as $file){

   //Open file
	 $fp = fopen('./data/'.$file,"r");

   //Start line count at zero
	 $line = 0;
	 
	 //While there are still lines to read
	 while (($buffer = fgets($fp, 4096)) !== false) {
	 
	    //Get a line
		  $buffer = iconv('ASCII', 'UTF-8//IGNORE', $buffer);
		  
		  //Try to decode it (turns json into a php array)
		  $json = json_decode($buffer);
		
		  //Show any errors as they occur
		  if(json_last_error()){
			  echo $file." ".$line." ".JsonError(json_last_error())." ".mb_detect_encoding($buffer)."\n";
		  }
		  
		  $line++;
	 }
	 fclose($fp);
	 
	 //This breaks and only runs ONE file right now.
	 break;
}


//Function to give a "string" error for any json errors
function JsonError($val){
    switch ($val) {
        case JSON_ERROR_NONE:
            return ' - No errors';
        break;
        case JSON_ERROR_DEPTH:
            return ' - Maximum stack depth exceeded';
        break;
        case JSON_ERROR_STATE_MISMATCH:
            return ' - Underflow or the modes mismatch';
        break;
        case JSON_ERROR_CTRL_CHAR:
            return ' - Unexpected control character found';
        break;
        case JSON_ERROR_SYNTAX:
            return ' - Syntax error, malformed JSON';
        break;
        case JSON_ERROR_UTF8:
            return ' - Malformed UTF-8 characters, possibly incorrectly encoded';
        break;
        default:
            return ' - Unknown error';
        break;
    }
}
```
http://www.commandlinefu.com/commands/view/3802/to-print-a-specific-line-from-a-file
