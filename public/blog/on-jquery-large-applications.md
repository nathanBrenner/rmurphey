# On jQuery & Large Applications

<p><em>Update: I&rsquo;ve written a separate post on the wisdom of <a href="http://blog.rebeccamurphey.com/on-rolling-your-own">rolling your own</a> large application toolkit that incorporates jQuery.</em></p>

<p>I&rsquo;ve been thinking a lot lately about JavaScript applications. As my skills have evolved, I&rsquo;ve had the privilege of working on more actual applications, and I&rsquo;ve gotten further and further from clients who want to add a bit of Ajax or bling to an otherwise fairly traditional web site.</p>

<p>The most interesting applications I work on are client-side intensive: the server is responsible for providing data as JSON to the client, and most everything else &mdash; templating, state management, data management, site navigation, and of course user interaction &mdash; is left to the client side.</p>

<p>It&rsquo;s a lovely way of writing an application. There&rsquo;s no need for me to touch server-side code; in some cases I work with a server-side developer to decide what the data they send will look like, but in others I just take what an API already provides and make it work. I get to use the same templating framework across projects, regardless of server-side technology, and I can prototype complex interactions before the server side even exists.</p>

<p>This is a land where HTML, CSS, and JavaScript are almost all you need, and I like it. I&rsquo;ve become a firm believer in moving giant hunks of functionality that used to belong to the server over to the client. For a variety of reasons, I think it&rsquo;s clear that this is where most interesting web development is headed, to the extent it&rsquo;s not already there.</p>

<hr />

<p>This style of building an application changes the front-end development game. In fact, &ldquo;development&rdquo; may no longer be an adequate description; we&rsquo;re moving into the realm of engineering, here. We&rsquo;re not using JavaScript to add a bit of bling to our sites &mdash; a slideshow here, some Ajax there &mdash; we&rsquo;re architecting an <em>application</em>, damnit. We can&rsquo;t just write some procedural code that binds a bunch of anonymous functions to some events and call it a day; if we do, I can tell you from experience that we&rsquo;re going to end up with a steaming pile of unmaintainable crap.</p>

<p>Among a host of questions presented by these sorts of applications, some of the most interesting to me are:</p>

<ul>
<li>What are the units of functionality that will make up the application?</li>
<li>How will those pieces be organized into units of code?</li>
<li>How will those pieces communicate with each other?</li>
<li>How will dependencies between components be expressed and managed while adhering to the principle of loose coupling?</li>
<li>How will components manifest themselves in the DOM? Do they need to?</li>
<li>How will we persist data across URL and page loads?</li>
<li>How will we manage communication with the server?</li>
<li>How will we make sure users only see the data they&rsquo;re allowed to see?</li>
</ul>


<p>At the risk of making a broad generalization, this isn&rsquo;t the way today&rsquo;s average JavaScripter learned to think. The mantra of jQuery, the most popular JavaScript library on the internets, is &ldquo;get some elements, do something with them&rdquo; &mdash; perfectly terrible preparation for analyzing an application from a perspective other than the DOM. And, IMHO, therein lies a tremendous problem.</p>

<hr />

<p>As more and more application logic moves to the browser, I&rsquo;m eager to see the JavaScript community rise to the challenge, but instead it feels like the opposite is happening. People with little understanding or appreciation of these questions are taking on projects that demand these questions be answered. The result is a land of fragile code that gets the job done while giving the finger to the next developer; a land of code so tightly coupled, so deeply beholden to the DOM, so blatantly not reusable or extensible or maintainable as to render every subsequent commit a complete crapshoot, as liable to cripple the application as not. The viability of the project is threatened, and so is the reputation of JavaScript.</p>

<p>We are better than this. JavaScript, even that old-fashioned browser kind, is a language worthy of respect, not a thing to be dreaded. But &mdash; and here&rsquo;s the sentence I have struggled 10 months to realize and an hour to write: in order to prove that we are better than this, we must make abundantly clear to the budding developers, to the project managers, to the enterprises, to anyone intending to build a remotely complex JavaScript application, that there&rsquo;s more to JavaScript than jQuery. The questions are bigger, the answers more complex, and the relevant skills, alas, a bit harder to come by.</p>

<p>We have to make clear that, in fact, jQuery is but a hammer. When it comes to building these intensively client-side applications, we&rsquo;re talking about building skyscrapers, for god&rsquo;s sake. The problems solved by a hammer are the least of our concerns.</p>

