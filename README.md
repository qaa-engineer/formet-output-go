# Форматированный вывод в Go

<article id="ember2996" class="step-show ember-view"><div class="step-dynamic-container">
<!---->
      <div id="ember2997" class="step-view step-view_material ember-view"><!----><div class="step-wrapper">
  <div class="step-inner page-fragment">
      <div id="ember2998" class="html-content rich-text-viewer ember-view" data-processed=""><!----><span>

<p><br>
Ряд возможностей для вывода&nbsp;и не только предоставляет пакет&nbsp;<a href="https://golang.org/pkg/fmt" rel="nofollow noopener noreferrer" target="_blank">fmt</a>. До этого&nbsp;мы использовали только <code>Print</code> и <code>Println</code>, а что если нам понадобится вывести, допустим у числа <strong>float64</strong> только 2&nbsp;знака&nbsp;после запятой. Подобные&nbsp;операции удобно делать через функцию <code>Printf</code>. Давайте рассмотрим&nbsp;основные возможности.</p>

<p><code>fmt.Printf()</code> на вход принимает сначала строку форматирования, а только потом&nbsp;переменные&nbsp;для вывода.&nbsp;Строка форматирования представляет набор спецификаторов. Каждый спецификатор представляет набор символов, которые интерпретируются определенным образом и предваряются знаком процента %.&nbsp;&nbsp;В&nbsp;качестве примера возьмем глагол&nbsp;-&nbsp;спецификатор&nbsp;<code>%q</code>&nbsp;, с помощью него можно вывести символ в кавычках:</p>

<pre><code class="language-go hljs"><span class="hljs-keyword">var</span> a <span class="hljs-keyword">rune</span> = <span class="hljs-string">'Ы'</span>
fmt.Printf(<span class="hljs-string">"%q"</span>, a)
<span class="hljs-comment">// вывод: 'Ы'</span>

</code></pre>

<p>Каждый спецификатор представляет определенный тип данных:</p>

<ul>
	<li>
	<p><code>%t</code>: для вывода значений типа boolean (true или false)</p>
	</li>
	<li>
	<p><code>%b</code>: для вывода целых чисел в двоичной системе</p>
	</li>
	<li>
	<p><code>%c</code>: для вывода символов, представленных числовым кодом</p>
	</li>
	<li>
	<p><code>%d</code>: для вывода целых чисел в десятичной системе</p>
	</li>
	<li>
	<p><code>%o</code>: для вывода целых чисел в восьмеричной системе</p>
	</li>
	<li>
	<p><code>%q</code>: для вывода символов в одинарных кавычках</p>
	</li>
	<li>
	<p><code>%x</code>: для вывода целых чисел в шестнадцатеричной системе, буквенные символы числа имеют нижний регистр a-f</p>
	</li>
	<li>
	<p><code>%X</code>: для вывода целых чисел в шестнадцатеричной&nbsp;системе, буквенные символы числа имеют верхний регистр A-F</p>
	</li>
	<li>
	<p><code>%U</code>: для вывода символов в формате кодов Unicode, например, U+1234</p>
	</li>
	<li>
	<p><code>%e</code>: для вывода чисел с плавающей точкой в экспоненциальном представлении, например, -1.234456e+78</p>
	</li>
	<li>
	<p><code>%E</code>: тоже самое что <code>%e</code> но в верхнем регистре, например, -1.234456E+78</p>
	</li>
	<li>
	<p><code>%f</code>: для вывода чисел с плавающей точкой, например, 123.456</p>
	</li>
	<li>
	<p><code>%F</code>: то же самое, что и %f</p>
	</li>
	<li>
	<p><code>%g&nbsp;</code>&nbsp; %e для огромных экспонент, %f в противном случае</p>
	</li>
	<li>
	<p><code>%G</code>&nbsp; &nbsp; %E для огромных экспонент, %F&nbsp;в противном случае</p>
	</li>
	<li>
	<p><code>%s</code>: для вывода строки</p>
	</li>
	<li>
	<p><code>%p</code>: для вывода значения указателя - адреса в шестнадцатеричном представлении (указатели мы пройдем на следующих уроках)</p>
	</li>
	<li>
	<p><code>%T</code> для вывода типа переменной</p>
	</li>
</ul>

<p>Также можно применять универсальный спецификатор&nbsp;<code>%v</code>, который для типа boolean аналогичен&nbsp;<code>%t</code>, для целочисленных типов -&nbsp;<code>%d</code>, для чисел с плавающей точкой -&nbsp;<code>%g</code>, для строк -&nbsp;<code>%s</code>.</p>

<p>К спецификаторам можно добавлять различные флаги, которые влияют на форматирование значений. Например, число перед спецификатором указывает, какую минимальную длину в символах будет занимать выводимое значение. Например,&nbsp;<code>%9f</code>&nbsp;- число с плавающей точкой будет занимать как минимум 9 позиций. Если ширина больше, чем требуется значению, то заполняется пробелами.</p>

<p>Для чисел с плавающей точкой можно указать точность или количество символов в дробной части. Для этого количество символов указывается после точки:&nbsp;<code>%.2f</code>&nbsp;- две цифры в дробной части после точки. Например, варианты форматирования чисел с плавающей точкой:</p>

<ul>
	<li>
	<p><code>%f</code>: точность и ширина значения по умолчанию</p>
	</li>
	<li>
	<p><code>%9f</code>: ширина - 9 символов и точность по умолчанию<br>
	(число с плавающей точкой будет занимать как минимум 9 позиций. Если ширина больше, чем требуется значению, то заполняется пробелами.)</p>
	</li>
	<li>
	<p><code>%.2f</code>: ширина по умолчанию и точность - 2 символа</p>
	</li>
	<li>
	<p><code>%9.2f</code>: ширина - 9 и точность - 2</p>
	</li>
	<li>
	<p><code>%9.f</code>: ширина - 9 и точность - 0</p>
	</li>
</ul>

<p>Также из флагов следует отметить дефис -, который дополняет значение пробелами не слева, как по умолчанию, а справа.</p>

<p>Примеры:</p>

<pre><code class="language-go hljs"><span class="hljs-keyword">var</span> a <span class="hljs-keyword">float64</span> = <span class="hljs-number">100.123456</span>
fmt.Printf(<span class="hljs-string">"это число %f типа %T"</span>, a, a)
<span class="hljs-comment">// вывод: это число 100.123456 типа float64</span>

<span class="hljs-keyword">var</span> a1 <span class="hljs-keyword">byte</span> = <span class="hljs-string">'s'</span>
<span class="hljs-keyword">var</span> a2 <span class="hljs-keyword">int</span> = <span class="hljs-number">1234</span>
fmt.Printf(<span class="hljs-string">"%q %b"</span>, a1, a2)
<span class="hljs-comment">// вывод: 's' 10011010010</span>


<span class="hljs-comment">// использование \n позволяет сделать перенос строки</span>
<span class="hljs-keyword">var</span> a1 <span class="hljs-keyword">string</span> = <span class="hljs-string">"123"</span>
<span class="hljs-keyword">var</span> a2 <span class="hljs-keyword">string</span> = <span class="hljs-string">"1234"</span>
fmt.Printf(<span class="hljs-string">"%q \n%s"</span>, a1, a2)
<span class="hljs-comment">// вывод: </span>
<span class="hljs-comment">// "123" </span>
<span class="hljs-comment">// 1234</span>
</code></pre></span></div>
      </div>
</div>
</div>
</article>
