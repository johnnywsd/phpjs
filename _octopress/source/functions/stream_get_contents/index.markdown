---
layout: page
title: "JavaScript stream_get_contents function"
comments: true
sharing: true
footer: true
alias:
- /functions/view/stream_get_contents:856
- /functions/view/stream_get_contents
- /functions/view/856
- /functions/stream_get_contents:856
- /functions/856
---
<!-- Generated by Rakefile:build -->
A JavaScript equivalent of PHP's stream_get_contents

{% codeblock stream/stream_get_contents.js lang:js https://raw.github.com/kvz/phpjs/master/functions/stream/stream_get_contents.js raw on github %}
function stream_get_contents (handle, maxLength, offset) {
  // http://kevin.vanzonneveld.net
  // +   original by: Brett Zamir (http://brett-zamir.me)
  // *     example 1: var stream = fopen('http://kevin.vanzonneveld.net/pj_test_supportfile_1.htm', 'r');
  // *     example 1: stream_get_contents(stream, 7, 2);
  // *     returns 1: 'DOCTYPE'
  if (!this.php_js || !this.php_js.resourceData || !this.php_js.resourceDataPointer || !handle || !handle.id) {
    return false;
  }
  offset = offset || 0;
  this.php_js.resourceDataPointer[handle.id] += offset;

  var chrs = this.php_js.resourceData[handle.id].slice(this.php_js.resourceDataPointer[handle.id]);
  chrs = maxLength >= 0 ? chrs.substr(0, maxLength) : chrs;

  this.echo(chrs);
  this.php_js.resourceDataPointer[handle.id] += chrs.length;

  return chrs;
}
{% endcodeblock %}

 - [view on github](https://github.com/kvz/phpjs/blob/master/functions/stream/stream_get_contents.js)
 - [edit on github](https://github.com/kvz/phpjs/edit/master/functions/stream/stream_get_contents.js)

### Example 1
This code
{% codeblock lang:js example %}
var stream = fopen('http://kevin.vanzonneveld.net/pj_test_supportfile_1.htm', 'r');
stream_get_contents(stream, 7, 2);
{% endcodeblock %}

Should return
{% codeblock lang:js returns %}
'DOCTYPE'
{% endcodeblock %}


### Other PHP functions in the stream extension
{% render_partial _includes/custom/stream.html %}
