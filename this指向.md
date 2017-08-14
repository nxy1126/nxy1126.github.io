##  JS中this的指向  
###  事件中的this:  
######  示例  
	<script>
		box.onclick = function(){
			this.style.background = "red";
			console.log(this);                 
		}
	</script>
`这个示例中的this在onclick事件中,所有的事件中的this始终指向这个事件的拥有者,所以这个示例中的this是指向box的;`  
###  函数中的this:
######  示例
	<script>
		function fn1(){
			console.log(this);
		}
	</script>
	fn1();
`函数中的this默认指向window;在函数拥有所有者时,this会指向这个函数的所有者;在这个示例中,函数没有所有者,所以"console.log(this)"结果是window;`  
###  对象中的this:  
######  示例  
	<script>
		var obj = {
			name:"张三",
			fn:function(){
				console.log(this.name);
			}
		}
		obj.fn();
	</script>
`在对象中使用的this指的就是这个对象,在这个对象中的"name"属性的值是张三,所以打印出来的就是张三;`    
###  定时器中的this:
######  实例
	<script>
		setInterval(function(){
			console.log(this);
		},1000)
	</script>
`可以打印一下试试,JS中定时器里的this始终指向window,就是放在函数中或者事件里,也始终是指向window;`  

###  this在构造函数中指的是实例化出来对象
######  示例
	function Fn1 () {
		this.name = "张三"
		console.log(this);
	}
	Fn1();
	var go = new Fn1();
`在这个示例中,Fn1()就相当于普通的函数,函数中的this默认指向window,所以Fn1()自己执行的结果是window;而构造函数在通过new实例化出来对象时,this的指向就会变为这个实例化出来的对象,this就会返回这个构造函数;`
###  通过call和apply来改变this指向:
######  call方法:
	function fn(){
		console.log(this);
	}
	fn();
	fn.call(document);
`在这个例子中函数fn中的this原本应该是指向window的,所以fn在自执行的时候打印的是"window";但是在函数调用时使用了call方法,表示吧这个函数的this指向改变为document,所以在"fn.call(document)"结果是"document";`  
######  apply方法:
	function fn(){
		console.log(this);
	}
	fn();
	fn.apply(document);
`和call方法一样,都是用来改变this指向,把默认指向window的this指向改变为"document";`
######  区别:
1.  call方法第一个参数之后的参数不限制类型和个数
2.  apply方法接受的第二个参数只能是数组