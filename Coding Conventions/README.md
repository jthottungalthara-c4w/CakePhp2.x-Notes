<h1>CODING CONVENTIONS IN CAKEPHP</h1>

Before we start with any type of coding conventions, I would prefer to go through some links

1.[http://www.codeproject.com/Articles/22769/Introduction-to-Object-Oriented-Programming-Concep][ObjectOrientedConcept]
[ObjectOrientedConcept]: http://www.codeproject.com/Articles/22769/Introduction-to-Object-Oriented-Programming-Concep

2.[http://book.cakephp.org/2.0/en/index.html][Cake Book]
[Cake Book]: http://book.cakephp.org/2.0/en/index.html

The Cake PHP is one of the PHP framework created in MVC architecture. It follows all MVC conventions in coding.  Cake PHP consist of three layers.

![Click Here To See : MVC Architecture] (https://github.com/webonise/CakePhp2.x-Notes/blob/master/Coding%20Conventions/Model-View-Controller-Architecture.png)

1. [Model](https://github.com/webonise/CakePhp2.x-Notes/tree/master/Coding%20Conventions#model)

2. [View](https://github.com/webonise/CakePhp2.x-Notes/tree/master/Coding%20Conventions#view)

3. [Controller](https://github.com/webonise/CakePhp2.x-Notes/tree/master/Coding%20Conventions#controller)

Lets take a look at following coding conventions in CakePHP

<h3>MODEL</h3>

Modals are mostly responsible for data fetching and associations. But it is not all of its functionality. It is also responsible for the business logic of the application. All the business login is been handled in modal side of the code. Creating associations, saving , updating , deleting data, and fetching data from tables are the basic functionality of the modal in Cake PHP

Creating any table in DB, following conventions should be followed

1. The ID of the table must be kept as its first field and must have primary key.
2. The associated table ID should come next to the ID of the table with the table name i.e tablename_id.  Eg. roles_id
3. The length of the fields should be defined in appropriate manner.
4. The filed name should be proper and meaningful.
5. Created and Modified must be at the end of table and should have data type as Datetime.
6. The table name be pural, i.e. should have at the end of the word and must be in small  case letters.
7. Eg:  “users”, “roles” etc
8. If table is having two words then the name should be joined by “_”.
9. Eg.  guest_users, user_details, etc


<h3>Creating Model :</h3>

In cake PHP. Model represents the table. We create model to perform table related activities.
Following are the conventions to be followed while creating any model

1. The name of the model should be in camel case letters starting with capital letter.
2. Model name is table name in singular form .
3. The file name of model should be in camel case letters.
4. The first word of the file name should be model name and the first letter should be capital.
5. The extension of the file is .php.
6. Eg: for table users the model will be
User.php
7. If model name is having two words the file name will be joined two words but the next word should start with capital letter
8. Eg. GuestUser.php , UserDetail.php, etc

<h3>Working with Model :</h3>

As I said earlier, model represents the table and also describe the business logic. Hence it is very important to write clean and meaning full code.
The model class starts with following conventions

1. After starting PHP tags, always write the comments about the file. It must contain the licencing details, Author details, purpose of creation of file and the created date.
2. Include parent class at top i.e
   ``'App::uses('AppModel', 'Model');'``
3. The model class name should be the model name with all above conventions for model name.
4. Model class should extends to the parent class i.e. AppModel
5. Define all the global variables at the beginning of the code.
6. Do all your associations at the beginning. Writing them in between bad practice.
7. Define all your validations for the fields after associations.
8. The object name should be camel case.
9.  No query should be in loop
10.  No query should be written in controller
11.  Utilise same content queries for multiple types.
12.  Keep Proper Relations with associated models
13.  Keep validations for required fields.
14. Eg.
    #app/Model/ModelName.php

    ```Php
    <?php
        App::uses('AppModel', 'Model');
        /**
        * @modal details
        * @author details
        */
        class ModelName extends AppModel {
        //Associations here
        //Validations here
        //Method Comments
            public function objectName ()
            {
                // your logic goes here
            }
        }
    ?>
    ```

<h3>CONTROLLER</h3>
Controller in Cake PHP are responsible for handling processing part of the application. It is a middle layer between modal and view. The controller handles the logic between model and view and post it to view for display. The object we create in it are called as “Actions”.
Following are the conventions to be followed while creating any action

1. Controller name should be meaningful and in camel case format.
2. The controller class should be extended to its parent class, i.e. AppController.
3. The object we create and call in url are call action hence there name should be meaningful.
4. The action name should be meaningful.
5.  Action should not have more than 20 lines of code. If crossing the limit, create one another object and call it. This simplifies the understanding of the code.
6. Action should have less less looping statements and less Nested If
7. It should be written in object oriented manner.
8. If any Action  has multiple thing to be handled, separate them in object.
9. Create Object is such a way that, it should be utilised by any other objects.
10. Avoid repetition of code.
11. All variables  name should be in camel case and initialised at the top.
12. Error and exceptions should have been handled properly.
13. Eg

    #app/Controller/ControllerName.php

    ```Php
    <?php
        App::uses('AppController', 'Controller');
       /**
        * @controller details
        * @author details
        */
        class ControllerNameController extends AppController {

        /*All public variables here*/

        /*Method Comments*/
            public function actionName()
            {
                //Your functionality goes here
            }
        }
    ?>
    ```

<h3>Working with Components</h3>
Components are the common set of code which helps controller to perform certain functionality. The class written in component can be used in any controller. The component can be used in controller by calling it at the top

1. Lets take a look at this.

    #app/Controller/Component/ComponentName.php

    ```Php
    <?php
        /**
         * @Component details
         * @author details
         *
         * */
         class ComponentNameComponent extends Component {

            /*All public variables here*/

            /*Method Comments*/
            public function objectName()
            {
                //Your functionality goes here


            }
        }
    ?>
    ```

In above, we have declared a variable as $component which include th component in that controller. The component written in Component folder in side the controller.Following are the conventions needs to be followed while creating a component.

1. Component name should define it purpose and should be meaningful.
2. The purpose of writing any component should be strong. It should be reusable in other functionality of controller.
3. It should not be controller specific.
4. Component should contain its purpose of creation at the beginning code in comment. With all details of author and file
5. The object name should be meaningful so that any other developer can get it easily.
6. Let take an example of File upload component, how I will write this.

    #app/Controller/Component/FileUpload.php

    ```Php
    <?php
        /**
         * File upload component
         * @purpose : To upload files on server
         * @Author : Name of the coder (www.weboniselab.com)
         * @createdOn : DateOfCreation         *
         * @copyright : Licencing goes here
         *
         * */

        class FileUploadComponent extends Component
        {

            //All public variables here

            //Object comments here

            public function uploadFile(/*All Parameters here in variable*/)
            {

                // File upload logic goes here

                 return /*upload status*/
            }

        }
    ?>
    ```

In above, we have created a file upload component which uploads the file on server in specific folder.Now, how we are going to use it in controller where I want upload a file. Lets take an another example.Suppose, I want to upload an image of user. So I will do my functionality in "UsersController.php"

1. Lets take a look.

    #app/Controller/Users.php

    ```Php
    <?php

        App::uses('AppController', 'Controller');

       /**
        * @name : UsersController
        * @author: Name of coder
        * @CreatedON : DateOfCreation
        * @purpose : To do all user related functionality
        *
        * */

        class ControllerNameController extends AppController {

            //to include component create public variable as $component which should be written as it is.
            public $component = array('FileUpload');

            /*In specific action I want to upload a file, say it signUp*/

            public function sign_up(){

                //With all logic goes here, I will call the component

                $isUploaded = $this->FileUpload->uploadFile(/*all file parameters here*/);

                /*then next logic according to the upload status goes here*/
            }
        }
    ?>
    ```

By above example, we can see that how we have called a component in controller and used it.

<h3>VIEW</h3>

View is the representation part of application. It is an UI. What ever the logic and functionality we have done, need to be represented in proper format and structure. The view is responsible for representing things i.e. UI.
In CakePHP, view come after controller and model. When a data is processed in controller, it  passes that data to view and view represents it.  Following are the conventions to be followed while working with view.
We store view related files in ``.ctp`` format.

1. Try to create light html pages.
2. Do use nested loops in view.
3. Use CakePHP helper for html.
4. For Common set of html which can be used in other pages also, shoud be converted to element.
5. Create Helpers to get common functionality done
6. No queries in View
7. No Controller Logic in view
8. No javascript in script tag should be written in Js file properly
9. Validation should be handled separately
10. No in line CSS in file. Create developer CSS to handle external changes.
11. The layout should be made in proper way and header, footer should be manged there itself.
11. Eg


    #app/View/Layout/default.ctp

    ```Php
    <?php
        /**
         *
         * PHP 5
         *
         * CakePHP(tm) : Rapid Development Framework (http://cakephp.org)
         * Copyright 2005-2012, Cake Software Foundation, Inc. (http://cakefoundation.org)
         *
         * Licensed under The MIT License
         * Redistributions of files must retain the above copyright notice.
         *
         * @copyright     Copyright 2005-2012, Cake Software Foundation, Inc. (http://cakefoundation.org)
         * @link          http://cakephp.org CakePHP(tm) Project
         * @package       Cake.View.Layouts
         * @since         CakePHP(tm) v 0.10.0.1076
         * @license       MIT License (http://www.opensource.org/licenses/mit-license.php)
         */

        $cakeDescription = __d('cake_dev', 'CakePHP: the rapid development php framework');
        ?>
        <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
        <html xmlns="http://www.w3.org/1999/xhtml">
        <head>
            <?php echo $this->Html->charset(); ?>
            <title>
                <?php echo $cakeDescription ?>:
                <?php echo $title_for_layout; ?>
            </title>
            <?php
                echo $this->Html->meta('icon');

                echo $this->Html->css('cake.generic');

                echo $this->fetch('meta');
                //All css files here
                $this->Html->css(array(/*all css file in array without extension*/));
                 echo $this->fetch('css');

                //All Js libraries here
                $this->Html->script(array(/*all JS file in array without extension*/));
                echo $this->fetch('script');?>
        </head>
        <body>
            <div id="container">
               <!-- Header -->
                <div id="header">
                    <h1><?php echo $this->Html->link($cakeDescription, 'http://cakephp.org'); ?></h1>
                </div>
                <div id="content">
                    <!--All flash messages will go here-->
                    <?php echo $this->Session->flash(); ?>
                    <!--All the contents of the view other than header and footer will come here-->
                    <?php echo $this->fetch('content'); ?>
                </div>
                <!-- Footer-->
                <div id="footer">
                    <?php echo $this->Html->link(
                            $this->Html->image('cake.power.gif', array('alt' => $cakeDescription, 'border' => '0')),
                            'http://www.cakephp.org/',
                            array('target' => '_blank', 'escape' => false)
                        );
                    ?>
                </div>
            </div>
            <!-- This displays all the sql queries here. Can be disabled by making Debug mode '0' in app/Config/core.php-->
            <?php echo $this->element('sql_dump'); ?>
        </body>
        </html>

    ?>
    ```

<h3>Working with Helpers</h3>

Helper are the common set of functionality, which can be used in any view. Likewise component in controller,  hepler  works in view. The helper are storred in ``app/View/Helper/HelperName.php``.
Following are the conventions to be followed while writing any helper.

1. Helper should not be view dependent. It should have common purpose of creation.
2. Helper should have meaningful name.
3. The Helper name should be in camel case letters starting first letter in capital.
4. The helper class should be extended to parent class i.e. ``AppHelper``
5. The comment should be given to the helper class.
6. Eg

    #app/View/Helper/HelperName.php

    ```Php
    <?php
        /**
         * Application level View Helper
         *
         * This file is helper for all the views.
         *
         *
         * PHP 5
         *
         * CakePHP(tm) : Rapid Development Framework (http://cakephp.org)
         * Copyright 2005-2012, Cake Software Foundation, Inc. (http://cakefoundation.org)
         *
         * Licensed under The MIT License
         * Redistributions of files must retain the above copyright notice.
         *
         * @copyright     Copyright 2005-2012, Cake Software Foundation, Inc. (http://cakefoundation.org)
         * @link          http://cakephp.org CakePHP(tm) Project
         * @package       app.View.Helper
         * @since         CakePHP(tm) v 0.2.9
         * @license       MIT License (http://www.opensource.org/licenses/mit-license.php)
         * */

            App::uses('AppHelper', 'Helper');

        /**
         * Common purpose helper
         *
         * Add your application-wide methods in the class below, your helpers
         * will inherit them.
         *
         * @package       app.View.Helper
         */

         class AppHelper extends Helper {

            // Logic goes here

         }

    ?>
    ```

