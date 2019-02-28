# mongodb-ace-mode [![][npm_img]][npm_url]

MongoDB ACE mode

## Installation

```
npm install --save mongodb-ace-mode
```

## Notes

https://github.com/ajaxorg/ace/blob/master/lib/ace/theme/monokai.css
https://ace.c9.io/build/kitchen-sink.html
https://github.com/ajaxorg/ace/wiki/Creating-or-Extending-an-Edit-Mode

### Basic Exploration

Given:

```js
average_cpi: {$avg: "$trends.icecream_cpi" }
```

Want to highlight:

- `$trends.icecream_cpi`
- `$avg`
- `"` around `$trends.icecream_cpi` separated

See 

HTML we want looks something like:

```html
<div class="ace_line" style="height: 16px; top: 32px;">  
  <span class="ace_identifier">average_cpi</span>
  <span class="ace_punctuation ace_operator">:</span> 
  <span class="ace_paren ace_lparen">{</span>
  <span class="ace_identifier ace_support ace_function">$avg</span>
  <span class="ace_punctuation ace_operator">:</span>
  <span class="ace_string ace_quasi ace_start">"</span>
  <span class="ace_variable">$trends.icecream_cpi</span>
  <span class="ace_string ace_quasi ace_end">"</span>
  <span class="ace_paren ace_rparen">}</span>
</div>
```

`$avg` Agg Operator:
- ace_support.ace_function
- ace_keyword.ace_operator 
- ace_function

$trends.icecream_cpi Field:
- ace_variable
- ace_identifier -> nice as it links back to semantics of `average_cpi`

Base on interpolated strings. JSX mode kind of implements this:

https://github.com/ajaxorg/ace/blob/master/lib/ace/mode/javascript_highlight_rules.js#L375-L391
```js
{
  token : "string.quasi.start",
  regex : /`/,
  push  : [{
      token : "constant.language.escape",
      regex : escapedRe
  }, {
      token : "paren.quasi.start",
      regex : /\${/,
      push  : "start"
  }, {
      token : "string.quasi.end",
      regex : /`/,
      next  : "pop"
  }, {
      defaultToken: "string.quasi"
  }]
}
```

average_cpi
- ace_identifier
- ace_variable.ace_parameter?

### Advanced

$lookup:
- special props at top level: `from`, `let`, `pipeline`

```
...
stageOperator: '$lookup',
stage: `{
  from: "air_airlines",
  let: { maybe_name: "$airlines" },
  pipeline: [
    {
      $match: {
...
```

$and $or conditionals:
- ace_keyword.ace_operator
- ace_keyword.ace_control -> flow control keywords


## License

Apache 2.0

[npm_img]: https://img.shields.io/npm/v/mongodb-ace-mode.svg?style=flat-square
[npm_url]: https://www.npmjs.org/package/mongodb-ace-mode
