SpreePlugins
============

This Spree extension enables Spree storefront owners to add custom scripts and features as plugins to products.
Currently it allows owners to easily insert code into every customer facing product page.

Installation
------------

Add spree_plugins to your Gemfile:

```ruby
gem 'spree_plugins'
```

Bundle your dependencies and run the installation generator:

```shell
bundle
bundle exec rails g spree_plugins:install
```

Creating a Plugin
--------
After installing this gem navigate to Configurations then choose the final option on the right sidebar, Add Plugins, then click Add One. Alternatively navigate to /admin/plugins/new.
Fields

  1. Name - Renders as the id on the div surrounding your plugin.  Id is rendered as name + _plugin
  2. CSS Class - renders directly as the class on the div surrounding your plugin
  3. Active - Whether or not to activate this on the storefront.
  4. Code - actual code rendered directly in the div

See example below.

Examples
--------
[**disqus**](https://www.disqus.com/)
  1. Activate plugin with the code below and name disqus.
```
<div id="disqus_thread"></div>
<script type="text/javascript">
    /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
    var disqus_shortname = 'spreeplugin'; // required: replace example with your forum shortname

    /* * * DON'T EDIT BELOW THIS LINE * * */
    (function() {
        var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
        dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
        (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
    })();
</script>
<noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
<a href="http://disqus.com" class="dsq-brlink">comments powered by <span class="logo-disqus">Disqus</span></a>
```

This code is linked to an existing account. To have all the features of add this, visit their [website](https://www.disqus.com/).

[**add this**](https://www.addthis.com/)
  1. Activate plugin with the code below and name as add_this.
```
<div class="addthis_native_toolbox"></div>
<script type="text/javascript" src="//s7.addthis.com/js/300/addthis_widget.js#pubid=ra-53d015385403dfff"></script>
```

This code is linked to an existing account. To have all the features of add this, visit their [website](https://www.addthis.com).

[**share-button**](https://github.com/carrot/share-button)

  1. Make a new plugin in the Configurations menu of admin
  2. Download and copy the script from the [Github page](https://github.com/carrot/share-button) as code for this new plugin.
  3. Activate then save the plugin.
  4. (Optional:) include a custom css class to position the plugin to your liking on the product page.

Customize
----------
To customize your css class, follow the instructions [here](http://guides.spreecommerce.com/developer/asset.html) to add a custom css class.  These guides suggest you put your stylesheets in vender/assets/stylesheets/spree/frontend however if you'd like your stylesheets in app/assets/stylesheets you can run
```shell
cp -r vendor/assets/ app/assets/
```
and proceed to make edits in app/assets/stylesheets/spree/frontend.
Note: everything is in frontend b/c our scripts render on the customer product page.

To customize where in the DOM you'd like the div and script tag to be inserted, you can add this jQuery script to the plugin's code to specify a DOM element to add the plugin scripts to:
```javascript
$(function() {
  $($('#[plugin_name]_plugin').detach()).appendTo([SELECTOR_FOR_YOUR_DOM_ELEMENT]);
});
```

For example, the code to put the disqus plugin into the footer, would be:
```javascript
$(function() {
  $($('#disqus_plugin').detach()).appendTo($('#footer'));
});
```

Note: The id for your plugin's div is defaulted to `[plugin_name]_plugin`

Testing
-------

First bundle your dependencies, then run `rake`. `rake` will default to building the dummy app if it does not exist, then it will run specs. The dummy app can be regenerated by using `rake test_app`.

```shell
bundle
bundle exec rake
```

When testing your applications integration with this extension you may use it's factories.
Simply add this require statement to your spec_helper:

```ruby
require 'spree_plugins/factories'
```

Copyright (c) 2014 GoDaddy, released under the New BSD License
