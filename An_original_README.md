<html>
 <body role="document">

<div>
  <div>
    <h1>{fmt}</h1>
    <p>A modern formatting library</p>
   <a href="https://github.com/fmtlib/fmt/releases/download/10.0.0/fmt-10.0.0.zip"> Download </a>   
  </div>
</div>

  <div class="row">
 <div class="content">
 <h2>Just a quick note from Christopher Peters - i'm just copying from their main website for tribute - but i need a PKGBUILD and didnt know how to put this onto my cachyOS install so had to learn a little bit</h2>     
  <section id="overview">
<h1>Overview<a class="headerlink" href="#overview" title="Permalink to this headline">¶</a></h1>
<p><strong>{fmt}</strong> is an open-source formatting library providing a fast and safe
alternative to C stdio and C++ iostreams.</p>
<div class="panel panel-default">
  <div class="panel-heading">What users say:</div>
  <div class="panel-body">
    Thanks for creating this library. It’s been a hole in C++ for
    a long time. I’ve used both <code>boost::format</code> and
    <code>loki::SPrintf</code>, and neither felt like the right answer.
    This does.
  </div>
</div><section id="format-api">
<span id="format-api-intro"></span><h2>Format API<a class="headerlink" href="#format-api" title="Permalink to this headline">¶</a></h2>
<p>The format API is similar in spirit to the C <code class="docutils literal notranslate"><span class="pre">printf</span></code> family of function but
is safer, simpler and several times <a class="reference external" href="https://www.zverovich.net/2020/06/13/fast-int-to-string-revisited.html">faster</a>
than common standard library implementations.
The <a class="reference external" href="syntax.html">format string syntax</a> is similar to the one used by
<a class="reference external" href="https://docs.python.org/3/library/stdtypes.html#str.format">str.format</a> in
Python:</p>
<div class="highlight-c++ notranslate"><div class="highlight"><pre><span></span><span class="n">std</span><span class="o">::</span><span class="n">string</span><span class="w"> </span><span class="n">s</span><span class="w"> </span><span class="o">=</span><span class="w"> </span><span class="n">fmt</span><span class="o">::</span><span class="n">format</span><span class="p">(</span><span class="s">&quot;The answer is {}.&quot;</span><span class="p">,</span><span class="w"> </span><span class="mi">42</span><span class="p">);</span>
</pre></div>
</div>
<p>The <code class="docutils literal notranslate"><span class="pre">fmt::format</span></code> function returns a string “The answer is 42.”. You can use
<code class="docutils literal notranslate"><span class="pre">fmt::memory_buffer</span></code> to avoid constructing <code class="docutils literal notranslate"><span class="pre">std::string</span></code>:</p>
<div class="highlight-c++ notranslate"><div class="highlight"><pre><span></span><span class="k">auto</span><span class="w"> </span><span class="n">out</span><span class="w"> </span><span class="o">=</span><span class="w"> </span><span class="n">fmt</span><span class="o">::</span><span class="n">memory_buffer</span><span class="p">();</span>
<span class="n">fmt</span><span class="o">::</span><span class="n">format_to</span><span class="p">(</span><span class="n">std</span><span class="o">::</span><span class="n">back_inserter</span><span class="p">(</span><span class="n">out</span><span class="p">),</span>
<span class="w">          </span><span class="s">&quot;For a moment, {} happened.&quot;</span><span class="p">,</span><span class="w"> </span><span class="s">&quot;nothing&quot;</span><span class="p">);</span>
<span class="k">auto</span><span class="w"> </span><span class="n">data</span><span class="w"> </span><span class="o">=</span><span class="w"> </span><span class="n">out</span><span class="p">.</span><span class="n">data</span><span class="p">();</span><span class="w"> </span><span class="c1">// pointer to the formatted data</span>
<span class="k">auto</span><span class="w"> </span><span class="n">size</span><span class="w"> </span><span class="o">=</span><span class="w"> </span><span class="n">out</span><span class="p">.</span><span class="n">size</span><span class="p">();</span><span class="w"> </span><span class="c1">// size of the formatted data</span>
</pre></div>
</div>
<p>The <code class="docutils literal notranslate"><span class="pre">fmt::print</span></code> function performs formatting and writes the result to a stream:</p>
<div class="highlight-c++ notranslate"><div class="highlight"><pre><span></span><span class="n">fmt</span><span class="o">::</span><span class="n">print</span><span class="p">(</span><span class="n">stderr</span><span class="p">,</span><span class="w"> </span><span class="s">&quot;System error code = {}</span><span class="se">\n</span><span class="s">&quot;</span><span class="p">,</span><span class="w"> </span><span class="n">errno</span><span class="p">);</span>
</pre></div>
</div>
<p>If you omit the file argument the function will print to <code class="docutils literal notranslate"><span class="pre">stdout</span></code>:</p>
<div class="highlight-c++ notranslate"><div class="highlight"><pre><span></span><span class="n">fmt</span><span class="o">::</span><span class="n">print</span><span class="p">(</span><span class="s">&quot;Don&#39;t {}</span><span class="se">\n</span><span class="s">&quot;</span><span class="p">,</span><span class="w"> </span><span class="s">&quot;panic&quot;</span><span class="p">);</span>
</pre></div>
</div>
<p>The format API also supports positional arguments useful for localization:</p>
<div class="highlight-c++ notranslate"><div class="highlight"><pre><span></span><span class="n">fmt</span><span class="o">::</span><span class="n">print</span><span class="p">(</span><span class="s">&quot;I&#39;d rather be {1} than {0}.&quot;</span><span class="p">,</span><span class="w"> </span><span class="s">&quot;right&quot;</span><span class="p">,</span><span class="w"> </span><span class="s">&quot;happy&quot;</span><span class="p">);</span>
</pre></div>
</div>
<p>You can pass named arguments with <code class="docutils literal notranslate"><span class="pre">fmt::arg</span></code>:</p>
<div class="highlight-c++ notranslate"><div class="highlight"><pre><span></span><span class="n">fmt</span><span class="o">::</span><span class="n">print</span><span class="p">(</span><span class="s">&quot;Hello, {name}! The answer is {number}. Goodbye, {name}.&quot;</span><span class="p">,</span>
<span class="w">           </span><span class="n">fmt</span><span class="o">::</span><span class="n">arg</span><span class="p">(</span><span class="s">&quot;name&quot;</span><span class="p">,</span><span class="w"> </span><span class="s">&quot;World&quot;</span><span class="p">),</span><span class="w"> </span><span class="n">fmt</span><span class="o">::</span><span class="n">arg</span><span class="p">(</span><span class="s">&quot;number&quot;</span><span class="p">,</span><span class="w"> </span><span class="mi">42</span><span class="p">));</span>
</pre></div>
</div>
<p>If your compiler supports C++11 user-defined literals, the suffix <code class="docutils literal notranslate"><span class="pre">_a</span></code> offers
an alternative, slightly terser syntax for named arguments:</p>
<div class="highlight-c++ notranslate"><div class="highlight"><pre><span></span><span class="k">using</span><span class="w"> </span><span class="k">namespace</span><span class="w"> </span><span class="nn">fmt</span><span class="o">::</span><span class="nn">literals</span><span class="p">;</span>
<span class="n">fmt</span><span class="o">::</span><span class="n">print</span><span class="p">(</span><span class="s">&quot;Hello, {name}! The answer is {number}. Goodbye, {name}.&quot;</span><span class="p">,</span>
<span class="w">           </span><span class="s">&quot;name&quot;</span><span class="n">_a</span><span class="o">=</span><span class="s">&quot;World&quot;</span><span class="p">,</span><span class="w"> </span><span class="s">&quot;number&quot;</span><span class="n">_a</span><span class="o">=</span><span class="mi">42</span><span class="p">);</span>
</pre></div>
</div>
</section>
<section id="safety">
<span id="id1"></span><h2>Safety<a class="headerlink" href="#safety" title="Permalink to this headline">¶</a></h2>
<p>The library is fully type safe, automatic memory management prevents buffer
overflow, errors in format strings are reported using exceptions or at compile
time. For example, the code</p>
<div class="highlight-c++ notranslate"><div class="highlight"><pre><span></span><span class="n">fmt</span><span class="o">::</span><span class="n">format</span><span class="p">(</span><span class="s">&quot;The answer is {:d}&quot;</span><span class="p">,</span><span class="w"> </span><span class="s">&quot;forty-two&quot;</span><span class="p">);</span>
</pre></div>
</div>
<p>throws the <code class="docutils literal notranslate"><span class="pre">format_error</span></code> exception because the argument <code class="docutils literal notranslate"><span class="pre">&quot;forty-two&quot;</span></code> is a
string while the format code <code class="docutils literal notranslate"><span class="pre">d</span></code> only applies to integers.</p>
<p>The code</p>
<div class="highlight-c++ notranslate"><div class="highlight"><pre><span></span><span class="n">format</span><span class="p">(</span><span class="n">FMT_STRING</span><span class="p">(</span><span class="s">&quot;The answer is {:d}&quot;</span><span class="p">),</span><span class="w"> </span><span class="s">&quot;forty-two&quot;</span><span class="p">);</span>
</pre></div>
</div>
<p>reports a compile-time error on compilers that support relaxed <code class="docutils literal notranslate"><span class="pre">constexpr</span></code>.
See <a class="reference external" href="api.html#compile-time-format-string-checks">here</a> for details.</p>
<p>The following code</p>
<div class="highlight-c++ notranslate"><div class="highlight"><pre><span></span>fmt::format(&quot;Cyrillic letter {}&quot;, L&#39;\x42e&#39;);
</pre></div>
</div>
<p>produces a compile-time error because wide character <code class="docutils literal notranslate"><span class="pre">L'\x42e'</span></code> cannot be
formatted into a narrow string. For comparison, writing a wide character to
<code class="docutils literal notranslate"><span class="pre">std::ostream</span></code> results in its numeric value being written to the stream
(i.e. 1070 instead of letter ‘ю’ which is represented by <code class="docutils literal notranslate"><span class="pre">L'\x42e'</span></code> if we
use Unicode) which is rarely desirable.</p>
</section>
<section id="compact-binary-code">
<h2>Compact Binary Code<a class="headerlink" href="#compact-binary-code" title="Permalink to this headline">¶</a></h2>
<p>The library produces compact per-call compiled code. For example
(<a class="reference external" href="https://godbolt.org/g/TZU4KF">godbolt</a>),</p>
<div class="highlight-c++ notranslate"><div class="highlight"><pre><span></span><span class="cp">#include</span><span class="w"> </span><span class="cpf">&lt;fmt/core.h&gt;</span>

<span class="kt">int</span><span class="w"> </span><span class="nf">main</span><span class="p">()</span><span class="w"> </span><span class="p">{</span>
<span class="w">  </span><span class="n">fmt</span><span class="o">::</span><span class="n">print</span><span class="p">(</span><span class="s">&quot;The answer is {}.&quot;</span><span class="p">,</span><span class="w"> </span><span class="mi">42</span><span class="p">);</span>
<span class="p">}</span>
</pre></div>
</div>
<p>compiles to just</p>
<div class="highlight-asm notranslate"><div class="highlight"><pre><span></span>main: # @main
  sub rsp, 24
  mov qword ptr [rsp], 42
  mov rcx, rsp
  mov edi, offset .L.str
  mov esi, 17
  mov edx, 1
  call fmt::v7::vprint(fmt::v7::basic_string_view&lt;char&gt;, fmt::v7::format_args)
  xor eax, eax
  add rsp, 24
  ret
.L.str:
  .asciz &quot;The answer is {}.&quot;
</pre></div>
</div>
</section>
<section id="portability">
<span id="id2"></span><h2>Portability<a class="headerlink" href="#portability" title="Permalink to this headline">¶</a></h2>
<p>The library is highly portable and relies only on a small set of C++11 features:</p>
<ul class="simple">
<li><p>variadic templates</p></li>
<li><p>type traits</p></li>
<li><p>rvalue references</p></li>
<li><p>decltype</p></li>
<li><p>trailing return types</p></li>
<li><p>deleted functions</p></li>
<li><p>alias templates</p></li>
</ul>
<p>These are available in GCC 4.8, Clang 3.4, MSVC 19.0 (2015) and more recent
compiler version. For older compilers use {fmt} <a class="reference external" href="https://github.com/fmtlib/fmt/releases/tag/4.1.0">version 4.x</a> which is maintained and
only requires C++98.</p>
<p>The output of all formatting functions is consistent across platforms.
For example,</p>
<div class="highlight-c++ notranslate"><div class="highlight"><pre><span></span><span class="n">fmt</span><span class="o">::</span><span class="n">print</span><span class="p">(</span><span class="s">&quot;{}&quot;</span><span class="p">,</span><span class="w"> </span><span class="n">std</span><span class="o">::</span><span class="n">numeric_limits</span><span class="o">&lt;</span><span class="kt">double</span><span class="o">&gt;::</span><span class="n">infinity</span><span class="p">());</span>
</pre></div>
</div>
<p>always prints <code class="docutils literal notranslate"><span class="pre">inf</span></code> while the output of <code class="docutils literal notranslate"><span class="pre">printf</span></code> is platform-dependent.</p>
</section>
<section id="ease-of-use">
<span id="id3"></span><h2>Ease of Use<a class="headerlink" href="#ease-of-use" title="Permalink to this headline">¶</a></h2>
<p>{fmt} has a small self-contained code base with the core library consisting of
just three header files and no external dependencies.
A permissive MIT <a class="reference external" href="https://github.com/fmtlib/fmt#license">license</a> allows
using the library both in open-source and commercial projects.</p>
<p><a class="reference external" href="contents.html">Learn more…</a></p>
<a class="btn btn-success" href="https://github.com/fmtlib/fmt">GitHub Repository</a>

<div class="section footer">
  
   </div>
  </div>
</div>
    <div class="footer" role="contentinfo">
        &copy; Copyright 2012-present, Victor Zverovich.
      Created using <a href="http://sphinx-doc.org/">Sphinx</a> 3.3.0.
    </div>


  </body>
</html>
