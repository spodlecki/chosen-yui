# chosen-yui

When using [Chosen JS](http://harvesthq.github.io/chosen/), make sure to grab the native js files, [abstract-chosen](https://github.com/harvesthq/chosen/blob/master/coffee/lib/abstract-chosen.coffee) and [select-parser](https://github.com/harvesthq/chosen/blob/master/coffee/lib/select-parser.coffee).

Then you're all set. Use the chosen.yui.js instead of the chosen.prototype or chosen.jquery

They (HarvestHQ) is preparing to release a fully native version of ChosenJS so I don't plan on continuing development on this.

```javascript
YUI().use('node','yui-chosen', function(Y) {
  Y.all('.yui-chosen').each(function(ele) {
    ele.plug(Y.Chosen, {
      no_results_text: "Nothing found dummy.",
      disable_search_threshold: 4,
      max_selected_options: 2,
      allow_single_deselect: true,
      width: "500px"
    });
    ele.on('change', function(e) {
      var value = null;
      if (e.currentTarget.getDOMNode().type == 'select-multiple') {
        var value = [];
        e.currentTarget.all('option').each(function(opt) {
          if (opt.get('selected')) {
            value.push(opt.get('value'));
          }
        });
      } else {
        value = e.currentTarget.get('value');
      }
    });
  });
});
```