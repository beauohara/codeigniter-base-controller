codeigniter-base-controller
===========================

Introduction
------------

This is an extended Controller class to use in CodeIgniter applications that provides some clever model loading, view loading and layout support. It uses a Rails-like convention system to automatically load the view based on the controller name and the current method, and uses a custom layout system. 

Usage
-----

Drag the MY\_Controller.php file into your _application/libraries_ folder. CodeIgniter will load and initialise this class automatically for you. Then all you have to do is make sure all your controllers extend from MY_Controller and all the functionality will be baked into your controllers automatically!

View Loading
------------

Depending on the controller and action running, this class will try to guess the location of the view and load it for you. To pass data through to the view you simply set the _$this->data_ array in a similar fashion to normal and it will be passed through to the view. For example, if we were in the _Games_ controller and the _index()_ action, the class would try to load the _application/views/games/index.php_ view.

If you need to customise this view loading convention in any way, you can by setting the _$this->view_ instance variable anywhere in your controller. Set this to any view and that view will be loaded, or set it to FALSE to not load a view at all. It's very flexible this way.

Layout Loading
--------------

This class will also try to load your view into a layout. By default, it will first look for a layout file (located in your _application/views/layouts_ folder) with the same name as the current controller. If it can't find that it will then look for _application/views/layouts/application.php_ - a global, application level layout file. For example, if you had an _Admin_ controller it will first look for _application/views/layouts/admin.php_ and then if that doesn't exist, it will try to load _application/views/layouts/application.php_ layout instead.

You can also override this functionality by setting the _$this->layout_ instance variable. Set it to a string to load that layout, or FALSE to load no layout. This will take precedence over the conventional loading strategy.

Model Loading
-------------

Set the _$this->models_ instance variable in your controller to be an array of all the models you want to load and this class will loop through that array, loading each one sequentially. It looks for the model with a filename of _$model\_name\_model.php_ and the class name of _$model\_name\_model_, but will load the model into the CI super object under _$model\_name_. For instance, if my _$this->models_ array had a _'game'_ model, it would look for the file and class _Game\_model_ but will load it to _$this->game_.

You can customise the suffix or prefix of the model name by setting the $this->model\_string variable. Use the % symbol, which will be replaced with the model you want to load.

Custom 404 Messages
-------------------

If you try to call a method that doesn't exist, the class will first look for a \_404 method in your controller. This method will be passed the method that you're trying to call. Otherwise, it will display a default CodeIgniter 404 message.

Version History
---------------

* 1.2.0 A bugfix, support for custom model names and custom 404 messages.
* 1.1.1 $this->data is now passed to layout, after the view is rendered
* 1.1.0 Partial support, asides and an improvement to documentation
* 1.0.5 Added support for multiple view rendering.
* 1.0.2 A few bugfixes
* 1.0.0 First release of library and basic functionality, with basic readme 