参考文档:

http://segmentfault.com/a/1190000000342636?from=androidqq

javascript:


### html:
``` bash
var template = require('./wrapview/wrapTpl.html');
var data = {
	say_hello: "it is handlebars",
	auther: {
		name: "meiminjun",
		age: "29",
		sex: "man"
	},
	list: [{
		name: 11
	}, {
		name: 222
	}, {
		name: 3333
	}],
		response:''
	};
    var result = template(data);

wrapTpl.html
<div>
	<h1>测试</h1>
	<h1>{{say_hello}}</h1>
	{{#with auther}}
		<h2>{{name}}</h2>
		<h2>{{age}}</h2>
		<h2>{{sex}}</h2>
	{{/with}}
	{{#each list}}
		{{name}}
	{{else}}
		<p>No content</p>
	{{/each}}
	{{#if response}}
		<p>有内容</p>
	{{else}}
		<p>没有内容</p>
	{{/if}}
</div>

```