#SQ Simple Frame Work
##Full Database System
<h3>Connect to database</h3>
<p>In App\Database\Connection.php
<br>change the pdo for Mysql</p>
<code>

return new \PDO("mysql:host=".self::$host.";dbname=".self::$database,self::$username,self::$password);
</code>
##Create Model
<p>Create a class in app\model</p>
<code>

namespace App\Models;

use App\Database\Connection;

use App\Database\Query;

class Author
{
    
    
   private $column=['name'=>"firstName","year"=>'Publish'];
    
   public $table = 'autor';
   
   use Query;
   
   private function createTable()
   
   {
   
   $this->query = "
                    
                    CREATE TABLE IF NOT  EXISTS `author` (
                      `id` int(11) NOT NULL AUTO_INCREMENT,
                      `name` varchar(255) DEFAULT NULL,
                      `year` year(4) DEFAULT NULL,
                      PRIMARY KEY (`id`) ) ";
    }
}

</code>
<strong>In createTable method You should define your database design</strong>

<h1>Create Main File</h1>
<h2>create autor.php</p>
<code>

<h4>Autoload file</h1>
require_once dirname(__FILE__) . "/vendor/autoload.php";

<h4>Create Session CSRF</h1>
$csrf = \Http\Request::session();

<h4>Store Edit Attribute</h1>
$editAttr = null;

// Create Request

function create()

{


$model = $_POST['model'];

    $year = $_POST['year'];

    (new \App\Models\car())->create(

        [
            'model' => $model,
            'year' => $year
        ])->runQuery();
}

\Http\Request::handle_post('create', $csrf);


// Delete Request

function delete()

{

    $id = $_GET['id'];
    (new \App\Models\car())->delete()->where('id', $id)->runQuery();
}

\Http\Request::handle_delete('delete', $csrf);

// Edit Request

function edit()
{

    global $editAttr;
    $editAttr = (new \App\Models\car())->select()->where('id', $_GET['id'])->get();
}

\Http\Request::handle_edit('edit');

// Update Request

function update()
{
 
    (new \App\Models\car())->update(['model' => $_POST['model'], 'year' => $_POST['year']])->where('id',$_GET['id'])->runQuery();
}


\Http\Request::handle_update('update');

$cars = (new \App\Models\Car())->all();

</code>

