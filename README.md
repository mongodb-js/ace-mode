# mongodb-ace-mode [![][npm_img]][npm_url]

MongoDB ACE mode

## Installation

```
npm install --save mongodb-ace-mode
```


## Discovery
https://codepen.io/imlucas/pen/eXJOrm

<style>
/**
 * Parens
 * {}[]()
 */
.ace-mongodb .ace_paren {
  font-weight: normal;
  color: blue;
}

/**
 * Quotes around a "field name"
 * "$trends.icecream_cpi"
 */
.ace_string.ace_quasi{
    color: magenta !important;
}

/**
 * Field names
 * _id, average_cpi, etc.
 */
.ace_identifier {
  color: green;
}

/**
 * Aggregation Operators
 * $avg $min $max
 */
.ace-mongodb .ace_support.ace_function {
  color: orange;
}

/**
 * BOILERPLATE BELOW
 */
.ace-mongodb .ace_gutter {
background: #f5f6f7;
color: #999999;
}
.ace-mongodb  {
  border: 1px solid #eee;
  padding: 10px;
  //background: #f5f6f7;
  color: #000;
  font-family: Monaco;
  
}
.ace-mongodb .ace_keyword {
color: #999999;
font-weight: normal;
}
.ace-mongodb .ace_gutter-cell {
padding-left: 5px;
padding-right: 10px;
}
.ace-mongodb .ace_string {
color: #5b81a9;
}
.ace-mongodb .ace_boolean {
color: #5b81a9;
font-weight: normal;
}
.ace-mongodb .ace_constant.ace_numeric {
color: #5b81a9;
}
.ace-mongodb .ace_string.ace_regexp {
color: #5b81a9;
}
.ace-mongodb .ace_variable.ace_class {
color: teal;
}
.ace-mongodb .ace_constant.ace_buildin {
color: #0086B3;
}

/*
.ace-mongodb .ace_support.ace_function {
  color: #0086B3;
}
*/
.ace-mongodb .ace_comment {
color: #998;
font-style: italic;
}
.ace-mongodb .ace_variable.ace_language  {
color: #0086B3;
}

</style>
<div class="ace-mongodb">
  <div class="ace_layer ace_text-layer" style="padding: 0px 4px;">
    <div class="ace_line" style="height:15px">
      <span class="ace_paren ace_lparen">{</span>
    </div>
    <div class="ace_line" style="height:15px">&nbsp;&nbsp;<span class="ace_identifier">_id</span><span class="ace_punctuation ace_operator">:</span><span class="ace_constant ace_numeric"> 0</span><span class="ace_punctuation ace_operator">,</span></div>
    <div class="ace_line" style="height:15px">&nbsp;&nbsp;<span class="ace_identifier">average_cpi</span><span class="ace_punctuation ace_operator">:</span> <span class="ace_paren ace_lparen">{</span><span class="ace_support ace_function">$avg</span><span class="ace_punctuation ace_operator">:</span><span class="ace_string ace_quasi ace_start">"</span><span class="ace_variable ace_language">$trends.icecream_cpi</span><span class="ace_string ace_quasi ace_end">"</span><span class="ace_paren ace_rparen">}</span><span class="ace_punctuation ace_operator">,</span></div>
    <div class="ace_line" style="height:15px">&nbsp;&nbsp;<span class="ace_identifier">max_cpi</span><span class="ace_punctuation ace_operator">:</span><span class="ace_paren ace_lparen">{</span><span class="ace_support ace_function">$max</span><span class="ace_punctuation ace_operator">:</span><span class="ace_string ace_quasi ace_start">"</span><span class="ace_variable ace_language">$trends.icecream_cpi</span><span class="ace_string ace_quasi ace_end">"</span><span class="ace_paren ace_rparen">}</span><span class="ace_punctuation ace_operator">,</span>
      </div>
    <div class="ace_line" style="height:15px">
      &nbsp;&nbsp;<span class="ace_identifier">min_cpi</span><span class="ace_punctuation ace_operator">:</span><span class="ace_paren ace_lparen">{</span><span class="ace_support ace_function">$min</span><span class="ace_punctuation ace_operator">:</span><span class="ace_string ace_quasi ace_start">"</span><span class="ace_variable ace_language">$trends.icecream_cpi</span><span class="ace_string ace_quasi ace_end">"</span><span class="ace_paren ace_rparen">}</span><span class="ace_punctuation ace_operator">,</span></div>
    <div class="ace_line" style="height:15px">
      &nbsp;&nbsp;<span class="ace_identifier">cpi_deviation</span><span class="ace_punctuation ace_operator">:</span><span class="ace_paren ace_lparen">{</span><span class="ace_support ace_function">$stdDevPop</span><span class="ace_punctuation ace_operator">:</span><span class="ace_string ace_quasi ace_start">"</span><span class="ace_variable ace_language">$trends.icecream_cpi</span><span class="ace_string ace_quasi ace_end">"</span><span class="ace_paren ace_rparen">}</span></div>
    <div class="ace_line" style="height:15px"><span class="ace_paren ace_rparen">}</span>
    </div>
  </div>
</div>









<br />


### Notes

- https://github.com/ajaxorg/ace/blob/master/lib/ace/theme/monokai.css
- https://ace.c9.io/build/kitchen-sink.html
- https://github.com/ajaxorg/ace/wiki/Creating-or-Extending-an-Edit-Mode

### Basic 

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
