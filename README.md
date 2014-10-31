
CakePHP 3.0 plugin to update e.g. `created_by` and `modified_by` fields.

## Installation

Add the following lines to your application's `composer.json`:

```
    "require": {
        "hmic/cakephp-blame": "dev-master"
    }
```

followed by the command:

`composer update`

Or run the following command directly without changing your `composer.json`:

`composer require hmic/cakephp-blame:dev-master`

OR:
Create a `plugins/Blame` dir under your app's dir and checkout this repo
and make sure `['autoload' => true]` is set when loading the plugin like shown below.

## Usage

In your app's `config/bootstrap.php` add: `Plugin::load('Blame', ['autoload' => true])`;

## Configuration

Add the following line to your AppController:

```
    use \Blame\Controller\BlameTrait;
```

Attach the behavior in the models you want with:

```
    public function initialize(array $config) {
        $this->addBehavior('Blame.Blame');
    }
```

## Routing

This is work in progress, but you can have routing working, for use with baked views,
(works only for the default configuration for now) by adding this to your app's
`config/routes.php` directly defore the `$routes->fallbacks();` and commenting that out,
like this:

```
 	$routes->connect('/:controller', ['action' => 'index'], ['routeClass' => 'Blame.BlameRoute']);
 	$routes->connect('/:controller/:action/*', [], ['routeClass' => 'Blame.BlameRoute']);
//	$routes->fallbacks();
```

## Bake
If you want to bake your stuff you need to bake the model first, then add the behavior as shown
above and afterwards bake the controller and views. It will take care of the associations
automatically. For the routing of the baked views to work for the assocations too, see above.
