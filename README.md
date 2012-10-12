yii-remember-filters-gridview
=============================

The ERememberFiltersBehavior Yii extension adds up some functionality to the default possibilites of CActiveRecord/Model implementation.

It will detect the **search** scenario and it will save the filters from the GridView. This comes handy when you need to **remember them between navigation** during page changes. For lot of navigation and heavy filtering, this functionality can be activated by just a couple of lines.

It supports **default filter values** and **remember scenarios** also. For example if you want to show only eg: Active Products, you can setup the default filter using this extension. Or if you have the same modal on different views, you can set different scenarios to remember state separated from each other. See the optional params under Advanced Functionalities and Scenarios section. 

![Please login to see the Demo image!](https://raw.github.com/pentium10/yii-remember-filters-gridview/master/res/remember_filters_10.png "Demo")

Requirements
--------------------

- Yii 1.1

Donate
----------

[Click here to donate](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=K9TM6HR8JQ4Z8 "Donate")

Resources
---------------

- **[Extension page](http://www.yiiframework.com/extension/remember-filters-gridview/) (don't forget to cast your support vote)**
- [Report a bug](http://github.com/pentium10/yii-remember-filters-gridview/issues "Report a bug")
- [Forum](http://www.yiiframework.com/forum/index.php?/topic/15847-extension-remember-filters-gridview/ "Forum")
- [Clear Filters Gridview extension](http://www.yiiframework.com/extension/clear-filters-gridview "http://www.yiiframework.com/extension/clear-filters-gridview")

Usage
---------

Step 1
--------

To use this extension, just copy this file to your components/ directory, add 'import' => 'application.components.ERememberFiltersBehavior', [...] to your config/main.php and paste the following code to your behaviors() method of your model

```php
public function behaviors() {
       return array(
           'ERememberFiltersBehavior' => array(
               'class' => 'application.components.ERememberFiltersBehavior',
			   'defaults'=>array(),           /* optional line */
			   'defaultStickOnClear'=>false   /* optional line */
           ),
       );
}
```

Step 2
---------

**Your actionAdmin() must not use unsetAttributes() as this was moved to the extension.**

With this extension the actionAdmin instead of the classic
```php
        public function actionAdmin()
        {
                $model=new Company('search');
                $model->unsetAttributes();  // clear any default values
                if(isset($_GET['Company']))
                        $model->attributes=$_GET['Company'];
                $this->render('admin',array(
                        'model'=>$model,
                ));
        }
```

can be as simple as:
```php
        public function actionAdmin()
        {
                $model=new Company('search');
                $this->render('admin',array(
                        'model'=>$model,
                ));
        }
```

Advanced Functionalities
----------------------------------

_(if you use these functionalities please Donate)_

- **'defaults'** is a key value pair array, that will hold the defaults for your filters. 
For example when you initially want to display `active products`, you set to `array('status'=>'1')`. 
You can of course put multiple default values in the array.

- **'defaultStickOnClear'=>true** can be used, if you want the default values to be put back when the user clears the filters
The default set is `false` so if the user clears the filters, also the defaults are cleared out, the user will get an absolutely clean filter form. When `true`, if the form is cleared, he will get a form with defaults values.


Scenarios
--------------

_(if you use these functionalities please Donate)_

You can use `scenarios` to remember the filters on multiple states of the same model. This is helpful when you use the same model on different views and you want to remember the state separated from each other.  
Known limitations: the views must be in different actions (not on the same view)  

To set a scenario add the setRememberScenario call after the instantiation  
Sample code:  
```php
        public function actionAdmin()
        {
                $model=new Company('search');
				$model->setRememberScenario('scene1');
                $this->render('admin',array(
                        'model'=>$model,
                ));
        }
````


This extension has also a pair [Clear Filters Gridview](http://www.yiiframework.com/extension/clear-filters-gridview "http://www.yiiframework.com/extension/clear-filters-gridview")

remember, filters, cgridview, gridview, store, reload, controller, model, behavior, interface, widget, stick, scenario

Change Log 
-----------------

[CHANGELOG.md](http://github.com/pentium10/yii-remember-filters-gridview/blob/master/CHANGELOG.md)

Contributing
------------

1. Fork it.
2. Create a branch (`git checkout -b my_enhancement_name`)
3. Commit your changes (`git commit -am "Added Sorting"`)
4. Push to the branch (`git push origin my_enhancement_name`)
5. Open a [Pull Request][1]
6. Enjoy a refreshing Diet Coke and wait

[1]: http://github.com/pentium10/yii-remember-filters-gridview/pulls