<hr />

<p>It was just a few months ago that I gave a presentation on <a href="http://www.slideshare.net/rmurphey/building-large-jquery-applications">building large jQuery applications</a>. I emphasized jQuery&rsquo;s role as strictly a DOM and Ajax tool, and demonstrated a few other tools &mdash; John Resig&rsquo;s <a href="http://ejohn.org/blog/simple-javascript-inheritance/">simple inheritance</a>, James Burke&rsquo;s <a href="http://requirejs.org/">RequireJS</a> dependency management and build tool, Jan Lenhardt&rsquo;s <a href="http://github.com/janl/mustache.js/">mustache.js</a> &mdash; that one would want to bring to the table for such an undertaking.</p>

<p>But to what end do we assemble said hodgepodge of tools? Is it just so we can continue to &ldquo;use jQuery&rdquo;?</p>

<p>jQuery&rsquo;s API is, indeed, dead-simple, but we are smart people! We are building skyscrapers! When it&rsquo;s time to write a complex application, and we need all of these things that jQuery doesn&rsquo;t offer, can we not learn to use another hammer &mdash; learn that <code>dojo.place('&lt;div&gt;I am new!&lt;/div&gt;', oldDomElement, 'last')</code> means the same thing as <code>$('&lt;div&gt;I am new!&lt;/div&gt;').appendTo(oldDomElement)</code> &mdash; if learning it gives us access to legions more functionality than jQuery even aspires to provide?</p>

<p>Do we assemble this hodgepodge because finding jQuery developers is perceived as an easier task than finding practitioners of another library, even though someone saying they &ldquo;know jQuery&rdquo; is little indication that they will know how to work with the assembled solution?</p>

<p>Do we do it for the plugin ecosystem &mdash; full of code of varying quality and maintenance &mdash; even though many of the large application needs addressed by those plugins are addressed by other libraries as well, and sometimes better?</p>

<p>And when we do it, when we assemble this collection of tools ourselves, what risks are we accepting? What price will we pay down the road to maintain three or five or 10 different pieces from three or five or 10 different authors, with different release cycles, no guarantee of compatibility or maintenance, and no central project thoughtfully considering their future?</p>

<hr />

<p>I&rsquo;ve wrestled with these questions for months, agonizing during sleepless early-morning hours over how to advise clients on the answers. I&rsquo;m the co-host of yayQuery, a contributor to the jQuery Cookbook, and, I&rsquo;ll venture to say, a decently respected member of the jQuery community. I did not arrive at this conclusion lightly, and I have few illusions it will be well-received, or even heeded.</p>

<p>But I&rsquo;ve grown weary of people championing a tool that simply does not answer the big questions I see in project after intensively client-side project. I&rsquo;ve grown weary of those same people dismissing tools that answer those questions handily and have been answering them for a while now. I cringe when clients tell me they&rsquo;ve chosen jQuery because it was &ldquo;easy,&rdquo; and then watch them predictably struggle with all of the questions it does not answer. And I&rsquo;ve found I can&rsquo;t continue to bite my tongue when people recommend jQuery as an enterprise-grade solution while failing to acknowledge these questions, let alone answer them*.</p>

<hr />

<p>I do not want to see jQuery go away. The simplicity of its API was undeniably instrumental in the rise of JavaScript as a language these last few years. It is a perfect gateway drug, and I greatly enjoy watching people transition from &ldquo;get some elements, do something with them&rdquo; to the elegant patterns of JavaScript itself.</p>

<p>jQuery is an entirely appropriate answer to so many questions, but it falls so short for large applications, forcing you to assemble such a tenuous toolkit of your own, that it simply isn&rsquo;t a viable answer &mdash; or, in my opinion, part of an answer &mdash; for large applications. If we hope to continue to gain respect as a community, we ought to admire jQuery&rsquo;s immense contributions, but we must not be afraid to accept and make very clear its limitations. We do otherwise at our peril.</p>

<hr />

<p><em>*An aside: To its credit, <a href="http://jupiterit.com">JupiterIT</a> has put forward <a href="http://javascriptmvc.com">JavaScriptMVC</a>, the only substantive attempt I&rsquo;ve seen at answering these large application questions using jQuery. I applaud them, but fear their efforts will continue to be somewhat isolated without the support and endorsement of the wider jQuery community. If you have read this far and still have your heart set on a jQuery-centric large application solution, you should by all means take a look at JavaScriptMVC.</em></p>